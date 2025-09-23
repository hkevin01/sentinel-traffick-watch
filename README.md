# SentinelTraffickWatch

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=flat&logo=docker&logoColor=white)](https://www.docker.com/)
[![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=flat&logo=kubernetes&logoColor=white)](https://kubernetes.io/)

**AI-Powered Human Trafficking Detection System**

*Real-time behavioral analysis through computer vision and temporal reasoning*

</div>

## 🎯 Project Purpose & Mission

### Why This Project Exists

Human trafficking is one of the most heinous crimes affecting millions of people worldwide, yet it often occurs hidden in plain sight. Traditional surveillance systems rely heavily on human operators who can't monitor multiple streams continuously or detect subtle behavioral patterns that indicate coercion, exploitation, or forced situations.

**SentinelTraffickWatch** addresses this critical gap by leveraging cutting-edge AI to:

- **Detect subtle behavioral indicators** that human observers might miss
- **Provide 24/7 monitoring** without fatigue or attention lapses
- **Analyze multiple video streams simultaneously** at scale
- **Generate actionable alerts** while maintaining privacy and dignity
- **Support law enforcement** with evidence-based detection capabilities

### Core Problem Statement

Current surveillance systems are reactive rather than proactive. By the time obvious signs of trafficking are visible, victims have already suffered. This system identifies early indicators through:

- **Behavioral pattern recognition** (coercive escorting, forced movement)
- **Temporal analysis** (prolonged control patterns, suspicious handoffs)
- **Multi-person interaction modeling** (group dynamics, power relationships)
- **Privacy-preserving detection** (indicators without identification)

## 🏗️ System Architecture

### High-Level System Overview

```mermaid
graph TB
    subgraph "Data Sources"
        A[📹 RTSP/RTMP Cameras]
        B[📁 Video Files]
        C[📱 Mobile Streams]
    end

    subgraph "Ingest Layer"
        D[🔄 Stream Processor<br/>GStreamer/OpenCV]
        E[⚡ Frame Batcher<br/>ROI Masking]
        F[📊 Metadata Extractor]
    end

    subgraph "Detection Pipeline"
        G[👤 Person Detection<br/>YOLOv11n]
        H[🦴 Pose Estimation<br/>RTMPose]
        I[🎯 Object Tracking<br/>ByteTrack]
        J[🔍 Re-ID Embedding<br/>FastReID]
    end

    subgraph "Behavioral Analysis"
        K[📈 Feature Extraction<br/>Keypoint Analysis]
        L[🤝 Interaction Graph<br/>Proximity/Contact]
        M[⚖️ Behavior Classification<br/>ST-GCN/TSM]
        N[🧠 Temporal Reasoning<br/>State Machines]
    end

    subgraph "Event Processing"
        O[📋 Rule Engine<br/>Durable Rules]
        P[📊 Risk Scoring<br/>ML Calibration]
        Q[🚨 Alert Generation<br/>Threshold Logic]
        R[🎬 Clip Generation<br/>Evidence Capture]
    end

    subgraph "Storage & API"
        S[🗄️ PostgreSQL<br/>TimescaleDB]
        T[💾 Object Storage<br/>MinIO/S3]
        U[🔍 Vector Store<br/>FAISS]
        V[🌐 REST API<br/>FastAPI]
    end

    subgraph "User Interface"
        W[💻 Web Dashboard<br/>React/Next.js]
        X[📱 Mobile App<br/>React Native]
        Y[🗺️ Map View<br/>Mapbox]
    end

    A --> D
    B --> D
    C --> D
    D --> E
    E --> F
    F --> G
    G --> H
    H --> I
    I --> J
    K --> L
    L --> M
    M --> N
    N --> O
    O --> P
    P --> Q
    Q --> R
    G --> K
    H --> K
    I --> K
    J --> K
    R --> S
    R --> T
    J --> U
    S --> V
    T --> V
    U --> V
    V --> W
    V --> X
    V --> Y

    classDef dataSource fill:#2d3748,stroke:#4a5568,stroke-width:2px,color:#ffffff
    classDef ingest fill:#1a365d,stroke:#2c5282,stroke-width:2px,color:#ffffff
    classDef detection fill:#22543d,stroke:#38a169,stroke-width:2px,color:#ffffff
    classDef behavior fill:#742a2a,stroke:#e53e3e,stroke-width:2px,color:#ffffff
    classDef event fill:#553c9a,stroke:#805ad5,stroke-width:2px,color:#ffffff
    classDef storage fill:#2d3748,stroke:#4a5568,stroke-width:2px,color:#ffffff
    classDef ui fill:#1a202c,stroke:#2d3748,stroke-width:2px,color:#ffffff

    class A,B,C dataSource
    class D,E,F ingest
    class G,H,I,J detection
    class K,L,M,N behavior
    class O,P,Q,R event
    class S,T,U,V storage
    class W,X,Y ui
```

### Microservices Architecture

```mermaid
graph TB
    subgraph "Message Queue Layer"
        MQ[🚀 Apache Kafka<br/>Event Streaming]
    end

    subgraph "Core Services"
        IS[🎥 Ingest Service<br/>Stream Processing]
        DS[🔍 Detection Service<br/>CV Models]
        IAS[🧠 Interaction Service<br/>Behavioral Analysis]
        ES[📊 Events Service<br/>API & Storage]
    end

    subgraph "Support Services"
        MS[📈 Monitoring Service<br/>Prometheus/Grafana]
        AS[🚨 Alert Service<br/>Notifications]
        CS[🎬 Clip Service<br/>Media Processing]
        US[👤 User Service<br/>Authentication]
    end

    subgraph "Data Stores"
        PG[🐘 PostgreSQL<br/>Metadata]
        TS[⏰ TimescaleDB<br/>Time Series]
        S3[💾 Object Storage<br/>Media Files]
        VS[🔍 Vector Store<br/>Embeddings]
    end

    IS --> MQ
    MQ --> DS
    MQ --> IAS
    MQ --> ES
    DS --> MQ
    IAS --> MQ
    ES --> PG
    ES --> TS
    CS --> S3
    DS --> VS
    AS --> ES
    MS --> IS
    MS --> DS
    MS --> IAS
    MS --> ES

    classDef service fill:#2d3748,stroke:#4a5568,stroke-width:2px,color:#ffffff
    classDef support fill:#1a365d,stroke:#2c5282,stroke-width:2px,color:#ffffff
    classDef data fill:#22543d,stroke:#38a169,stroke-width:2px,color:#ffffff
    classDef queue fill:#742a2a,stroke:#e53e3e,stroke-width:2px,color:#ffffff

    class IS,DS,IAS,ES service
    class MS,AS,CS,US support
    class PG,TS,S3,VS data
    class MQ queue
```

### Behavioral Detection Pipeline

```mermaid
flowchart TD
    subgraph "Input Processing"
        A[🎥 Video Frame<br/>1920x1080@30fps]
        B[👤 Person Detection<br/>YOLOv11n ONNX]
        C[🦴 Pose Estimation<br/>17 Keypoints]
    end

    subgraph "Tracking & Identity"
        D[🎯 Multi-Object Tracking<br/>ByteTrack Algorithm]
        E[🔍 Person Re-ID<br/>Feature Vectors]
        F[📊 Track History<br/>Temporal Buffer]
    end

    subgraph "Feature Extraction"
        G[📏 Geometric Features<br/>Distances, Angles]
        H[⚡ Motion Features<br/>Velocity, Acceleration]
        I[🤝 Interaction Features<br/>Proximity, Contact]
    end

    subgraph "Behavior Classification"
        J[🔴 Aggression Detection<br/>Hand/Arm Movements]
        K[👥 Escort Detection<br/>Adult-Minor Control]
        L[🔄 Handoff Detection<br/>Quick Exchanges]
        M[👁️ Loitering Detection<br/>Prolonged Observation]
    end

    subgraph "Temporal Analysis"
        N[⏱️ State Machines<br/>Event Progression]
        O[📈 Risk Scoring<br/>Weighted Features]
        P[🚨 Alert Generation<br/>Threshold Crossing]
    end

    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
    F --> G
    F --> H
    F --> I
    G --> J
    H --> J
    I --> K
    G --> L
    H --> L
    I --> L
    F --> M
    J --> N
    K --> N
    L --> N
    M --> N
    N --> O
    O --> P

    classDef input fill:#2d3748,stroke:#4a5568,stroke-width:2px,color:#ffffff
    classDef track fill:#1a365d,stroke:#2c5282,stroke-width:2px,color:#ffffff
    classDef feature fill:#22543d,stroke:#38a169,stroke-width:2px,color:#ffffff
    classDef behavior fill:#742a2a,stroke:#e53e3e,stroke-width:2px,color:#ffffff
    classDef temporal fill:#553c9a,stroke:#805ad5,stroke-width:2px,color:#ffffff

    class A,B,C input
    class D,E,F track
    class G,H,I feature
    class J,K,L,M behavior
    class N,O,P temporal
```

## 🔧 Technology Stack & Rationale

### Core Technologies Comparison

| Technology | Purpose | Why Chosen | Alternatives Considered |
|------------|---------|------------|------------------------|
| **Python 3.11+** | Primary Language | • Excellent ML/CV ecosystem<br/>• Async/await support<br/>• Rich data science libraries<br/>• Fast prototyping | C++ (performance), Rust (safety), Go (concurrency) |
| **YOLOv11n** | Person Detection | • State-of-the-art accuracy<br/>• Real-time performance<br/>• ONNX export support<br/>• Nano variant for edge | YOLOX, YOLOv8, EfficientDet, RetinaNet |
| **RTMPose** | Pose Estimation | • Lightweight architecture<br/>• High accuracy on occluded poses<br/>• Mobile-optimized variants<br/>• MMPose ecosystem | MediaPipe, OpenPose, PoseNet, AlphaPose |
| **ByteTrack** | Multi-Object Tracking | • SOTA tracking performance<br/>• Robust to occlusions<br/>• Low computational overhead<br/>• Association quality | SORT, DeepSORT, FairMOT, CenterTrack |
| **Apache Kafka** | Message Streaming | • High throughput<br/>• Fault tolerance<br/>• Horizontal scaling<br/>• Event sourcing support | NATS, RabbitMQ, Redis Streams, Pulsar |
| **PostgreSQL** | Primary Database | • ACID compliance<br/>• JSON/JSONB support<br/>• Mature ecosystem<br/>• Extension support | MySQL, MongoDB, CockroachDB |
| **TimescaleDB** | Time Series Data | • PostgreSQL extension<br/>• Time-based partitioning<br/>• Compression<br/>• SQL compatibility | InfluxDB, Prometheus, ClickHouse |
| **FastAPI** | Web Framework | • Automatic OpenAPI docs<br/>• Type hints integration<br/>• High performance<br/>• Modern async support | Flask, Django, Starlette, Tornado |
| **Docker** | Containerization | • Consistent environments<br/>• Easy deployment<br/>• Resource isolation<br/>• CI/CD integration | Podman, LXC, rkt |
| **Kubernetes** | Orchestration | • Auto-scaling<br/>• Service discovery<br/>• Rolling deployments<br/>• GPU scheduling | Docker Swarm, Nomad, ECS |

### Machine Learning Model Architecture

| Component | Model | Input | Output | Performance |
|-----------|-------|-------|--------|-------------|
| **Person Detection** | YOLOv11n | 640x640 RGB | Bounding boxes + confidence | 35+ FPS on RTX 3060 |
| **Pose Estimation** | RTMPose-Tiny | Person crops | 17 keypoints + visibility | 25+ FPS on RTX 3060 |
| **Action Recognition** | ST-GCN-Lite | Keypoint sequences | Action probabilities | 50+ FPS on RTX 3060 |
| **Person Re-ID** | FastReID-Small | Person crops | 512-dim embeddings | 100+ FPS on RTX 3060 |
| **Risk Scoring** | Logistic Regression | Feature vectors | Risk probability | 1000+ FPS CPU |

### Behavioral Detection Classes

```mermaid
mindmap
  root((Behavioral<br/>Indicators))
    Physical Aggression
      Striking motions
      Pushing gestures
      Grabbing actions
      Threatening postures
    Coercive Control
      Adult-minor proximity
      Restrictive movement
      Hand-to-arm contact
      Velocity mismatch
    Group Dynamics
      Surrounding formation
      Coordinated movement
      Power positioning
      Escape blocking
    Suspicious Exchanges
      Brief encounters
      Object transfers
      Rapid divergence
      Directional changes
    Predatory Behavior
      Prolonged observation
      Targeted approach
      Following patterns
      Isolation attempts
```

### Privacy & Ethics Framework

| Principle | Implementation | Technology | Compliance |
|-----------|----------------|------------|-------------|
| **Face Privacy** | Automatic face blurring | OpenCV + MTCNN detection | GDPR Article 9 |
| **Minor Protection** | Age estimation + enhanced blur | Age classification model | COPPA compliance |
| **Data Minimization** | Configurable retention periods | TimescaleDB lifecycle policies | GDPR Article 5 |
| **Consent Management** | Opt-in data collection | User service + consent logs | GDPR Article 7 |
| **Audit Trails** | Comprehensive action logging | Structured logs + immutable storage | SOX compliance |
| **Differential Privacy** | Statistical noise injection | DP-SGD algorithms | Academic standards |

## 🚀 Key Features

### 🎯 Real-Time Detection Capabilities

- **Multi-Stream Processing**: Handle 10+ concurrent 1080p streams
- **Sub-Second Latency**: <600ms end-to-end processing time
- **Behavioral Pattern Recognition**: 6 primary trafficking indicator classes
- **Temporal Context**: 6-second sliding window analysis
- **Privacy-First**: Automatic face blurring and consent management

### 🧠 Advanced AI Pipeline

- **Computer Vision**: YOLOv11n person detection with 95%+ accuracy
- **Pose Analysis**: 17-point skeleton tracking for behavior understanding
- **Action Recognition**: Spatio-temporal graph networks for activity classification
- **Person Re-ID**: Cross-camera identity tracking with 512-dim embeddings
- **Risk Calibration**: ML-based scoring with precision-recall optimization

### 🔒 Security & Compliance

- **GDPR Compliant**: Built-in privacy controls and data rights management
- **Audit Logging**: Comprehensive action trails for legal compliance
- **Secure Storage**: Encrypted data at rest and in transit
- **Role-Based Access**: Granular permissions for different user types
- **Evidence Chain**: Immutable event logging for legal proceedings

### 📊 Monitoring & Analytics

- **Real-Time Dashboards**: Live system health and detection metrics
- **Performance Analytics**: Model accuracy and system throughput tracking
- **Alert Management**: Configurable thresholds and notification routing
- **False Positive Reduction**: Human feedback loops for continuous improvement

## 🏃 Quick Start

### Prerequisites

- Docker 20.10+ and Docker Compose
- NVIDIA GPU with CUDA 11.8+ (for optimal performance)
- 16GB+ RAM recommended
- Network access to RTSP/RTMP streams

### 1. Clone and Setup

```bash
git clone https://github.com/your-org/sentinel-traffick-watch.git
cd sentinel-traffick-watch
cp CONFIG.example.yaml CONFIG.yaml
```

### 2. Configure Streams

Edit `CONFIG.yaml` to add your camera streams:

```yaml
streams:
  - id: cam_entrance
    url: rtsp://username:password@192.168.1.100:554/stream
    roi: [[0.1, 0.1], [0.9, 0.1], [0.9, 0.9], [0.1, 0.9]]
  - id: cam_lobby
    url: rtsp://username:password@192.168.1.101:554/stream
    roi: [[0.0, 0.0], [1.0, 0.0], [1.0, 1.0], [0.0, 1.0]]
```

### 3. Start Services

```bash
# Development environment
cd deployments
docker-compose -f docker-compose.dev.yml up --build

# Production environment
docker-compose -f docker-compose.prod.yml up -d
```

### 4. Access Dashboard

- **Web UI**: <http://localhost:3000>
- **API Docs**: <http://localhost:8080/docs>
- **Monitoring**: <http://localhost:3001> (Grafana)

## 📚 Documentation

- [**Project Plan**](docs/project-plan.md) - Development phases and milestones
- [**API Reference**](docs/api-reference.md) - Complete REST API documentation
- [**Deployment Guide**](docs/deployment.md) - Production deployment instructions
- [**Model Training**](docs/model-training.md) - Custom model training procedures
- [**Security Guidelines**](SECURITY.md) - Security best practices and reporting
- [**Ethics Framework**](ETHICS.md) - Ethical AI and privacy considerations

## 🧪 Development

### Running Tests

```bash
# Unit tests
python -m pytest tests/unit/ -v

# Integration tests
python -m pytest tests/integration/ -v

# End-to-end tests
python -m pytest tests/e2e/ -v
```

### Model Training

```bash
# Train action recognition model
python scripts/training/train_action_model.py --config configs/training.yaml

# Calibrate detection thresholds
python scripts/calibration/calibrate_thresholds.py --eval-data data/eval/labeled_events.jsonl
```

### Performance Profiling

```bash
# Profile inference pipeline
python scripts/profiling/profile_inference.py --stream rtsp://test-stream

# GPU utilization analysis
python scripts/profiling/gpu_analysis.py --duration 300
```

## 🔧 Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `APP_CONFIG` | Path to main configuration file | `CONFIG.yaml` |
| `LOG_LEVEL` | Logging verbosity | `INFO` |
| `KAFKA_BOOTSTRAP` | Kafka broker addresses | `kafka:9092` |
| `DATABASE_URL` | PostgreSQL connection string | `postgresql://postgres:postgres@postgres:5432/postgres` |
| `REDIS_URL` | Redis connection string | `redis://redis:6379` |
| `S3_ENDPOINT` | Object storage endpoint | `http://minio:9000` |

### Detection Thresholds

Configure behavioral detection sensitivity:

```yaml
thresholds:
  aggression: 0.72      # Physical aggression indicators
  escort: 0.65          # Coercive escorting behavior
  handoff: 0.70         # Suspicious person exchanges
  loiter: 0.60          # Predatory loitering patterns
  group_control: 0.68   # Group surrounding dynamics
  forced_movement: 0.75 # Non-voluntary movement patterns
```

## 📈 Performance Benchmarks

### Hardware Requirements

| Deployment | GPU | RAM | Streams | Latency |
|------------|-----|-----|---------|---------|
| **Edge** | RTX 3060 | 16GB | 4x1080p | <800ms |
| **Server** | RTX 4090 | 32GB | 16x1080p | <600ms |
| **Cluster** | 4x A100 | 128GB | 64x1080p | <400ms |

### Model Performance

| Model | mAP@0.5 | Precision | Recall | FPS |
|-------|---------|-----------|--------|-----|
| Person Detection | 0.94 | 0.91 | 0.96 | 35 |
| Pose Estimation | 0.88 | 0.85 | 0.91 | 25 |
| Action Recognition | 0.76 | 0.82 | 0.71 | 50 |
| Behavioral Detection | 0.68 | 0.85 | 0.58 | - |

## 🛡️ Security Considerations

### Data Protection

- All video data encrypted at rest using AES-256
- TLS 1.3 for all network communications
- Regular security audits and penetration testing
- Compliance with GDPR, CCPA, and local privacy laws

### Access Control

- Multi-factor authentication required
- Role-based permissions with principle of least privilege
- API rate limiting and request validation
- Comprehensive audit logging for all actions

### Privacy Safeguards

- Automatic face blurring for all detected persons
- Enhanced privacy protection for minors
- Configurable data retention policies
- User consent management system

## 🤝 Contributing

We welcome contributions from the community! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details on:

- Code of conduct and community standards
- Development workflow and branch policies
- Testing requirements and coverage expectations
- Documentation standards and review process

### Development Setup

```bash
# Clone repository
git clone https://github.com/your-org/sentinel-traffick-watch.git
cd sentinel-traffick-watch

# Install development dependencies
pip install -r requirements-dev.txt

# Install pre-commit hooks
pre-commit install

# Run development environment
docker-compose -f deployments/docker-compose.dev.yml up
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support & Community

- **Documentation**: [docs.sentineltraffickwatch.org](https://docs.sentineltraffickwatch.org)
- **Issues**: [GitHub Issues](https://github.com/your-org/sentinel-traffick-watch/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-org/sentinel-traffick-watch/discussions)
- **Security Reports**: <security@sentineltraffickwatch.org>

## 🙏 Acknowledgments

- **Research Community**: Built on open-source computer vision research
- **Anti-Trafficking Organizations**: Guidance on behavioral indicators and ethical considerations
- **Privacy Advocates**: Input on privacy-preserving AI techniques
- **Law Enforcement**: Feedback on practical deployment requirements

---

<div align="center">

**Together, we can leverage technology to protect the vulnerable and fight human trafficking.**

*This project is developed with the highest ethical standards and commitment to privacy, human rights, and social responsibility.*

</div>
