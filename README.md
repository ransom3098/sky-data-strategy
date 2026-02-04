# 📡 Sky UK Data Management Strategy & Cloud Architecture

> **A comprehensive data strategy analysis and technology integration proposal for Sky UK's real-time analytics, personalisation, and cloud-native transformation**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Cloud: GCP](https://img.shields.io/badge/Cloud-Google%20Cloud-4285F4?logo=google-cloud)](https://cloud.google.com/)
[![Data: BigQuery](https://img.shields.io/badge/Data-BigQuery-669DF6?logo=google-cloud)](https://cloud.google.com/bigquery)
[![Streaming: Kafka](https://img.shields.io/badge/Streaming-Apache%20Kafka-231F20?logo=apache-kafka)](https://kafka.apache.org/)

---

<div align="center">

## 🌐 [**VIEW LIVE INTERACTIVE DASHBOARD →**](https://ransom3098.github.io/sky-data-strategy/)

[![Live Demo](https://img.shields.io/badge/🚀_Live_Demo-Click_Here-brightgreen?style=for-the-badge)](https://ransom3098.github.io/sky-data-strategy/)

</div>

---

## 🎯 Project Overview

This project presents a **data management strategy and technology modernisation proposal** for **Sky UK**, Europe's largest pay-TV broadcaster by revenue. The analysis addresses critical challenges in real-time analytics, cross-platform data integration, and AI-driven personalisation across Sky's streaming ecosystem (Sky Q, Sky Glass, Sky Go, NOW TV).

### Business Context

Sky processes **over 1 billion daily events** from millions of devices, requiring robust data infrastructure to support:
- **AdSmart**: Addressable TV advertising with real-time audience targeting
- **Content Personalisation**: AI-powered recommendations across platforms
- **Customer Analytics**: Churn prediction, engagement tracking, and behavioural insights
- **Operational Intelligence**: Real-time diagnostics and service monitoring

---

## 🏗️ Current Architecture Analysis

### Existing Technology Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Cloud Platform** | Google Cloud Platform (GCP) | Core infrastructure |
| **Data Warehouse** | BigQuery | Analytics engine for petabyte-scale data |
| **Stream Ingestion** | Cloud Pub/Sub + Dataflow | Real-time telemetry processing |
| **Data Mesh** | Starburst | Federated data access across domains |
| **Marketing Tech** | Adobe Experience Cloud | Customer data platform |
| **Container Orchestration** | AWS EKS | Video encoding workloads |

### Architecture Diagram: Current State

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           SKY DATA ECOSYSTEM                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │
│  │   Sky Q      │  │   Sky Go     │  │    NOW TV    │  │  Sky Glass   │    │
│  │   Devices    │  │    App       │  │   Platform   │  │   Devices    │    │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘    │
│         │                 │                 │                 │            │
│         └─────────────────┴────────┬────────┴─────────────────┘            │
│                                    │                                       │
│                                    ▼                                       │
│                     ┌──────────────────────────┐                           │
│                     │    Cloud Pub/Sub         │                           │
│                     │  (Event Ingestion)       │                           │
│                     └────────────┬─────────────┘                           │
│                                  │                                         │
│                                  ▼                                         │
│                     ┌──────────────────────────┐                           │
│                     │      Dataflow            │                           │
│                     │  (Stream Processing)     │                           │
│                     └────────────┬─────────────┘                           │
│                                  │                                         │
│              ┌───────────────────┼───────────────────┐                     │
│              ▼                   ▼                   ▼                     │
│  ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐           │
│  │    BigQuery      │ │    Starburst     │ │  Adobe Experience │           │
│  │  (Data Warehouse)│ │   (Data Mesh)    │ │      Cloud        │           │
│  └──────────────────┘ └──────────────────┘ └──────────────────┘           │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

### Identified Challenges

| Challenge | Impact | Business Risk |
|-----------|--------|---------------|
| **Real-time Latency** | Batch processing delays insights by hours | Missed personalisation opportunities |
| **Data Silos** | Fragmented customer view across platforms | Inconsistent user experience |
| **ML Integration** | Disconnected AI/ML workflows | Slow model deployment |
| **Governance Gaps** | Complex GDPR compliance tracking | Regulatory exposure |

---

## 💡 Proposed Solution

### Recommended Technology Stack

The proposal integrates three key technologies to address identified gaps:

#### 1. Apache Kafka (Managed Service)
**Purpose**: High-throughput, low-latency event streaming

```
Key Capabilities:
├── Exactly-once semantics for data integrity
├── Strict event ordering for behavioural tracking
├── Fault-tolerant distributed architecture
└── Native GCP integration via Confluent Cloud
```

#### 2. BigQuery (Enhanced)
**Purpose**: Unified analytics and AI platform

```
Key Capabilities:
├── Serverless petabyte-scale analytics
├── BigQuery ML for in-warehouse model training
├── Vertex AI integration for advanced workflows
└── Real-time streaming ingestion
```

#### 3. Looker
**Purpose**: Governed business intelligence and semantic layer

```
Key Capabilities:
├── Centralised metric definitions
├── Self-service analytics for business users
├── Embedded analytics capabilities
└── Natural language query interface
```

### Proposed Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     PROPOSED DATA ARCHITECTURE                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                    DATA SOURCES                                      │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │   │
│  │  │ Sky Q    │ │ Sky Go   │ │ NOW TV   │ │ AdSmart  │ │ Search   │  │   │
│  │  │ Telemetry│ │ Events   │ │ Streams  │ │ Clicks   │ │ Behaviour│  │   │
│  │  └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘  │   │
│  └───────┼────────────┼────────────┼────────────┼────────────┼────────┘   │
│          └────────────┴────────────┼────────────┴────────────┘            │
│                                    ▼                                       │
│                    ┌───────────────────────────────┐                       │
│                    │      APACHE KAFKA             │                       │
│                    │   ┌─────────────────────┐     │                       │
│                    │   │ • Real-time streams │     │                       │
│                    │   │ • Event ordering    │     │                       │
│                    │   │ • 1B+ events/day    │     │                       │
│                    │   └─────────────────────┘     │                       │
│                    └──────────────┬────────────────┘                       │
│                                   │                                        │
│          ┌────────────────────────┼────────────────────────┐               │
│          ▼                        ▼                        ▼               │
│  ┌───────────────┐    ┌───────────────────┐    ┌───────────────────┐      │
│  │   BIGQUERY    │    │   BIGQUERY ML     │    │    VERTEX AI      │      │
│  │  ┌─────────┐  │    │  ┌─────────────┐  │    │  ┌─────────────┐  │      │
│  │  │Analytics│  │    │  │Churn Models │  │    │  │Recommender  │  │      │
│  │  │Warehouse│  │    │  │Segmentation │  │    │  │Embeddings   │  │      │
│  │  │(PB-scale│  │    │  │Predictions  │  │    │  │GenAI        │  │      │
│  │  └─────────┘  │    │  └─────────────┘  │    │  └─────────────┘  │      │
│  └───────┬───────┘    └─────────┬─────────┘    └─────────┬─────────┘      │
│          └──────────────────────┼──────────────────────────┘               │
│                                 ▼                                          │
│                    ┌───────────────────────────────┐                       │
│                    │          LOOKER               │                       │
│                    │   ┌─────────────────────┐     │                       │
│                    │   │ • Semantic Layer    │     │                       │
│                    │   │ • Self-Service BI   │     │                       │
│                    │   │ • Embedded Analytics│     │                       │
│                    │   └─────────────────────┘     │                       │
│                    └──────────────┬────────────────┘                       │
│                                   │                                        │
│          ┌────────────────────────┼────────────────────────┐               │
│          ▼                        ▼                        ▼               │
│  ┌───────────────┐    ┌───────────────────┐    ┌───────────────────┐      │
│  │  MARKETING    │    │    EDITORIAL      │    │    EXECUTIVE      │      │
│  │  Campaign     │    │    Content        │    │    Strategic      │      │
│  │  Dashboards   │    │    Performance    │    │    KPIs           │      │
│  └───────────────┘    └───────────────────┘    └───────────────────┘      │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## 📊 Business Use Cases

### 1. Real-Time AdSmart Targeting

```python
# Conceptual data flow for addressable advertising
Pipeline:
    User_Interaction (Sky Q) 
    → Kafka Stream (< 100ms latency)
    → BigQuery (audience segmentation)
    → Looker (campaign dashboard)
    → AdSmart (personalised ad delivery)

Impact: Dynamic audience segments updated in real-time vs. daily batch
```

### 2. Personalised Content Recommendations

```python
# ML-powered recommendation system
Pipeline:
    Viewing_History + Search_Behaviour
    → BigQuery ML (collaborative filtering)
    → Vertex AI (embedding generation)
    → Content_Ranking (similarity search)
    → Platform_Delivery (Sky Q, NOW, Sky Go)

Impact: 15-20% improvement in content discovery engagement
```

### 3. Cross-Functional Analytics

```python
# Self-service BI for business teams
Pipeline:
    Raw_Data (BigQuery)
    → Semantic_Layer (Looker metrics)
    → Natural_Language_Query
    → Interactive_Dashboard
    → Export_to_Presentation

Impact: Reduce data request backlog by 60%
```

---

## 📈 Comparative Analysis

### Current vs. Proposed Capabilities

| Capability | Current State | Proposed State | Improvement |
|------------|---------------|----------------|-------------|
| **Real-time Processing** | Limited (batch-heavy) | Enhanced (Kafka streaming) | Sub-second latency |
| **ML/AI Integration** | Fragmented tools | Unified (BigQuery ML + Vertex AI) | 3x faster model deployment |
| **Business Intelligence** | Custom Sky Analytics | Governed Looker semantic layer | Consistent metrics |
| **Cross-team Collaboration** | Moderate | Strong (notebooks + dashboards) | Self-service enabled |
| **Data Governance** | Manual processes | Automated audit trails | GDPR-compliant by design |

---

## 🎓 Theoretical Frameworks Applied

### DIKW Hierarchy (Rowley, 2007)

The solution transforms raw telemetry into strategic decisions:

```
                    ┌─────────────┐
                    │   WISDOM    │  Strategic decisions on content
                    │             │  and advertising investments
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  KNOWLEDGE  │  Understanding of customer
                    │             │  preferences and behaviour patterns
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ INFORMATION │  Processed insights from
                    │             │  BigQuery analytics and Looker
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │    DATA     │  Raw events from STBs,
                    │             │  apps, and user interactions
                    └─────────────┘
```

### DAMA-DMBOK Framework Alignment

| DAMA Knowledge Area | Implementation |
|---------------------|----------------|
| **Data Architecture** | Centralised warehouse + streaming integration |
| **Data Governance** | Access control and audit trails in Looker |
| **Data Quality** | Pipeline validation from Kafka to BigQuery |
| **Data Integration** | Semantic metrics and unified data products |

---

## ⚠️ Risk Assessment & Mitigation

| Risk Category | Description | Mitigation Strategy |
|---------------|-------------|---------------------|
| **Integration Complexity** | Legacy system compatibility | Phased rollout starting with NOW TV pilot |
| **Cost Management** | Cloud spending optimisation | Serverless architecture + usage monitoring |
| **Staff Upskilling** | Technical capability gaps | Training programmes for Looker and BigQuery ML |
| **GDPR Compliance** | Privacy and consent management | Automated data governance with audit trails |
| **Change Management** | Organisational resistance | Stakeholder engagement and quick wins |

---

## 🚀 Implementation Roadmap

### Phase 1: Foundation (Months 1-3)
- [ ] Deploy managed Kafka for NOW TV streaming data
- [ ] Establish BigQuery ML development environment
- [ ] Configure Looker semantic layer for core metrics

### Phase 2: Integration (Months 4-6)
- [ ] Migrate Sky Q telemetry to Kafka pipelines
- [ ] Deploy churn prediction models via BigQuery ML
- [ ] Enable self-service BI for marketing teams

### Phase 3: Optimisation (Months 7-12)
- [ ] Extend to AdSmart real-time targeting
- [ ] Implement Vertex AI recommendation system
- [ ] Full GDPR audit trail automation

---

## 📁 Repository Structure

```
sky-data-strategy/
│
├── 📄 README.md                    # This file
├── 📄 STRATEGY_REPORT.md           # Full strategic analysis
│
├── 📂 architecture/
│   ├── current-state.png           # Current architecture diagram
│   ├── proposed-state.png          # Proposed architecture diagram
│   └── data-flow.mermaid           # Data pipeline flows
│
├── 📂 analysis/
│   ├── technology-comparison.md    # Detailed tech evaluation
│   ├── stakeholder-impact.md       # Managerial assessment
│   └── risk-assessment.md          # Risk mitigation strategies
│
├── 📂 frameworks/
│   ├── dikw-application.md         # DIKW hierarchy analysis
│   └── dama-dmbok-alignment.md     # DAMA framework mapping
│
└── 📂 assets/
    ├── diagrams/                   # Architecture diagrams
    └── presentations/              # Executive summaries
```

---

## 📚 Key References

| Source | Description |
|--------|-------------|
| [Google Cloud - Sky UK Case Study](https://cloud.google.com/customers/sky-uk) | Official cloud migration story |
| [Starburst - Sky Case Study](https://www.starburst.io/resources/sky-case-study/) | Data mesh implementation |
| [Datatonic - Sky Analytics Platform](https://datatonic.com/case-studies/creating-a-powerful-streaming-analytics-platform-for-sky/) | Streaming analytics details |
| [DAMA-DMBOK 2nd Edition](https://www.dama.org/cpages/body-of-knowledge) | Data management framework |

---

## 🛠️ Technologies & Tools

![Google Cloud](https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![BigQuery](https://img.shields.io/badge/BigQuery-669DF6?style=for-the-badge&logo=google-cloud&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=for-the-badge&logo=apache-kafka&logoColor=white)
![Looker](https://img.shields.io/badge/Looker-4285F4?style=for-the-badge&logo=looker&logoColor=white)
![Vertex AI](https://img.shields.io/badge/Vertex_AI-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)

---

## 👤 Author

**Ransom Robins Fernando**

- 🎓 MSc Business Analytics | University of Birmingham
- 💼 Business Analyst | Infosys (Novartis Account)
- 🔗 [LinkedIn](https://www.linkedin.com/in/ransom-robinsfernando)
- 📧 [Email](mailto:ransomrobinsfernando@gmail.com)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <i>This analysis was completed as part of the MSc Business Analytics programme at the University of Birmingham, focusing on Data Management Strategies and Technologies.</i>
</p>
