# SentinelTraffickWatch - Copilot Instructions

This project is an AI-powered human trafficking detection system that uses computer vision, pose estimation, and behavioral analysis to identify potential trafficking indicators in real-time video streams. 

## Project Context
- **Domain**: Human trafficking detection and prevention
- **Technology Stack**: Python, Docker, Computer Vision (YOLOv11n, RTMPose), Message Queues (Kafka), Databases (PostgreSQL, TimescaleDB)
- **Architecture**: Microservices with event-driven processing
- **Primary Goal**: Real-time detection of behavioral indicators like aggression, coercion, escorting, and suspicious handoffs

## Code Standards
- Use Python 3.11+ with type hints
- Follow PEP 8 naming conventions
- Include comprehensive error handling with proper logging
- Implement graceful degradation and recovery mechanisms
- Add detailed docstrings for all functions and classes
- Use async/await patterns for I/O operations
- Implement proper resource cleanup and memory management

## Key Behavioral Detection Classes
1. **Physical aggression**: striking, pushing, grabbing
2. **Coercive escorting**: adult tightly controlling minor's movement  
3. **Group escorting**: multiple adults surrounding and steering individual
4. **Handoffs/exchanges**: short meetings with immediate divergence
5. **Loitering + targeting**: prolonged observation followed by approach
6. **Rapid forced movement**: being pulled vs. walking voluntarily

## Privacy and Ethics Guidelines
- Default blur faces and minors unless authorized
- Use "indicators, not conclusions" language
- Implement configurable retention windows
- Maintain strict audit logs
- Support differential privacy for analytics
- Ensure explainable AI decisions

## Performance Requirements
- Single RTX 3060: 25-35 FPS per 1080p stream
- End-to-end latency: < 600ms average
- False alert rate: < 2 per hour after calibration
- Graceful handling of concurrent streams (up to 10 persons)

## Architecture Components
- **Ingest**: RTSP/RTMP stream processing
- **Detection**: YOLOv11n person detection + pose estimation
- **Interaction**: Temporal reasoning and rule engines
- **Events**: API, storage, and alerting
- **Storage**: PostgreSQL + TimescaleDB, S3-compatible object store

## Development Patterns
- Use Pydantic for data validation
- Implement proper async patterns with aiokafka
- Use ONNX/TensorRT for model inference
- Include comprehensive unit and integration tests
- Follow container-first development approach
- Implement proper logging and monitoring
