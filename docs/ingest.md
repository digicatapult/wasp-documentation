# WASP Ingests

WASP ingest services are the point of entry for `thing` payload data into WASP, such as temperature and GPS readings from a sensor. An ingest service receives messages from whichever network the `thing` sends its messages to, and parses these messages into a generic format for WASP. Finally, it forwards payloads (via Kafka) to [`wasp-routing-service`](https://github.com/digicatapult/wasp-routing-service), which routes (again via Kafka) to the appropriate [`wasp-payload-processor`](https://github.com/digicatapult/wasp-payload-processor) for the `thing` from which each message originated. Splitting the ingesting and processing of payloads is necessary because a `thing`'s payloads can be ingested through any number of different services and networks, but its 'actual' payload data (readings and events) can be handled by a `thing`-specific payload processor.

## Architecture

See [architecture](./architecture.md). Ingest is located in box 2.


# Active WASP ingest repositories

| Repository                                                                          | Description               |
| ----------------------------------------------------------------------------------- | ------------------------- |
| [wasp-ingest-mqtt](https://github.com/digicatapult/wasp-ingest-mqtt)                 | MQTT ingest for WASP      |
| [wasp-ingest-ttn](https://github.com/digicatapult/wasp-ingest-ttn)                   | WASP Ingest for TTN v2    |
| [wasp-ingest-nordic-cloud](https://github.com/digicatapult/wasp-ingest-nordic-cloud) | WASP Ingest for nRF Cloud |


# Writing a new ingest

A new ingest can be created by copying an existing ingest service and changing a few files. [wasp-ingest-nordic-cloud](https://github.com/digicatapult/wasp-ingest-nordic-cloud) will be used as an example.

There are three pieces of logic to implement along the message chain:

- Listening for a payload.
- Parsing the payload into the correct format.
- Forwarding the payload.

The message chain is composed in [`app/messagePipeline/index.js`](https://github.com/digicatapult/wasp-ingest-nordic-cloud/blob/main/app/messagePipeline/index.js).


## Listening for a payload

This can vary significantly depending on the protocol and environment the `thing` uses, although MQTT is common. [wasp-ingest-nordic-cloud](https://github.com/digicatapult/wasp-ingest-nordic-cloud) ingests from Nordic Cloud hosted MQTT brokers, using a wildcard to subscribe to multiple topics. [`MQTT.js`](https://www.npmjs.com/package/mqtt) manages connection and subscription. Environment variables set the MQTT endpoint, credentials and topic prefix.

See [`nordicCloud.js`](https://github.com/digicatapult/wasp-ingest-nordic-cloud/blob/main/app/messagePipeline/nordicCloud.js).

## Parsing the payload

Payloads should be parsed into the following format before forwarding:

```
{
    ingestId: 'THING_DEVICE_ID', // String
    payload: {
        payloadId: 'UUID' // String (uuid)
        ingest: WASP_INGEST_NAME, // String (env) 
        ingestId: 'THING_DEVICE_ID', // String
        timestamp: '2021-08-31T14:51:36.507Z', // Date (ISO)
        payload: {}, // JSON object (actual payload data e.g. readings, events)
        metadata: {} // JSON object (catch all for other thing-specific important data)
    }
}
```

`payloadId` can be generated with [`uuid`](https://www.npmjs.com/package/uuid).

As WASP works with devices (things) from many different environments, it's necessary to maintain an ID for each `thing` to avoid potential clashes. `ingest` and `ingestId` are used by [`wasp-routing-service`](https://github.com/digicatapult/wasp-routing-service) to get WASP's ID for the `thing` that has sent a payload. `ingest` is the name that identifies an ingest throughout WASP (e.g. `nordic-cloud`, `ttn_v2`). `ingestId` is some kind of unique ID inherent to the device, usually set by its manufacturer (e.g. a device serial number or [devEui](https://lora-developers.semtech.com/library/tech-papers-and-guides/the-book/deveui/)). These should match what's been set in [`wasp-thing-service` database](https://github.com/digicatapult/wasp-thing-service/blob/main/docs/db.md).

See [`parser.js`](https://github.com/digicatapult/wasp-ingest-nordic-cloud/blob/main/app/messagePipeline/parser.js).

## Forwarding the payload

The payload is then forwarded to a Kafka topic (default: `raw-payloads`) which is consumed by [`wasp-routing-service`](https://github.com/digicatapult/wasp-routing-service). `clientId` for the Kafka instance should be set to something unique for this ingest e.g. `ingest-{WASP_INGEST_NAME}`.

See [`forwarder.js`](https://github.com/digicatapult/wasp-ingest-nordic-cloud/blob/main/app/messagePipeline/forwarder.js).