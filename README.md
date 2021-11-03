# **W**ide-**A**rea-**S**ensor-**P**latform (WASP)

`WASP` is the **W**ide-**A**rea-**S**ensor-**P**latform; an end-to-end solution for condition monitoring using `IoT` technology. The platform supports numerous device types with an extensible system for adding more. The platform is a complete `IoT` monitoring solution including features like:

- Provisioning new devices (`things`)
- Assignment of `things` to the assets that the user actually cares about
- Payload processing of `thing` packets to time series readings
- Threshold setting and events
- Tracking events when assets move between locations

## READMEs

This repo includes READMEs that explain concepts within WASP:

- [Architecture](./docs/architecture.md)
- [Ingest](./docs/ingest.md)
- [Payload Parsing](./docs/payloadParsing.md)
- [Kafka Message Flow](./docs/kafkaFlow.md)

## Repositories

### Active WASP repositories

These repositories contain code being actively maintained as part of the WASP project.

| Repository                                                                                    | Description                                                                                                            |
| --------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| [wasp-documentation](https://github.com/digicatapult/wasp-documentation)                       | Documentation for WASP platform                                                                                        |
| [wasp-service-template](https://github.com/digicatapult/wasp-service-template)                 | Template repository for building new WASP services                                                                     |
| [wasp-testing](https://github.com/digicatapult/wasp-testing)                                   | Platform tests for WASP                                                                                                |
| [wasp-thing-service](https://github.com/digicatapult/wasp-thing-service)                       | Thing service for WASP                                                                                                 |
| [wasp-user-service](https://github.com/digicatapult/wasp-user-service)                         | User service for WASP                                                                                                  |
| [wasp-reading-service](https://github.com/digicatapult/wasp-reading-service)                   | Readings service for WASP                                                                                              |
| [wasp-event-service](https://github.com/digicatapult/wasp-event-service)                       | Event service for WASP                                                                                                 |
| [wasp-ws-reading-service](https://github.com/digicatapult/wasp-ws-reading-service)             | Web socket service for streaming WASP readings                                                                         |
| [wasp-ws-event-service](https://github.com/digicatapult/wasp-ws-event-service)                 | Web socket service for streaming WASP events                                                                           |
| [wasp-authentication-service](https://github.com/digicatapult/wasp-authentication-service)     | Authentication service for WASP                                                                                        |
| [wasp-open-api](https://github.com/digicatapult/wasp-open-api)                                 | Amalgamated API specs for WASP                                                                                         |
| [wasp-api](https://github.com/digicatapult/wasp-api)                                           | GraphQL API service for WASP                                                                                           |
| [wasp-routing-service](https://github.com/digicatapult/wasp-routing-service)                   | Identifies the thing that produced a message for an ingest and routes that payload to an appropriate payload processor |
| [wasp-ingest-mqtt](https://github.com/digicatapult/wasp-ingest-mqtt)                           | MQTT ingest for WASP                                                                                                   |
| [wasp-ingest-ttn](https://github.com/digicatapult/wasp-ingest-ttn)                             | WASP Ingest for TTN v2                                                                                                 |
| [wasp-ingest-nordic-cloud](https://github.com/digicatapult/wasp-ingest-nordic-cloud)           | WASP Ingest for nRF Cloud                                                                                              |
| [wasp-ingest-http](https://github.com/digicatapult/wasp-ingest-http)                           | WASP Ingest that accepts new messages via HTTP POST from a gateway service                                         |
| [wasp-payload-parser-template](https://github.com/digicatapult/wasp-payload-parser-template)   | Template repository for bootstrapping new WASP payload parsers                                                         |
| [wasp-payload-processor](https://github.com/digicatapult/wasp-payload-processor)               | Service builder for WASP payload processors                                                                            |
| [wasp-thingy91](https://github.com/digicatapult/wasp-thingy91)                                 | A payload parsing service for Thingy91 devices                                                                      |
| [wasp-payload-parser-oyster2](https://github.com/digicatapult/wasp-payload-parser-oyster2)     | A payload parsing service for Digital Matter Oyster2 devices                                                        |
| [wasp-deti-power](https://github.com/digicatapult/wasp-deti-power)                             | A payload parsing service for Schneider Electric power meters                                                       |
| [resolver-cache-datasource](https://github.com/digicatapult/resolver-cache-datasource)         | Resolver caching DataSource for Apollo GraphQL projects                                                                |
| [apollo-type-validation-plugin](https://github.com/digicatapult/apollo-type-validation-plugin) | Directive base type validations for GraphQL queries                                                                    |

## Contributing

If you want to contribute to `WASP` that's brilliant! First of all have a look at our contributor guidelines [here](./CONTRIBUTING.md).

## Lingo

The world of `IoT` is full of lingo (see we can't even write a sentence without an acronym). Here's our glossary of what we mean by some of these terms:

| Term   | Means                                                                                                                                                                                                                                                           |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IoT    | The Internet of things is a system of interrelated computing devices, mechanical and digital machines provided with unique identifiers (UIDs) and the ability to transfer data over a network without requiring human-to-human or human-to-computer interaction |
| Thing  | A device that communicates readings of the environment over LoRaWAN. Elsewhere this may be referred to as a device or node                                                                                                                                      |
| Sensor | The term used in WASP v1 for `things`                                                                                                                                                                                                                           |
| Asset  | The real world thing that the user is actually trying to monitor the environment of. This could be a building, a cow, a pizza or anything else                                                                                                                  |
