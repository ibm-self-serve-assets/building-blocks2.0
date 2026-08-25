# Context Hub

**Context Hub** is a solution building block for combining **real-time events**, **enterprise data**, and **business metadata/governance** into a reusable context layer for applications, analytics and AI agents.

!!! important "Not a standalone product"
    Context Hub is an architectural pattern. The primary products are **IBM Confluent**, **IBM watsonx.data**, and **IBM watsonx.data intelligence**.

## Why it matters

AI and analytics often fail to deliver useful outcomes when they see only one side of the enterprise: historical data without current events, or live events without business meaning and governance. A Context Hub closes that gap by bringing together **data in motion** and **data at rest**, then enriching it with metadata, lineage, terms, classifications and policy context.

IBM describes the combined IBM Confluent + watsonx.data value as unifying real-time event streams with structured and unstructured enterprise data, adding metadata, lineage and policy-driven context, and delivering governed data products to applications, analytics and AI agents.

## Business value

- **Current context for AI:** agents and applications can react to continuously changing operational state.
- **Trusted reuse:** business meaning, lineage and governance make the same data safer to reuse across teams.
- **Less point-to-point integration:** a streaming backbone plus open lakehouse reduces custom copies and brittle hand-offs.
- **Faster time to decision:** real-time events can become queryable and consumable without waiting for nightly batch windows.
- **Better explainability:** metadata and lineage help users understand where the context came from and how it changed.

## When to use

Use Context Hub when:

- AI agents need **real-time operational facts** plus historical or reference context.
- Streaming events need to be enriched with governed enterprise data before downstream use.
- Multiple teams need a reusable source of context instead of building separate integrations.
- You want streaming data to become available for SQL analytics in open table formats.
- Governance and metadata need to apply consistently across data used by analytics and AI.

Avoid using Context Hub as a synonym for a simple data lake or message bus. The value comes from the **combination of real-time flow + persistent/open data + governed business context**.

## Reference architecture

```mermaid
flowchart LR
    S["Systems of record<br/>Apps<br/>IoT<br/>SaaS"] --> K["IBM Confluent<br/>Kafka + Connectors"]
    K --> F["Apache Flink<br/>filter / join / enrich"]
    F --> T["Kafka topics / Tableflow / Iceberg sink"]
    T --> W["IBM watsonx.data<br/>open hybrid data foundation"]
    W --> D["watsonx.data intelligence<br/>metadata / lineage / terms / policy"]
    K --> A["Real-time applications"]
    W --> A
    D --> A
    A --> X["AI agents / Analytics / Automation"]
```

## Core product roles

### IBM Confluent

Use for the real-time backbone: Kafka-based event streaming, managed connectors, Apache Flink stream processing, Schema Registry and Stream Governance.

### IBM watsonx.data

Use as the open hybrid data foundation for structured and unstructured data, multi-engine processing, open table formats and AI-ready data access.

### IBM watsonx.data intelligence

Use to add business terms, generated names and descriptions, classifications, relationships, lineage, quality and governance context that make technical data easier to discover and use safely.

## Integration pattern: streaming to open lakehouse

IBM documents an integration in which the Confluent Apache Iceberg Sink Connector writes Kafka topic data into Apache Iceberg tables for near-real-time analytics in watsonx.data. Confluent Tableflow is another managed approach for materializing topics as Iceberg or Delta tables. This is especially useful when the same real-time data must support SQL analytics and AI context.

## What to demonstrate

1. A source application publishes an event to IBM Confluent.
2. Flink enriches or correlates the event with another stream.
3. Stream Governance shows schemas/lineage and enforces compatibility.
4. The event stream is materialized or written into an Iceberg table in watsonx.data.
5. watsonx.data intelligence enriches the table/columns with business metadata.
6. An analyst or AI agent consumes the same contextualized information.

## Official references

- [IBM Confluent](https://www.ibm.com/products/confluent)
- [IBM watsonx.data](https://www.ibm.com/products/watsonx-data)
- [IBM watsonx.data intelligence - metadata enrichment](https://www.ibm.com/docs/en/watsonx/wdi/2.4.x?topic=data-enriching-your-assets)
- [Confluent Apache Iceberg Sink Connector with watsonx.data](https://www.ibm.com/docs/en/watsonxdata/saas?topic=integrations-integrating-confluent-apache-iceberg-sink-connector)
