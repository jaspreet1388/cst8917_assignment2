# CST8917 – Serverless Applications  
## Assignment 2 – Serverless Service Alternatives Report
## Submitted By : Jaspreet Singh
> **Objective**: Compare Azure serverless services with AWS and GCP equivalents in terms of features, triggers/bindings, integration options, monitoring, pricing, and architectural trade-offs.

---

## Quick Reference – Azure -- AWS --  GCP

| Azure Service | AWS Equivalent | GCP Equivalent |
|---|---|---|
| Azure Functions | AWS Lambda | Cloud Functions |
| Durable Functions | Step Functions | Workflows |
| Azure Logic Apps | AWS Step Functions (Express) / EventBridge Pipes / AppFlow | Workflows / Cloud Composer (for orchestration) |
| Azure Service Bus | Amazon SQS (Queues) + SNS (Topics) | Pub/Sub |
| Azure Event Grid | Amazon EventBridge | Eventarc |
| Azure Event Hubs | Amazon Kinesis Data Streams | Pub/Sub Lite |

---

## 1. Azure Functions

**Overview**  
Event-driven compute service that runs code on demand without managing infrastructure. Supports many triggers/bindings to integrate with other Azure services.

**Core Features**  
- Triggers: HTTP, Timer, Blob Storage, Queue Storage, Event Hub, Service Bus, Cosmos DB, Event Grid  
- Bindings: Input/output bindings for storage, messaging, and databases  
- Multiple languages: C#, Java, Python, JavaScript, PowerShell  
- Consumption and Premium plans

**Integration Options**  
- Integrates with Azure DevOps and GitHub Actions for CI/CD  
- Works with Event Grid, Event Hubs, Service Bus, Cosmos DB, Key Vault  
- Can run locally with Azure Functions Core Tools

**Monitoring & Observability**  
- Azure Application Insights integration for metrics, traces, and logs  
- Built-in metrics in Azure Monitor  
- Log streaming in portal

**Pricing Model**  
- Consumption plan: Pay per execution, GB-seconds, and outbound data  
- Premium plan: Reserved instances + execution costs

**Strengths & Weaknesses**  
- Flexible triggers/bindings  
- Multiple hosting plans  
- Cold start latency in Consumption plan  
- Vendor lock-in on bindings

**Comparison Table**

| Feature | Azure Functions | AWS Lambda | GCP Cloud Functions |
|---|---|---|---|
| Language Support | Many incl. Python, C#, Node.js | Similar set, plus Go, Ruby | Node.js, Python, Go, Java, .NET, PHP |
| Triggers | Broad Azure service support | Broad AWS service support | GCP event sources + HTTP |
| Pricing | Per execution/GB-sec | Per execution/GB-sec | Per execution/GB-sec |
| Cold Start | Present in Consumption plan | Present | Present |

---

## 2. Durable Functions

**Overview**  
Extension of Azure Functions for stateful orchestration with patterns like chaining, fan-out/fan-in, and human interaction.

**Core Features**  
- Orchestration Functions (define workflows)  
- Activity Functions (perform work)  
- Entity Functions (manage state)  
- Patterns: Function chaining, fan-out/fan-in, async HTTP APIs, human interaction

**Integration Options**  
- Works seamlessly with Azure Functions triggers/bindings  
- Integrated with Azure Storage for state management  
- Deploy via ARM/Bicep, Terraform, or CI/CD pipelines

**Monitoring & Observability**  
- Application Insights telemetry for orchestration state and function executions  
- Durable Task Framework history stored in Azure Storage

**Pricing Model**  
- Same as Azure Functions + storage costs

**Strengths & Weaknesses**  
- Built-in state management  
- Familiar function model  
- Azure-specific; no direct portability  
- State stored in Azure Storage only

**Comparison Table**

| Feature | Durable Functions | AWS Step Functions | GCP Workflows |
|---|---|---|---|
| State Mgmt | Azure Storage | JSON-based state | YAML/JSON |
| Patterns | Chaining, fan-out/fan-in | Same + parallel, map state | Same + error handling |
| Pricing | Per execution + storage | Per state transition | Per execution step |

---

## 3. Azure Logic Apps

**Overview**  
Low-code/no-code integration and workflow automation platform.

