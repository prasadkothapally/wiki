# Home
This is the root of the page-tree for all design documentation related to Fintrust

## Available components

```kroki-plantuml
@startmindmap
skinparam monochrome true
* Components
** AllFunds
*** Profile
*** Portfolio
*** Funds
*** Notifications
** Global
*** MFU Session Provider
** Accounting
*** API (api)
*** BackOffice (bo)
*** Analytics
** Technical
*** DLQ Processor
*** Event Publisher
** Utilities
*** PGBouncer
*** OpenObserve
*** Kestra
@endmindmap
```

### Purpose

The purpose of the components is as follows

Component            | Purpose
---------------------|-------
Profile              | Handles all aspects of a user in the AllFunds system
Portfolio            | Handles all aspects of a user's financial investments in the AllFunds system
Funds                | Handles all aspects of a Fund, it's proerties and performance
Notifications        | Handles all aspects of communication with the end users across various channels.
MFU Session Provider | A lightweight service for initialiazing and sharing a MFU session with various other components.
Accounting API       | Accounting system interface
Accounting BackOffice| Accounting system backoffice that heavy-lifts all the backoffie processing for data loads, fund analytics, reconciliations, investor analytics etc.
Accounting Analytics | Recolytics layer. Yet to be built.
DLQ Processor        | Handles message retries using backoffs across the system.
Event Publisher      | Traps the Mongo CDC streams and publishes the changes as Business events 
PGBouncer            | A postgres connection pooler
OpenObserve          | Log aggregations and visualizations
Kestra               | A task scheduler.

## API Reference

Please see this [The API documentation](https://fintrust-dev.techwave.net/swagger-ui) for all exposed REST APIs

## Principles

### SCM

 1. Every component has its own git project. Using a single git project and nested folders to manage resources of various kind is discouraged.
 2. Every git project results in an artifact. It maybe an executable, or a docker container or a Java archive or a Helm chart.
 3. Main is the default branch and is left unprotected for all devs to be able to commit.
 4. Trunk based development is followed. Main is the only branch. Devs can use other branches to build their features but this is not mandatory. Only the main branch is connected to the pipelines. This approach may change post go-live.
 
### CI

 1. Every git project has a build pipeline connected to it. 
 2. The build pipeline is setup using gitlab CI.
 3. Docker artifacts are stored in GitLab Container Registry
 4. Helm artifacts are stored in GitLab Package Registry
 5. Java artifacts (jars) are stored in Reposilite

### Versioning
 1. All components are versioned as 0.{SprintNumber}.{FixNumber} at the start of the sprint. These changes are made in the individual build and pipeline manifests (pom.xml and .gitlab-ci.yaml for example).
 2. The Helm chart's app version is adjusted to 0.{SprintNumber}.{FixNumber}
 3. The images referenced in the Helm chart are modified to use the 0.{SprintNumber}.{FixNumber} of each component.

 