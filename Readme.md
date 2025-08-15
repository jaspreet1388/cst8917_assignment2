# CST8917 – Serverless Applications  
## Assignment 2 – Serverless Service Alternatives Report

> **Objective**: Compare Azure serverless services with AWS and GCP equivalents in terms of features, triggers/bindings, integration options, monitoring, pricing, and architectural trade-offs.  
> This report covers the **six core services required** by the assignment and **additional Azure serverless offerings** to show the broader ecosystem.

---

## 🔎 Quick Reference – Azure → AWS → GCP

| Azure Service | AWS Equivalent | GCP Equivalent |
|---|---|---|
| Azure Functions | AWS Lambda | Cloud Functions |
| Durable Functions | Step Functions | Workflows |
| Azure Logic Apps | AWS Step Functions (Express) / EventBridge Pipes / AppFlow | Workflows / Cloud Composer |
| Azure Service Bus | Amazon SQS (Queues) + SNS (Topics) | Pub/Sub |
| Azure Event Grid | Amazon EventBridge | Eventarc |
| Azure Event Hubs | Amazon Kinesis Data Streams | Pub/Sub Lite |
| Azure Container Apps | AWS App Runner / Fargate | Cloud Run |
| Azure API Management (Consumption) | Amazon API Gateway | API Gateway (GCP) |
| Azure SignalR Service | API Gateway WebSocket + AppSync | WebSocket via API Gateway / Firebase Realtime Database |
| Azure Cognitive Services | AWS AI Services (Rekognition, Polly, Comprehend, etc.) | Vertex AI APIs |
| Azure Form Recognizer | Textract | Document AI |
| Azure Batch | AWS Batch | Batch in GCP |
| Azure Stream Analytics | Kinesis Data Analytics | Dataflow (Streaming) |
| Azure SQL Database Serverless | Aurora Serverless | Cloud SQL Serverless |
| Azure Blob Storage Event Triggers | S3 Event Notifications | Cloud Storage Event Notifications |
| Azure Web PubSub | AppSync / API Gateway WebSocket | Firebase Realtime DB / Web PubSub on GCP Marketplace |

---

## 💰 Consolidated Pricing Overview

| Azure Service | Azure Pricing Model | AWS Pricing Model | GCP Pricing Model |
|---|---|---|---|
| Azure Functions | Per execution/GB-sec | Per execution/GB-sec | Per execution/GB-sec |
| Durable Functions | Functions cost + storage | Per state transition | Per workflow step |
| Azure Logic Apps | Per action/trigger | Per transition/event | Per workflow step |
| Azure Service Bus | Per op/message | Per request | Per message |
| Azure Event Grid | Per million ops | Per million events | Per million events |
| Azure Event Hubs | TU/hour + egress | Shard-hour + data | Capacity-hour |
| Azure Container Apps | vCPU/sec + memory/sec | vCPU/sec + memory/sec | vCPU/sec + memory/sec |
| Azure API Management (Consumption) | Per call | Per million API calls | Per million API calls |
| Azure SignalR Service | Per million messages | Per million messages | Per million messages |
| Azure Cognitive Services | Per API call | Per API call | Per API call |
| Azure Form Recognizer | Per page | Per page | Per page |
| Azure Batch | Per vCPU-hour | Per vCPU-hour | Per vCPU-hour |
| Azure Stream Analytics | SU/hour | Kinesis Analytics PU/hour | Dataflow vCPU/memory/time |
| Azure SQL Database Serverless | vCore/sec + storage | ACU/sec + storage | vCPU/sec + storage |
| Azure Blob Storage Event Triggers | Per operation | Per request | Per request |
| Azure Web PubSub | Per million messages | Per million messages | Per million messages |

---

# **Core Assignment Services**

## 1. Azure Functions

**Overview**  
Event-driven compute that runs code without provisioning servers.

**Core Features**  
- Triggers: HTTP, Timer, Blob, Queue, Event Hub, Service Bus, Cosmos DB, Event Grid  
- Bindings: Input/output for Azure services  
- Languages: C#, Java, Python, Node.js, PowerShell  

**Integration Options**  
- Azure DevOps/GitHub Actions  
- Works with Service Bus, Event Grid, Event Hubs

**Monitoring & Observability**  
- Application Insights  
- Azure Monitor metrics/logs

**Pricing Model**  
- Per execution, GB-seconds, outbound data

**Strengths & Weaknesses**  
✅ Wide triggers/bindings  
❌ Cold starts in Consumption plan

**Comparison Table**

| Feature | Azure Functions | AWS Lambda | GCP Cloud Functions |
|---|---|---|---|
| Languages | C#, Java, Python, Node.js | + Go, Ruby | Node.js, Python, Go, Java |
| Triggers | Broad Azure sources | Broad AWS sources | GCP events + HTTP |
| Pricing | Per execution/GB-sec | Per execution/GB-sec | Per execution/GB-sec |

---

## 2. Durable Functions

**Overview**  
Stateful orchestrations on Azure Functions.

**Core Features**  
- Orchestrator, Activity, Entity Functions  
- Patterns: Chaining, fan-out/fan-in, async APIs

**Integration Options**  
- Azure Storage for state  
- Works with all Azure Function triggers