**Core Features**  
- Designer-based workflows  
- 400+ connectors (Office 365, Dynamics, SAP, Salesforce, SQL, Service Bus, etc.)  
- Triggers: HTTP, Timer, Event Grid, Service Bus, Blob Storage, etc.  
- Actions: Call APIs, manipulate data, send messages

**Integration Options**  
- Deep integration with Azure Functions, Service Bus, Event Grid  
- Can be invoked via HTTP from other apps  
- CI/CD via ARM templates and Azure DevOps

**Monitoring & Observability**  
- Run history in portal  
- Azure Monitor integration  
- Alerts on failed runs

**Pricing Model**  
- Consumption (per action/trigger)  
- Standard (per workflow run capacity)

**Strengths & Weaknesses**  
- Fast integration with SaaS/enterprise apps  
- Visual designer reduces dev time  
- Less control than code-first approach  
- Complex logic can be harder to maintain visually

**Comparison Table**

| Feature | Logic Apps | AWS Step Functions / EventBridge Pipes | GCP Workflows |
|---|---|---|---|
| Model | Visual, low-code | JSON/YAML | YAML/JSON |
| Connectors | 400+ | Fewer native, more custom | Limited |
| Pricing | Per action | Per transition/event | Per step |

---

## 4. Azure Service Bus

**Overview**  
Enterprise messaging service supporting queues (point-to-point) and topics (publish/subscribe).

**Core Features**  
- Queues, topics, subscriptions  
- FIFO and message sessions  
- Dead-letter queues  
- Scheduled messages

**Integration Options**  
- Works with Functions, Logic Apps, Event Grid  
- Supports AMQP 1.0 standard

**Monitoring & Observability**  
- Metrics in Azure Monitor  
- Dead-letter queue inspection  
- Service Bus Explorer

**Pricing Model**  
- Basic, Standard, Premium tiers (per operation, message size, brokered connection)

**Strengths & Weaknesses**  
- Rich enterprise features (sessions, transactions)  
- Reliable delivery  
- More complex than basic queues  
- Premium tier cost

**Comparison Table**

| Feature | Service Bus | AWS SQS + SNS | GCP Pub/Sub |
|---|---|---|---|
| Model | Queues & Topics | SQS (queues), SNS (topics) | Topics/subscriptions |
| Ordering | Sessions | FIFO queues | Ordering keys |
| Pricing | Per op/message | Per request | Per message |

---

## 5. Azure Event Grid

**Overview**  
Event routing service for building reactive applications.

**Core Features**  
- Event sources: Blob Storage, Resource Groups, IoT Hub, etc.  
- Event handlers: Functions, Logic Apps, WebHooks  
- Advanced filtering, retries, and dead-letter destinations

**Integration Options**  
- Works with most Azure services and custom topics  
- Integrates with Kubernetes Event Grid on AKS

**Monitoring & Observability**  
- Metrics in Azure Monitor  
- Dead-letter destinations for undeliverable events

**Pricing Model**  
- Per million operations

**Strengths & Weaknesses**  
- Low latency, high scalability  
- Native integration across Azure  
- Limited outside Azure unless using WebHooks  
- Charges per event

**Comparison Table**

| Feature | Event Grid | AWS EventBridge | GCP Eventarc |
|---|---|---|---|
| Delivery | Push | Push | Push |
| Filters | Advanced | Advanced | Basic/Advanced |
| Pricing | Per op | Per op | Per op |

---

## 6. Azure Event Hubs

**Overview**  
Big data streaming platform for telemetry ingestion.

**Core Features**  
- Partitioned consumer model  
- Integrations: Functions, Stream Analytics, Databricks, Kafka endpoint  
- High-throughput event ingestion

**Integration Options**  
- Direct integration with Azure Functions (Event Hub trigger)  
- Azure Data Explorer, Synapse, Databricks

**Monitoring & Observability**  
- Metrics in Azure Monitor  
- Capture to Blob or Data Lake for auditing

**Pricing Model**  
- Per throughput unit/hour + egress  
- Dedicated clusters for high scale

**Strengths & Weaknesses**  
- High throughput  
- Kafka compatibility  
- Requires planning partitions and throughput  
- Pricing complexity

**Comparison Table**

| Feature | Event Hubs | AWS Kinesis | GCP Pub/Sub Lite |
|---|---|---|---|
| Model | Partitions | Shards | Lite regions |
| Retention | Configurable | Configurable | Configurable |
| Pricing | TU/hour | Shard-hour | Capacity-hour |

---
