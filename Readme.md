# CST8917 – Serverless Applications  
## Assignment 2 – Serverless Service Alternatives Report
## Submitted By: Jaspreet Singh

> **Objective**: Compare Azure serverless services with AWS and GCP equivalents in terms of features, triggers/bindings, integration options, monitoring, pricing, and architectural trade-offs.  
> This report covers the **six core services required** by the assignment and **additional Azure serverless offerings** to show the broader ecosystem.

---

## Quick Reference – Azure → AWS → GCP

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

## Consolidated Pricing Overview

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



---

## 7. Azure Container Apps

**Overview**  
Runs containerized applications serverlessly with automatic scaling, event-driven execution, and no Kubernetes management.

**Core Features**  
- Deploy containers directly from registries  
- Scale to zero on idle  
- Supports HTTP, gRPC, Dapr sidecars  
- Event triggers from Service Bus, Event Grid, Blob Storage

**Integration Options**  
- Azure Container Registry, GitHub Actions, Azure DevOps  
- Works with Service Bus, Event Grid, Logic Apps

**Monitoring & Observability**  
- Azure Monitor metrics/logs  
- Container logs in Log Analytics

**Pricing Model**  
- Pay per vCPU-second and GiB-second

**Strengths & Weaknesses**  
✅ Flexible runtimes via containers  
✅ Event-driven scaling  
❌ More expensive for constant workloads  
❌ Cold starts on scale-to-zero

**Comparison Table**

| Feature | Azure Container Apps | AWS App Runner / Fargate | GCP Cloud Run |
|---|---|---|---|
| Runtime | Any container | Any container | Any container |
| Scaling | To zero | To zero | To zero |
| Pricing | vCPU/mem-sec | vCPU/mem-sec | vCPU/mem-sec |

---

## 8. Azure API Management (Consumption Tier)

**Overview**  
API gateway in a serverless consumption tier with per-call billing.

**Core Features**  
- Secure, publish, and monitor APIs  
- Rate limiting, quotas, authentication  
- Transformations and caching

**Integration Options**  
- Functions, Logic Apps, Container Apps  
- CI/CD with ARM/Bicep, DevOps, GitHub Actions

**Monitoring & Observability**  
- Azure Monitor, API analytics dashboard

**Pricing Model**  
- Pay per API call

**Strengths & Weaknesses**  
✅ Global API gateway  
✅ Built-in security and analytics  
❌ Per-call cost can grow for high-volume APIs

**Comparison Table**

| Feature | Azure API Mgmt (Consumption) | AWS API Gateway | GCP API Gateway |
|---|---|---|---|
| Billing | Per call | Per million calls | Per million calls |
| Auth | OAuth2, JWT | OAuth2, JWT | OAuth2, JWT |
| Transforms | Yes | Yes | Limited |

---

## 9. Azure SignalR Service (Serverless Tier)

**Overview**  
Managed real-time messaging service for WebSockets and push updates.

**Core Features**  
- Publish/subscribe messaging  
- Serverless tier integrates with Functions  
- Multiple protocols: WebSockets, Server-Sent Events

**Integration Options**  
- Functions triggers/bindings  
- Web apps, mobile apps

**Monitoring & Observability**  
- Azure Monitor metrics for connections, messages

**Pricing Model**  
- Per million messages

**Strengths & Weaknesses**  
✅ Scales real-time messaging easily  
❌ Not suitable for heavy compute

**Comparison Table**

| Feature | Azure SignalR | AWS API Gateway WebSocket / AppSync | GCP Firebase Realtime DB |
|---|---|---|---|
| Protocol | WebSockets, SSE | WebSockets, GraphQL | WebSockets |
| Billing | Per message | Per message | Per GB transfer |
| Integration | Functions | Lambda | Cloud Functions |

---

## 10. Azure Cognitive Services

**Overview**  
Pre-built AI APIs for vision, speech, language, and decision-making.

**Core Features**  
- Computer Vision, Text Analytics, Speech-to-Text, Translation  
- REST API-based  
- No model training needed

**Integration Options**  
- Functions, Logic Apps, Web Apps  
- CI/CD with API keys in Key Vault

**Monitoring & Observability**  
- Azure Monitor for API metrics

**Pricing Model**  
- Per API call

**Strengths & Weaknesses**  
✅ Fast AI integration  
❌ Cost scales with usage

**Comparison Table**

| Feature | Azure Cognitive Services | AWS AI Services | GCP Vertex AI APIs |
|---|---|---|---|
| Model Mgmt | Fully managed | Fully managed | Fully managed |
| Billing | Per call | Per call | Per call |
| Custom Models | Limited | Limited | Limited |

---

## 11. Azure Form Recognizer

**Overview**  
AI-powered OCR and form data extraction.

**Core Features**  
- Prebuilt models for invoices, receipts  
- Custom form training  
- PDF/image support

**Integration Options**  
- Functions for event-driven OCR  
- Blob triggers for document ingestion

**Monitoring & Observability**  
- Azure Monitor metrics

**Pricing Model**  
- Per page processed

**Strengths & Weaknesses**  
✅ High accuracy  
❌ Pricing for large volumes

**Comparison Table**

