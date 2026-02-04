# Sky UK Data Management Strategy Report

## Strategic Technology Integration for Real-Time Analytics & Personalisation

**Version:** 1.0  
**Author:** Ransom Robins Fernando  
**Date:** May 2025

---

## Executive Summary

Sky UK, the largest pay-TV broadcaster in Europe, operates a complex digital ecosystem serving millions of customers across Sky Q, Sky Glass, Sky Go, and NOW TV platforms. In an industry where personalisation, speed, and multi-platform consistency are critical for customer retention, data management plays a strategic role.

This report critically examines Sky's existing data infrastructure—encompassing Google Cloud's BigQuery, Adobe Experience Cloud, and a Starburst-powered data mesh—and proposes an enhanced technology stack to address gaps in real-time personalisation, system integration, and data latency.

**Key Recommendation:** Implement an integrated stack of **Apache Kafka**, **BigQuery ML**, and **Looker** to enable real-time streaming, scalable machine learning, and collaborative data workflows.

### Strategic Impact

| Objective | Current Gap | Proposed Solution | Expected Outcome |
|-----------|-------------|-------------------|------------------|
| Real-time targeting | Batch delays (hours) | Kafka streaming | Sub-second latency |
| Personalisation | Fragmented ML tools | BigQuery ML + Vertex AI | Unified AI platform |
| Business intelligence | Inconsistent metrics | Looker semantic layer | Trusted analytics |
| Operational efficiency | High DevOps overhead | Serverless architecture | 40% cost reduction |

---

## 1. Company & Data Environment Analysis

### 1.1 Business Context

Sky operates one of the most complex media data ecosystems in Europe:

- **Scale**: 1+ billion daily events from millions of devices
- **Platforms**: Sky Q, Sky Glass, Sky Go, NOW TV
- **Services**: Live TV, on-demand streaming, broadband, advertising (AdSmart)
- **Markets**: UK, Ireland, Germany, Italy, Austria

### 1.2 Current Technology Landscape

#### Google Cloud Platform Migration

Sky has migrated from legacy on-premises Hadoop clusters to a cloud-native architecture on GCP. The core components include:

| Technology | Function | Scale |
|------------|----------|-------|
| Cloud Pub/Sub | Event ingestion | 1B+ events/day |
| Dataflow | Stream processing | Auto-scaling |
| BigQuery | Analytics warehouse | Petabyte-scale |
| Cloud Storage | Data lake | Multi-region |

#### Data Mesh via Starburst

To overcome data silos across business units, Sky implemented a federated data mesh architecture using Starburst:

- **Domain ownership**: Business units manage their own datasets
- **Unified query interface**: Cross-domain analytics without data duplication
- **Governed access**: Centralised permission management

#### Marketing Technology Stack

- **Adobe Experience Cloud**: Customer data platform for personalisation
- **Sky Analytics**: Self-serve advertising planning portal
- **AdSmart**: Addressable TV advertising platform
- **Sky AdVance**: Cross-platform retargeting

### 1.3 Identified Challenges

| Challenge | Technical Impact | Business Impact |
|-----------|------------------|-----------------|
| **Real-time latency** | Overnight batch loads | Delayed campaign optimisation |
| **Integration complexity** | Siloed systems | Inconsistent customer view |
| **ML fragmentation** | Disconnected workflows | Slow model deployment |
| **Governance gaps** | Manual compliance | GDPR exposure risk |

---

## 2. Proposed Technology Stack

### 2.1 Architecture Overview

The proposed solution enhances Sky's existing GCP foundation with three integrated technologies:

