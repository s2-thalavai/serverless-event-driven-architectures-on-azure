# Vendor and Invoice Management: Event-Driven Architecture on Azure

## ⚙️ Core Azure Components

### 1. Azure Event Grid
- Central event broker for publishing events:
  - `VendorRegistered`
  - `InvoiceSubmitted`
  - `InvoiceValidated`
  - `InvoiceApproved`
  - `InvoicePaid`
- Supports filtering, schema validation, and routing to Azure Functions, Logic Apps, and Service Bus.

### 2. Azure Service Bus
- Reliable message queue for decoupling producers and consumers.
- Use **topics** for fan-out and **DLQs** for failed invoice events.
- Ideal for validation, compliance, and payment triggers.

### 3. Azure Functions
- Stateless processors for each event type.
- Sample functions:
  - Validate invoice schema
  - Enrich vendor metadata
  - Trigger payment workflows
  - Send notifications

### 4. Azure Cosmos DB / Table Storage
- Stores:
  - Vendor profiles
  - Invoice metadata
  - Audit logs
- Features:
  - TTL for auto-expiry
  - Change feed for downstream analytics

### 5. Azure Logic Apps / Durable Functions (Optional)
- Orchestrates multi-step workflows:
  - Invoice approval chains
  - Dispute resolution
- Supports retries, conditional branching, and human-in-the-loop approvals.

---

## Sample Workflow: Invoice Lifecycle

| Event              | Producer          | Consumer                              | Action                          |
|--------------------|-------------------|----------------------------------------|----------------------------------|
| VendorRegistered   | Portal/API        | Azure Function → Cosmos DB            | Create vendor profile            |
| InvoiceSubmitted   | Vendor Portal     | Azure Function → Service Bus          | Validate invoice schema          |
| InvoiceValidated   | Validator Function| Event Grid → Compliance Function       | Trigger compliance checks        |
| InvoiceApproved    | Compliance Function| Event Grid → Payment Function         | Initiate payment                 |
| InvoicePaid        | Payment Function  | Event Grid → Notification Logic App   | Notify vendor, update status     |

---

## Observability & Auditability

- **Azure Monitor & Application Insights**: Track latency, failures, and throughput.
- **Event Grid Dead Lettering**: Capture undelivered events for replay.
- **Cosmos DB Change Feed**: Stream updates for audit logs or dashboards.
- **Diagnostic Settings**: Export logs to Log Analytics or Storage.

---

## Reference Architectures

- [Azure Event-Driven Architecture Guide](https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven)
- [Invoice Processing Pipeline on Azure (GitHub)](https://github.com/jeeeet25/Invoice_Processing_Pipeline_on_Azure)
- [SynergySparq EDA Guide](https://www.synergysparq.com/implementing-event-driven-architecture-with-azure-a-step-by-step-guide/)