| Feature | Azure Form Recognizer | AWS Textract | GCP Document AI |
|---|---|---|---|
| Input | PDF, images | PDF, images | PDF, images |
| Billing | Per page | Per page | Per page |
| Training | Yes | No | Yes |

---

## 12. Azure Batch

**Overview**  
Serverless job scheduling for large-scale compute tasks.

**Core Features**  
- Parallel task execution  
- Auto-scaling compute pools  
- Supports Docker containers

**Integration Options**  
- Blob storage for input/output  
- Functions or Logic Apps to trigger jobs

**Monitoring & Observability**  
- Azure Monitor job metrics  
- Logging via Storage

**Pricing Model**  
- Per vCPU-hour

**Strengths & Weaknesses**  
✅ Handles large jobs easily  
❌ Longer startup time

**Comparison Table**

| Feature | Azure Batch | AWS Batch | GCP Batch |
|---|---|---|---|
| Compute | VM/Container | VM/Container | VM/Container |
| Scaling | Auto | Auto | Auto |
| Pricing | vCPU-hour | vCPU-hour | vCPU-hour |

---

## 13. Azure Stream Analytics

**Overview**  
Serverless stream processing engine.

**Core Features**  
- SQL-like queries over event streams  
- Input from Event Hubs, IoT Hub, Blob  
- Output to Power BI, Blob, SQL DB

**Integration Options**  
- Event-driven pipelines with Event Hubs, Functions

**Monitoring & Observability**  
- Job metrics in Azure Monitor

**Pricing Model**  
- Streaming Unit (SU) per hour

**Strengths & Weaknesses**  
✅ Simple streaming queries  
❌ Limited compared to Apache Flink

**Comparison Table**

| Feature | Azure Stream Analytics | AWS Kinesis Analytics | GCP Dataflow |
|---|---|---|---|
| Language | SQL | SQL | Java, Python, SQL |
| Billing | SU/hour | PU/hour | vCPU/mem/hr |
| Integrations | Azure native | AWS native | GCP native |

---

## 14. Azure SQL Database (Serverless Tier)

**Overview**  
Auto-pausing SQL database with per-second billing.

**Core Features**  
- Auto-scale compute  
- Pause when idle  
- Built-in backups

**Integration Options**  
- Works with Functions, Logic Apps  
- CI/CD with ARM templates

**Monitoring & Observability**  
- Query performance insights  
- Azure Monitor metrics

**Pricing Model**  
- vCore-second + storage

**Strengths & Weaknesses**  
✅ Cost savings for intermittent workloads  
❌ Cold start on resume

**Comparison Table**

| Feature | Azure SQL Serverless | AWS Aurora Serverless | GCP Cloud SQL Serverless |
|---|---|---|---|
| Scaling | Auto | Auto | Auto |
| Billing | vCore-sec | ACU-sec | vCPU-sec |
| Pause | Yes | Yes | Yes |

---

## 15. Azure Blob Storage Event Triggers

**Overview**  
Event-driven triggers for blob changes via Event Grid.

**Core Features**  
- Create, update, delete events  
- Native Event Grid integration

**Integration Options**  
- Functions, Logic Apps, Event Hubs

**Monitoring & Observability**  
- Azure Monitor events

**Pricing Model**  
- Per operation

**Strengths & Weaknesses**  
✅ Simple file-based workflows  
❌ Requires Event Grid for push

**Comparison Table**

| Feature | Blob Event Triggers | S3 Event Notifications | GCP Storage Event Notifications |
|---|---|---|---|
| Trigger | Create/update/delete | Same | Same |
| Billing | Per op | Per op | Per op |
| Push | Event Grid | SQS/Lambda | Pub/Sub |

---

## 16. Azure Web PubSub

**Overview**  
Real-time publish/subscribe for web and mobile clients.

**Core Features**  
- WebSocket-based pub/sub  
- Serverless tier with Functions integration  
- Scales automatically

**Integration Options**  
- Functions, Logic Apps  
- Supports cloud-to-client messaging

**Monitoring & Observability**  
- Connection/message metrics

**Pricing Model**  
- Per million messages

**Strengths & Weaknesses**  
✅ Easy real-time apps  
❌ Latency in some regions

**Comparison Table**

| Feature | Azure Web PubSub | AWS AppSync / API Gateway WebSocket | GCP Firebase Realtime DB |
|---|---|---|---|
| Protocol | WebSocket | WebSocket, GraphQL | WebSocket |
| Billing | Per message | Per message | Per GB transfer |
| Integration | Functions | Lambda | Cloud Functions |
---

In conclusion, the comparative study of Azure, AWS, and GCP serverless offerings highlights that all three cloud providers deliver highly capable solutions for building scalable, event-driven applications without the operational overhead of managing infrastructure. Azure stands out for its seamless integration with the broader Microsoft ecosystem, making it ideal for enterprises already leveraging Azure services. AWS provides the most mature and diverse set of event-driven and messaging services, while GCP excels in developer-friendly tooling and data analytics integration. By understanding these equivalencies, organizations can design resilient, portable, and cost-efficient serverless architectures, enabling flexibility to adopt single- or multi-cloud strategies that align with performance, integration, and compliance needs.