```
┌─────────────────────────────────────────────────────────────────┐
│                    PROPOSED ARCHITECTURE                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│    DATA SOURCES          PROCESSING           ANALYTICS         │
│    ───────────           ──────────           ─────────         │
│                                                                 │
│    ┌─────────┐          ┌──────────┐        ┌──────────┐       │
│    │ Sky Q   │──────────│          │        │          │       │
│    │ Devices │          │  APACHE  │        │ BIGQUERY │       │
│    ├─────────┤          │  KAFKA   │───────▶│    ML    │       │
│    │ Sky Go  │──────────│          │        │          │       │
│    │ App     │          │ (Stream  │        │ (Models) │       │
│    ├─────────┤          │ Ingest)  │        │          │       │
│    │ NOW TV  │──────────│          │        └────┬─────┘       │
│    │ Platform│          └────┬─────┘             │             │
│    ├─────────┤               │                   │             │
│    │ AdSmart │───────────────┤                   │             │
│    │ Events  │               │                   ▼             │
│    └─────────┘               │            ┌──────────┐         │
│                              │            │          │         │
│                              └───────────▶│  LOOKER  │         │
│                                           │   (BI)   │         │
│                                           │          │         │
│                                           └────┬─────┘         │
│                                                │               │
│                         ┌──────────────────────┼───────────┐   │
│                         ▼                      ▼           ▼   │
│                    ┌─────────┐          ┌─────────┐  ┌───────┐ │
│                    │Marketing│          │Editorial│  │Execs  │ │
│                    │ Teams   │          │ Teams   │  │       │ │
│                    └─────────┘          └─────────┘  └───────┘ │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 2.2 Technology Components

#### Apache Kafka (Managed Service)

**Purpose**: Replace/augment Cloud Pub/Sub for high-throughput streaming

| Capability | Benefit for Sky |
|------------|-----------------|
| Exactly-once semantics | Data integrity for billing/analytics |
| Strict event ordering | Accurate user journey tracking |
| Fault tolerance | Zero data loss during failures |
| GCP integration | Seamless with existing infrastructure |

**Use Case**: Real-time ingestion of 1B+ daily events with <100ms latency

#### BigQuery ML + Vertex AI

**Purpose**: Unified analytics and AI platform

| Capability | Benefit for Sky |
|------------|-----------------|
| In-warehouse ML | SQL-based model training |
| Vertex AI integration | Advanced model deployment |
| Vector embeddings | Recommendation systems |
| Generative AI | Content summarisation |

**Use Case**: Churn prediction, content recommendations, audience segmentation

#### Looker

**Purpose**: Governed business intelligence with semantic layer

| Capability | Benefit for Sky |
|------------|-----------------|
| Semantic modelling | Consistent metric definitions |
| Self-service BI | Reduced analyst backlog |
| Embedded analytics | Customer-facing dashboards |
| Natural language | Non-technical user access |

**Use Case**: Campaign performance dashboards, content analytics, executive KPIs

---

## 3. Business Use Case Alignment

### 3.1 Real-Time AdSmart Targeting

**Current State**: Daily batch audience segments
**Proposed State**: Real-time dynamic segmentation

```
Flow: User watches content on Sky Q
      → Kafka captures viewing event (<100ms)
      → BigQuery updates audience segment
      → AdSmart delivers personalised ad
      → Looker tracks campaign performance
```

**Business Impact**: Improved ad relevance, higher CPMs, better advertiser retention

### 3.2 Personalised Content Recommendations

**Current State**: Fragmented recommendation systems
**Proposed State**: Unified ML-powered personalisation

```
Flow: User browses content library
      → BigQuery ML generates embeddings
      → Vertex AI performs similarity search
      → Platform delivers ranked recommendations
      → Feedback loop refines model
```

**Business Impact**: Increased content discovery, reduced churn, higher engagement

### 3.3 Cross-Functional Analytics

**Current State**: Technical bottleneck for data access
**Proposed State**: Self-service governed analytics

```
Flow: Marketing needs campaign insights
      → Looker provides governed dashboard
      → Natural language query available
      → Consistent metrics across teams
      → Export to presentations
