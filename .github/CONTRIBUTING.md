# Contributing to SentinelTraffickWatch

Thank you for your interest in contributing to SentinelTraffickWatch! This project aims to help detect potential human trafficking indicators using AI and computer vision.

## Code of Conduct

This project is committed to creating a safe and inclusive environment. All contributors are expected to adhere to ethical guidelines and respect privacy considerations.

## Getting Started

1. Fork the repository
2. Clone your fork: `git clone https://github.com/your-username/sentinel-traffick-watch.git`
3. Create a virtual environment: `python -m venv venv && source venv/bin/activate`
4. Install dependencies: `pip install -r requirements-dev.txt`
5. Set up pre-commit hooks: `pre-commit install`

## Development Workflow

### Branch Naming
- `feature/description` - New features
- `bugfix/description` - Bug fixes
- `docs/description` - Documentation updates
- `perf/description` - Performance improvements

### Commit Messages
Follow conventional commit format:
- `feat: add new detection algorithm`
- `fix: resolve memory leak in tracker`
- `docs: update API documentation`
- `test: add unit tests for pose estimation`

### Code Standards

#### Python
- Use Python 3.11+
- Follow PEP 8 style guidelines
- Use type hints for all functions
- Add comprehensive docstrings
- Maximum line length: 100 characters
- Use `black` for formatting
- Use `pylint` for linting

#### Error Handling
- Always include proper exception handling
- Log errors with appropriate levels
- Implement graceful degradation
- Add retry logic for network operations
- Use structured logging with context

#### Performance
- Profile code for memory usage
- Implement proper resource cleanup
- Use async/await for I/O operations
- Monitor GPU memory utilization
- Implement caching where appropriate

#### Privacy and Ethics
- Never log personally identifiable information
- Implement face blurring by default
- Use "indicators, not conclusions" language
- Maintain audit trails
- Consider differential privacy for analytics

### Testing

#### Unit Tests
- Write tests for all new functions
- Aim for >80% code coverage
- Use pytest fixtures for common setup
- Mock external dependencies
- Test edge cases and error conditions

#### Integration Tests
- Test service interactions
- Verify message queue processing
- Test database operations
- Validate Docker container behavior

#### Performance Tests
- Benchmark inference speed
- Test memory usage under load
- Validate GPU utilization
- Test concurrent stream processing

### Documentation

- Update README.md for user-facing changes
- Add docstrings for all public functions
- Update API documentation
- Include configuration examples
- Document performance characteristics

## Ethical Guidelines

### Data Handling
- Never use real surveillance footage in commits
- Use synthetic or anonymized test data only
- Respect all privacy laws and regulations
- Implement data retention policies

### Model Bias
- Test models across diverse demographics
- Document potential biases and limitations
- Implement fairness metrics
- Consider social impact of features

### Responsible Disclosure
- Report security vulnerabilities privately
- Consider ethical implications of new features
- Engage with domain experts and stakeholders
- Document decision rationale

## Review Process

1. Create a pull request with descriptive title
2. Fill out the PR template completely
3. Ensure all CI checks pass
4. Request review from maintainers
5. Address feedback promptly
6. Maintain clean commit history

## Performance Requirements

- Maintain 25-35 FPS on RTX 3060
- Keep end-to-end latency < 600ms
- Target < 2 false alerts per hour
- Support up to 10 concurrent person tracks

## Getting Help

- Check existing issues and documentation
- Join discussions in project issues
- Contact maintainers for sensitive topics
- Refer to the project's ethical guidelines

## Recognition

Contributors will be recognized in:
- CONTRIBUTORS.md file
- Release notes for significant contributions
- Project documentation for major features

Thank you for contributing to this important project!