**Monitoring & Observability**  
- Application Insights  
- Durable Task Framework history

**Pricing Model**  
- Functions cost + storage

**Strengths & Weaknesses**  
✅ Simplifies stateful workflows  
❌ Azure-only storage backend

**Comparison Table**

| Feature | Durable Functions | Step Functions | Workflows |
|---|---|---|---|
| State | Azure Storage | JSON-based state | YAML/JSON |
| Pricing | Per exec + storage | Per transition | Per step |

---

## 3. Azure Logic Apps

**Overview**  
Low-code workflow automation.

**Core Features**  
- 400+ connectors  
- Triggers: HTTP, Event Grid, Service Bus  
- Actions: API calls, data transforms

**Integration Options**  
- Functions, Service Bus, Event Grid  
- CI/CD with ARM, Azure DevOps

**Monitoring & Observability**  
- Run history  
- Azure Monitor alerts

**Pricing Model**  
- Consumption: per action/trigger  
- Standard: per run capacity

**Strengths & Weaknesses**  
✅ Quick SaaS integration  
❌ Less flexible than code

**Comparison Table**

| Feature | Logic Apps | Step Functions / EventBridge | Workflows |
|---|---|---|---|
| Model | Visual | JSON/YAML | YAML/JSON |
| Connectors | 400+ | Fewer native | Limited |
| Pricing | Per action | Per event/transition | Per step |

---

## 4. Azure Service Bus

**Overview**  
Enterprise-grade messaging with queues and topics.

**Core Features**  
- FIFO, sessions, DLQs  
- AMQP 1.0

**Integration Options**  
- Functions, Logic Apps

**Monitoring & Observability**  
- Azure Monitor metrics  
- DLQ inspection

**Pricing Model**  
- Per op/message

**Strengths & Weaknesses**  
✅ Rich features  
❌ More complex than basic queues

**Comparison Table**

| Feature | Service Bus | SQS + SNS | Pub/Sub |
|---|---|---|---|
| Model | Queues, Topics | Queues, Topics | Topics/subs |
| Ordering | Sessions | FIFO queues | Ordering keys |
| Pricing | Per op | Per request | Per message |

---

## 5. Azure Event Grid

**Overview**  
Event routing for reactive apps.

**Core Features**  
- Sources: Blob, Resource Group, IoT Hub  
- Handlers: Functions, Logic Apps, WebHooks

**Integration Options**  
- Native Azure services, custom topics

**Monitoring & Observability**  
- Metrics, dead-letter queues

**Pricing Model**  
- Per million ops

**Strengths & Weaknesses**  
✅ Low latency  
❌ Limited non-Azure triggers

**Comparison Table**

| Feature | Event Grid | EventBridge | Eventarc |
|---|---|---|---|
| Delivery | Push | Push | Push |
| Filters | Advanced | Advanced | Basic/Advanced |
| Pricing | Per op | Per op | Per op |

---

## 6. Azure Event Hubs

**Overview**  
High-throughput data streaming.

**Core Features**  
- Partitions, consumer groups  
- Kafka endpoint

**Integration Options**  
- Functions, Databricks, Synapse

**Monitoring & Observability**  
- Metrics in Monitor  
- Capture to Blob/Data Lake

**Pricing Model**  
- TU/hour + egress

**Strengths & Weaknesses**  
✅ Scalable ingestion  
❌ Partition planning needed

**Comparison Table**

| Feature | Event Hubs | Kinesis | Pub/Sub Lite |
|---|---|---|---|
| Model | Partitions | Shards | Lite regions |
| Pricing | TU/hour | Shard-hour | Capacity-hour |

---

# **Additional Azure Serverless Services**

*(These extend the serverless ecosystem and show multi-cloud equivalents)*

## Azure Container Apps  
- AWS: App Runner / Fargate  
- GCP: Cloud Run  
- Run containerized apps serverlessly with event triggers.

## Azure API Management (Consumption)  
- AWS: API Gateway  
- GCP: API Gateway  
- Manage, secure, and expose APIs pay-per-call.

## Azure SignalR Service  
- AWS: API Gateway WebSockets / AppSync  
- GCP: Firebase Realtime DB  
- Real-time push messaging serverlessly.

## Azure Cognitive Services  
- AWS: AI Services  
- GCP: Vertex AI APIs  
- Prebuilt AI APIs, billed per call.

## Azure Form Recognizer  
- AWS: Textract  
- GCP: Document AI  
- OCR and form parsing serverlessly.

## Azure Batch  
- AWS: Batch  
- GCP: Batch  
- Large-scale job scheduling.

## Azure Stream Analytics  
- AWS: Kinesis Data Analytics  
- GCP: Dataflow  
- Real-time data processing.

## Azure SQL Database Serverless  
- AWS: Aurora Serverless  
- GCP: Cloud SQL Serverless  
- Pausable, auto-scaling database.

## Azure Blob Storage Event Triggers  
- AWS: S3 Events  
- GCP: Cloud Storage Events  
- Event-based serverless triggers.

## Azure Web PubSub  
- AWS: AppSync / API Gateway WebSockets  
- GCP: Firebase Realtime DB  
- PubSub for web real-time messaging.

---