```

**Business Impact**: 60% reduction in data request backlog, faster decisions

---

## 4. Technical & Managerial Evaluation

### 4.1 Technical Benefits

| Benefit | Description | Measurement |
|---------|-------------|-------------|
| **Real-time processing** | Sub-second event ingestion | <100ms latency |
| **Scalable ML** | In-warehouse model training | 3x faster deployment |
| **Unified platform** | Single analytics environment | Reduced complexity |
| **Automated governance** | Built-in access controls | GDPR-compliant |

### 4.2 Managerial Impact

| Stakeholder | Impact |
|-------------|--------|
| **Marketing** | Faster insights, campaign optimisation capability |
| **Engineering** | Streamlined data ops, reduced DevOps overhead |
| **Executives** | Strategic alignment, data-driven decisions |
| **Customers** | Better personalisation, improved experience |

### 4.3 Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Integration complexity | Medium | High | Phased rollout, pilot with NOW TV |
| Cost overruns | Medium | Medium | Serverless architecture, usage monitoring |
| Staff capability gaps | High | Medium | Training programme, gradual adoption |
| GDPR non-compliance | Low | High | Automated audit trails, consent management |

---

## 5. Strategic Alignment

### 5.1 DIKW Framework Application

The proposed stack transforms raw data into strategic wisdom:

| Level | Sky Implementation |
|-------|-------------------|
| **Data** | Raw events from STBs, apps, user interactions |
| **Information** | Processed analytics in BigQuery and Looker dashboards |
| **Knowledge** | Understanding of customer preferences and patterns |
| **Wisdom** | Strategic decisions on content and advertising investments |

### 5.2 DAMA-DMBOK Alignment

| DAMA Knowledge Area | Implementation |
|---------------------|----------------|
| Data Architecture | Centralised warehouse + streaming integration |
| Data Governance | Access control and audit in Looker |
| Data Quality | Pipeline validation Kafka → BigQuery |
| Data Integration | Semantic metrics, unified data products |

---

## 6. Implementation Roadmap

### Phase 1: Foundation (Months 1-3)

| Activity | Owner | Deliverable |
|----------|-------|-------------|
| Deploy managed Kafka | Platform Team | NOW TV streaming pipeline |
| Configure BigQuery ML | Data Science | Development environment |
| Set up Looker | BI Team | Core metric definitions |

### Phase 2: Integration (Months 4-6)

| Activity | Owner | Deliverable |
|----------|-------|-------------|
| Migrate Sky Q telemetry | Platform Team | Kafka integration |
| Deploy churn model | Data Science | Production ML pipeline |
| Enable self-service BI | BI Team | Marketing dashboards |

### Phase 3: Optimisation (Months 7-12)

| Activity | Owner | Deliverable |
|----------|-------|-------------|
| AdSmart real-time targeting | AdTech Team | Live personalisation |
| Vertex AI recommendations | Data Science | Content recommendation engine |
| GDPR automation | Compliance | Full audit trail system |

---

## 7. Recommendations

Based on the analysis, Sky should:

1. **Implement phased Kafka integration** starting with NOW TV data as a pilot
2. **Build self-service BI capabilities** through Looker training for business teams
3. **Expand BigQuery ML use cases** for audience segmentation and churn modelling
4. **Formalise GDPR controls** with explainability and audit trails throughout the stack
5. **Adopt data product thinking** with domain teams treating pipelines as products

---

## 8. Conclusion

The proposed technology stack positions Sky to deliver personalised, fast, and data-driven services at scale. By enhancing its existing Google Cloud foundation with Apache Kafka, BigQuery ML, and Looker, Sky can:

- Achieve sub-second real-time analytics
- Unify fragmented ML workflows
- Empower business teams with self-service BI
- Ensure GDPR compliance through automated governance

This proposal aligns Sky's data infrastructure with its strategic focus on real-time analytics, personalisation, and cloud-native transformation, keeping data at the heart of its digital strategy.

---

## References

- Google Cloud. (2025). *Sky UK Case Study*. https://cloud.google.com/customers/sky-uk
- Starburst. (2025). *Sky Case Study*. https://www.starburst.io/resources/sky-case-study/
- Datatonic. (2025). *Creating a Powerful Streaming Analytics Platform for Sky*. https://datatonic.com/case-studies/
- Henderson, D. (2024). *DAMA-DMBOK: Data Management Body of Knowledge* (2nd Edition).
- Rowley, J. (2007). The wisdom hierarchy: representations of the DIKW hierarchy. *Journal of Information Science*, 33(2), 163-180.
- Confluent. (2023). *What is Apache Kafka?* https://www.confluent.io/what-is-apache-kafka/
