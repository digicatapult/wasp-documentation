# WASP Payload Parsing

WASP payload parsers are where ingested `thing` payload data is parsed and reformatted as readings or events (or ignored), then forwarded (via Kafka) to [`wasp-reading-service`](https://github.com/digicatapult/wasp-reading-service) or [`wasp-event-service`](https://github.com/digicatapult/wasp-event-service). Each `thing` has its own payload-parser e.g. [wasp-thingy91](https://github.com/digicatapult/wasp-thingy91) is a payload parser for [Nordic Thingy:91](https://www.nordicsemi.com/Products/Development-hardware/Nordic-Thingy-91) prototyping devices. 


## Architecture

See [architecture](./architecture.md). Payload parsing is located in box 4.


# Active WASP payload parser repositories

## Parsers

| Repository                                                            | Description               |
| --------------------------------------------------------------------- | ------------------------- |
| [wasp-thingy91](https://github.com/digicatapult/wasp-thingy91)         | A payload processing service for Thingy91 devices               |
| [wasp-deti-power](https://github.com/digicatapult/wasp-deti-power)     | A payload processing service for Schneider Electric power meters|

## Templates and builders

| Repository                                                                                  | Description               |
| ------------------------------------------------------------------------------------------- | ------------------------- |
| [wasp-payload-parser-template](https://github.com/digicatapult/wasp-payload-parser-template) | Template repository for bootstrapping new WASP payload parsers|
| [wasp-payload-processor](https://github.com/digicatapult/wasp-payload-processor)             | Service builder for WASP payload parsers (used in template)   |


# Writing a new parser
Follow the README in [wasp-payload-parser-template](https://github.com/digicatapult/wasp-payload-parser-template) to generate a new repo.

Change `payloadProcessor` in [`app/server.js`](https://github.com/digicatapult/wasp-payload-parser-template/blob/main/app/server.js) to parse the new `thing` payload data into readings and events. Unimportant payloads can also be set to be ignored.


## Incoming format
Payloads are received via Kafka from [wasp-routing-service](https://github.com/digicatapult/wasp-routing-service) with the following format:

```
{
    thingId: 'THING_ID' // String (uuid)
    timestamp: '2021-08-31T14:51:36.507Z', // Date (ISO)
    payload: {}, // JSON object (actual payload data to parse e.g. readings, events)
    metadata: {} // JSON object (catch-all for other thing-specific important data)
}
```

## Outgoing format

The `payloadProcessor` function must return an object of type `PayloadProcessorResult` which contains descriptions of readings and events to be published. See [`wasp-payload-processor`](https://github.com/digicatapult/wasp-payload-processor/blob/main/README.md#message-format) for type signatures of the outgoing format.

An example of how `app/server.js` can look:

```js
const { buildService } = require('@digicatapult/wasp-payload-processor')

buildService({
    sensorType: WASP_SENSOR_TYPE, // identifying name for the `thing` across WASP e.g. `thingy91`
    payloadProcessor: ({ logger }) => ({ thingId, timestamp, payload }) => {
    const asBuffer = Buffer.from(payload, 'base64')
    return {
      readings: [{
        dataset: {
          thingId,
          type: 'temperature',
          label: 'dataset-label-if-any',
        },
        timestamp,
        value: asBuffer[0],
      }]),
      events: [{
        thingId,
        timestamp,
        type: 'SHOCK',
        details: { arbitrary: "details" }
      }]
  },
})
```