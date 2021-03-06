# WASP Architecture

This page describes the WASP v2 architecture and the changes that were undertaken as part of the major redesign from WASP v1.

## WASP version 2

`WASP` version 2 aims to rectify all of the issues with version 1 by refactoring the code-base and splitting out the concerns into separate micro-services. Specifically:

- Splitting out the ingest pipeline so that the ingest mechanism, routing and payload parsing are handled by separately scalable services.
- Separate concerns around sensors, readings, events and the evaluation of dependent datasets into separate microservices with there own abstracted datastores.
- Separate notification mechanisms out into their own services so that they can be deployed onto dependent infrastructure as necessary.
- Refactor the infrastructure into a platform agnostic Kubernetes based infrastructure.

The version 2 of the WASP architecture is designed as follows:

![Architecture Diagram v2](../assets/architecture-v2.svg)

Note the following deviations of the current codebase from this architecture:

1. The dependency calculation process and dependency event generation used to be handled by the `wasp-packet-forwarder` which has been removed. Work to develop the dependency calculator services and re-instate these features in a generic way is planned for completion soon.

## Problems with the version 1 architecture and motivation for change

The first version of `WASP` (see [Version 1 architecture](#version-1-architecture)) had many architectural issues. Notably:

- Lack of network abstraction with hardcoded data-structures that could only support LoRaWAN networks and devices.
- Tight coupling between different services via their shared interaction with `wasp-database`.
- Tight coupling of the infrastructure to AWS specific services such as ECS and SES.
- `wasp-packet-forwarder` cannot be scaled as only one service may subscribe to the TTN mqtt broker else we get duplicate messages.
- `wasp-client` was a mess, built around specific end-user goals that the team tried (and mostly failed) to generify.
- `wasp-api` acted as the central interaction point for all user actions. It was bloated and definitely not singularly concerned.
- `wasp-api` only supported a graphql interface making it difficult for users not familiar with that query language to engage with the platform.
- Dependent datasets associated with `assets` and not `sensors` were evaluated at query time. This led to poor query performance that didn't scale.

## Version 1 architecture

Version 1 of the WASP was architected as follows

![Architecture Diagram](../assets/architecture-v1.svg)

### wasp-packet-forwarder

This service processes sensor payloads and evaluates those payloads to determine if any events should be raised against the asset(s) connected to that sensor

### [wasp-api](https://github.com/digicatapult/wasp-api)

This service acts as the control interface for the platform and handles all user requests. It can be used to:

- register new sensors with the platform
- create/edit/delete assets
- attach/detach sensors from assets
- set thresholds for asset condition alerts
- query readings; both at an asset and sensor level
- query asset events
- manage user credentials within the platform

### wasp-client

The client is the main user interface for `WASP` and allows end users to

- Create and edit assets
- Assign sensors to assets
- View sensor readings associated with assets
- View/resolve alerts and other events

### wasp-database
`WASP` v1 uses a PostgreSQL database at its core to store all persistent data. This module allows the `WASP` services to both provision and use the database ensuring its compatibility with the service.
