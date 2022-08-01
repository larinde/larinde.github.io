---
layout: post
author: Olarinde Ajai
---

# Tactical/Strategic Workflow Engine Approach

## Motivation for a workflow engine

1. Transparent overview of processes that span multiple services
2. Transparent view of participating microservices in workflow orchestration
3. Transparent insight into improving and changing processes.
4. Reduced effort in state management of long running processes.

## Technology Choice

1. Activiti
2. Camunda
3. jBPM

## Main features required

1. BPMN (Business Process Model Notation)
   - workflow definition
   - SME/Dev collaboration
2. DMN (Decision Model and Notation)
   - To capture existing and new business rules with decision tables
   - Substitute for Excel
   - Human and machine readable contract


## Tactical/Strategic Approach

1. Dedicated workflow engine per domain/bounded context
   - Example: "price creation" and "price maintenance" workflow belong in the pricing domain
2. Dedicated Dev Team for each workflow engine
3. Service calls to workflow microservice will be via domain-centric API (Swagger/OpenAPI) implementation. Direct workflow engine calls will be via the engine-specific Java API.
   - to reduce number of HTTP calls required to complete a workflow task
   - to prevent abstraction leak of engine specific context
   - to future-proof API from changes in underlying workflow engine preference.

| Domain-centric API Call         | Engine-specific REST call            |
|:-------------------------------:|:------------------------------------:|
| POST /api/pricing/creation      |  POST /api/runtime/process-instances |

## Orchestration vs Choreography

1. Orchestration
   - for command flows that require a process manager
2. Choreography
   - For event-based flows

## Architecture Overview

![Component Architecture](./images/prj_daimler_platform_component_architecture.png)

![Price Creation Process](./images/prj_daimler_price_creation_flow_seq.png)

![Data Historisation](./images/prj_daimler_data_historisation_flow.png)
