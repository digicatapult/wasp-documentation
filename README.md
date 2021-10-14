# **W**ide-**A**rea-**S**ensor-**P**latform (WASP)

`WASP` is the **W**ide-**A**rea-**S**ensor-**P**latform; an end-to-end solution for condition monitoring using `IoT` technology. The platform supports numerous device types with an extensible system for adding more. The platform is a complete `IoT` monitoring solution including features like:

- Provisioning new devices (`things`)
- Assignment of `things` to the assets that the user actually cares about
- Payload processing of `thing` packets to time series readings
- Threshold setting and events
- Tracking events when assets move between locations

## Quick-start

The latest version of WASP is deployed via a Kubernetes based infrastructure. Documentation for getting up and running with this can be found in the [wasp-k8s-infra](https://github.com/digicatapult/wasp-k8s-infra/) repository

## READMEs

This repo includes READMEs that explain concepts within WASP:

- [Architecture](./docs/architecture.md)
- [Ingest](./docs/ingest.md)
- [Payload Parsing](./docs/payloadParsing.md)
- [Kafka Message Flow](./docs/kafkaFlow.md)

## Repositories

### Active WASP repositories

These repositories contain code being actively maintained as part of the wasp project

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
| [wasp-ingest-http](https://github.com/digicatapult/wasp-ingest-http)                           | WASP Ingest for that accepts new messages via HTTP POST from a gateway service                                         |
| [wasp-payload-parser-template](https://github.com/digicatapult/wasp-payload-parser-template)   | Template repository for bootstrapping new WASP payload parsers                                                         |
| [wasp-payload-processor](https://github.com/digicatapult/wasp-payload-processor)               | Service builder for WASP payload processors                                                                            |
| [wasp-thingy91](https://github.com/digicatapult/wasp-thingy91)                                 | A payload processing service for Thingy91 devices                                                                      |
| [wasp-payload-parser-oyster2](https://github.com/digicatapult/wasp-payload-parser-oyster2)     | A payload processing service for Digital Matter Oyster2 devices                                                        |
| [wasp-deti-power](https://github.com/digicatapult/wasp-deti-power)                             | A payload processing service for Schneider Electric power meters                                                       |
| [wasp-database](https://github.com/digicatapult/wasp-database)                                 | Database component for the WASP platform                                                                               |
| [resolver-cache-datasource](https://github.com/digicatapult/resolver-cache-datasource)         | Resolver caching DataSource for Apollo GraphQL projects                                                                |
| [apollo-type-validation-plugin](https://github.com/digicatapult/apollo-type-validation-plugin) | Directive base type validations for GraphQL queries                                                                    |
| [wasp-k8s-tf](https://github.com/digicatapult/wasp-k8s-tf)                                     | Terraform HCL for deploying a new WASP Kubernetes cluster                                                              |
| [wasp-k8s-infra](https://github.com/digicatapult/wasp-k8s-infra)                               | FluxCD deployment repo for WASP                                                                                        |
| [wasp-cluster](https://github.com/digicatapult/wasp-cluster)                                   | k8s cluster dependencies for WASP                                                                                      |

### Outdated payload processor repositories

These repositories contain payload processor code used in WASP v1. These are now outdated but could be straightforwardly upgraded to be supported by WASP v2.

| Repository                                                                                          | Description                                      |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| [wasp-ewattch-energy-sensor](https://github.com/digicatapult/wasp-ewattch-energy-sensor)             | Tyness eWatch Energy sensor extension for WASP   |
| [wasp-ztrack-pro-sensor](https://github.com/digicatapult/wasp-ztrack-pro-sensor)                     | Zane zTrack Pro sensor extension for WASP        |
| [wasp-tektelic-agriculture-sensor](https://github.com/digicatapult/wasp-tektelic-agriculture-sensor) | Tektelic Argricultural sensor extension for WASP |
| [wasp-elsys-elt-ultrasonic-sensor](https://github.com/digicatapult/wasp-elsys-elt-ultrasonic-sensor) | Elsys ELT Ultrasonic sensor extension for WASP   |
| [wasp-dl-smtp-soil-sensor](https://github.com/digicatapult/wasp-dl-smtp-soil-sensor)                 | DecentLab DL-SMTP sensor extension for WASP      |
| [wasp-dl-5tm-soil-sensor](https://github.com/digicatapult/wasp-dl-5tm-soil-sensor)                   | DecentLab DL-5TM sensor extension for WASP       |
| [wasp-dl-atm41-weather-sensor](https://github.com/digicatapult/wasp-dl-atm41-weather-sensor)         | DecentLabs ATM41 sensor extension for WASP       |
| [wasp-dl-atm22-wind-sensor](https://github.com/digicatapult/wasp-dl-atm22-wind-sensor)               | DecentLabs ATM22 sensor extension for WASP       |
| [wasp-dl-mbx-ultrasonic-sensor](https://github.com/digicatapult/wasp-dl-mbx-ultrasonic-sensor)       | DecentLab DL-MBX sensor extension for WASP       |

### Deprecated repositories from WASP v1

These repositories are documented here for posterity but are otherwise redundant or so out of date as to justify being entirely rewritten.

| Repository                                                                            | Description                                                                                  |
| ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| [wasp-infrastructure](https://github.com/digicatapult/wasp-infrastructure)             | Terraform HCL for WASP v1                                                                    |
| [wasp-client](https://github.com/digicatapult/wasp-client)                             | Web client for WASP v1                                                                       |
| [wasp-packet-forwarder](https://github.com/digicatapult/wasp-packet-forwarder)         | Ingest service for WASP v1                                                                   |
| [wasp-siconia-omni](https://github.com/digicatapult/wasp-siconia-omni)                 | WASP sensor extension supporting Sagemcom Siconia sensors programmed with DC "omni" firmware |
| [wasp-csv-global-generator](https://github.com/digicatapult/wasp-csv-global-generator) | CSV download generator for WASP v1                                                           |
| [wasp-siconia](https://github.com/digicatapult/wasp-siconia)                           | Repo for Sagemcom Siconia devices                                                            |
| [wasp-ttn-cli-wrapper](https://github.com/digicatapult/wasp-ttn-cli-wrapper)           | Proxy service for ttn v3 cli                                                                 |
| [wasp-ar](https://github.com/digicatapult/wasp-ar)                                     | AR experiment using WASP v1                                                                  |
| [wasp-client-assets](https://github.com/digicatapult/wasp-client-assets)               | repo for per-client assets used in deployed WASP                                             |

## Contributing

If you want to contribute to `WASP` that's brilliant! First of all have a look at our contributor guidelines [here](./CONTRIBUTING.md).

If you want to contribute code changes you'll need to get a valid development setup by following the instructions in the [wasp-k8s-infra](https://github.com/digicatapult/wasp-k8s-infra/) repository.

## Lingo

The world of `IoT` is full of lingo (see we can't even write a sentence without an acronym). Here's our glossary of what we mean by some of these terms:

| Term   | Means                                                                                                                                                                                                                                                           |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IoT    | The Internet of things is a system of interrelated computing devices, mechanical and digital machines provided with unique identifiers (UIDs) and the ability to transfer data over a network without requiring human-to-human or human-to-computer interaction |
| Thing  | A device that communicates readings of the environment over LoRaWAN. Elsewhere this may be referred to as a device or node                                                                                                                                      |
| Sensor | The term used in WASP v1 for `things`                                                                                                                                                                                                                           |
| Asset  | The real world thing that the user is actually trying to monitor the environment of. This could be a building, a cow, a pizza or anything else                                                                                                                  |
