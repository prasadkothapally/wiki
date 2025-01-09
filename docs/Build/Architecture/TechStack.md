# Stack

This page describes all the tools and technologies utilized for buiding the AllFunds application.

## Engineering Stack

Aspect                | Technology
----------------------|------------
Version Control       | GitLab (powered by techwave's gitlab instance) 
Backend CI/CD         | GitLab
Build                 | Maven
Code Coverage         | SonarQube
API Automation        | Karate
Perf. Automation      | K6
Documentation         | MkDocs
Diagrams as code      | Kroki, Mermaid, PlantUML
Diagrams              | Draw.io
Docker                | Docker Desktop (windows), Docker Engine (linux)
Kubernetes            | Docker Desktop (windows), Minikube (linux), EKS (aws cloud)
Kubernetes tools      | kubectl, helm, helm-dashboard
Java Artifact store   | Reposilite
Container Registry    | GitLab CR
Helm Package Registry | GitLab Package Registry
API Docs              | Open API 3.0



## Mobile App Engineering Stack

Aspect                | Technology
----------------------|------------
App CI/CD             | Fastlane
App BetaStore         | Firebase AppTester
Build                 | Gradle


## Application Backend Stack

Aspect                | Technology
----------------------|------------
Deployment            | AWS (for higher environments such as staging, perf, prod)
Deployment            | Minikube for DEV environment (1 node - 16 core, 32 GB RAM running on Techwave servers)
Deployment            | Docker Desktop for Local environment (4 core, 16 GB RAM running on developer machines)
Preferred Language    | Java
Alternate Language    | Python to support analytics use cases and Golang for performance for niche components
Document Store        | MongoDB for Scalable read / write data store for all end user facing use cases
Relational Store      | Postgres for OLTP data store for all transactional data and batch processing needs such as Accounting 
Java frameworks       | Quarkus + SpringBoot
Native builds         | Quarkus + Mandrel for low resource footprint and quick startup
Authentication        | Custom built 2FA (email/phone+password + mpin)
Authorization         | Standard webframework supported RBAC (Quarkus / SpringBoot)
Message Broker        | RabbitMQ
Events                | Transactional Outbox using Mongo CDC for capturing and relaying application events
Observability         | FluentBit + OpenObserve + AWS ContainerInsights (future)
Push Notifications    | Google FCM
SMS Gateway           | TextLocal
Email Gateway         | No email gateway for now. Plain simple SMTP relay.
Secrets and Keys      | AWS SSPM (to be implemented)
Blob store            | AWS S3
Job Scheduling        | Kestra (community edition)
Search                | Embedded Lucene (since we have only 1 search use case)
API Style             | Restful
Caching               | In-memory and MongoDB based caching for select use cases
Sensitive(PI/PII) data| Currently no data is considered sensitive (for example PAN), but this needs to be relooked at. 


## Mobile Application Stack

Aspect                | Technology
----------------------|------------
Language/Framework    | React Native

## Web Application Stack

Aspect                | Technology
----------------------|------------
Language/Framework    | ReactJS


## Cloud specifics

Aspect                | Technology
----------------------|------------
Network security      | Everything in private subnets + SSH Access from Bastion + Bastion whitelisting to Techwave IPs + Individual SSH crdentials
Infrastructure as Code| OpenTofu (Terraform fork)
AWS console access    | Restricted to authorized personnel




## Web Site Stack

Aspect                | Technology
----------------------|------------
Headless CMS          | Strapi
Site                  | Gatsby generated static site (because site contains only a handful of pages)
