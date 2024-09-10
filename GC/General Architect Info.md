# DevOps

**SDLC: Software development life cycle**
Three elements of great software teams -> *Business* | *Development* | *Operations*
- Atomate as many steps as posible

    = **Continuius Integration** Continuously run test and packaging
    = **Continuius Deployment** Continuously deploy to test enviroments
    = **Continuius Delivery** Continuously deploy to production

Recommended things to do:
    - Satic Code Analysis
        - Lint, Sonar
        - Include Static Security Checks
    - Runtime Checks
        - Run vulnerability Scanners
    - Tests
        - Unit tests
        - Integration tests
        - System tests
        - Sanity and Regression tests

_Spinnaker_: Multicloud continuous delivery platform

**Infrastructure as Code**: Treat infrastructure the same way as application code
    - Terraform: Open Source Cloud Neutral
    - Google Cloud Deployment Manager

# Site Reliability Engineering (SRE)

Focus on every aspect of an application:
    - availability, latency, performance, efficiency, change, management, monitoring, emergency response, and capacity planning
    Key principles:
        - Manage by Service Level Objevtives (SLOs)
        - Minimize toil (maul work to do -> automate as many things as possible)
        - Moving fast by reducing cost of failure -> **Have frequent small releases** | **automate things**
        - Share ownership with developers

## SRE Key Metrics
To metric:
    - **Service Level Indicator (SLI):** Quantitative measure of an aspect of a service
        availability, latencym throughput, durability
    - **Service Level Objective (SLO)** - SLI + target
        99.99 availability
    - **Service Level agreement (SLA)** - SLO + Consequences (contract)
        Have stricter SLOs than the SLAs

## SRE Best Practices

- Handling Excess Loads:
    - Load shedding: 
        - Set API Limits
        - Streaming Data
    - Reduce Quality of Service:
        Instead of talking to an API, return a hardcoded set of values
- Avoiding cascading failures
    - Plan to avoid thrashing
        Circuit breaker
- Penetration Testing (Ethical Hacking)
    - Simulate an attack with the objective of finding security vulnerabilities
- Load testing
    - Simulate real world traffic as closely as possible
- Resilience testing: How an app behaves under stress
    - Include network in your testing
