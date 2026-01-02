# DevOps Documentation Prompts

This document contains a collection of prompts for generating DevOps documentation and operational guides, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

### Standard Prompts (1-10)
1. [Generate Infrastructure Documentation](#generate-infrastructure-documentation)
2. [Generate Deployment Runbook](#generate-deployment-runbook)
3. [Generate Incident Response Playbook](#generate-incident-response-playbook)
4. [Generate Operational Procedures Manual](#generate-operational-procedures-manual)
5. [Generate API Documentation](#generate-api-documentation)
6. [Generate Security Configuration Guide](#generate-security-configuration-guide)
7. [Generate Monitoring Setup Guide](#generate-monitoring-setup-guide)
8. [Generate Disaster Recovery Documentation](#generate-disaster-recovery-documentation)
9. [Generate Configuration Management Guide](#generate-configuration-management-guide)
10. [Generate Performance Optimization Guide](#generate-performance-optimization-guide)

### Advanced Prompts (11-20)
11. [Generate Advanced Architecture Design Document](#generate-advanced-architecture-design-document)
12. [Generate Advanced Compliance Documentation](#generate-advanced-compliance-documentation)
13. [Generate Advanced GitOps Documentation](#generate-advanced-gitops-documentation)
14. [Generate Advanced Service Mesh Documentation](#generate-advanced-service-mesh-documentation)
15. [Generate Advanced Multi-Cloud Documentation](#generate-advanced-multi-cloud-documentation)
16. [Generate Advanced Security Operations Manual](#generate-advanced-security-operations-manual)
17. [Generate Advanced Performance Engineering Guide](#generate-advanced-performance-engineering-guide)
18. [Generate Advanced Infrastructure Automation Guide](#generate-advanced-infrastructure-automation-guide)
19. [Generate Advanced Observability Implementation Guide](#generate-advanced-observability-implementation-guide)

---

## Generate Infrastructure Documentation

### Purpose

Create comprehensive infrastructure documentation including architecture diagrams, component descriptions, and operational procedures.

### Prompt

```
You are an expert DevOps engineer specializing in technical documentation and infrastructure architecture.

Generate comprehensive infrastructure documentation for [INFRASTRUCTURE_SYSTEM] including:

- Architecture Overview: System architecture diagram and component relationships
- Component Descriptions: Detailed descriptions of each infrastructure component
- Network Architecture: Network topology, security groups, and connectivity patterns
- Deployment Procedures: Step-by-step deployment and configuration processes
- Monitoring and Alerting: Monitoring setup, alert configurations, and escalation procedures
- Security Configuration: Security policies, access controls, and compliance requirements
- Troubleshooting Guide: Common issues, diagnostic procedures, and resolution steps

Requirements:
- Use clear, technical language suitable for infrastructure teams
- Include configuration examples and command references
- Provide visual diagrams where appropriate (ASCII art or Mermaid syntax)
- Include version information and change tracking
- Add links to relevant tools and external documentation
- Include capacity planning and scaling considerations

Create documentation that serves as a comprehensive reference for infrastructure operations.
```

**Notes:** Include both high-level architectural views and detailed technical specifications. Ensure documentation is maintained and updated with infrastructure changes. Consider different audiences: architects, operators, and security teams.

---

## Generate Deployment Runbook

### Purpose

Create detailed deployment runbooks with step-by-step procedures, rollback plans, and emergency procedures.

### Prompt

```
You are an expert DevOps engineer specializing in deployment automation and operational procedures.

Generate a comprehensive deployment runbook for [APPLICATION_NAME] including:

- Pre-deployment Checklist: Environment validation, dependency checks, and readiness verification
- Deployment Procedures: Step-by-step deployment process with commands and validations
- Post-deployment Validation: Testing procedures, health checks, and verification steps
- Rollback Procedures: Emergency rollback process with clear decision criteria
- Communication Protocol: Stakeholder notifications, status updates, and escalation paths
- Troubleshooting Section: Common deployment issues and resolution procedures
- Emergency Contacts: Contact information for escalation and support

Requirements:
- Include specific commands, scripts, and configuration examples
- Provide clear decision points and validation criteria
- Include timing estimates for each procedure
- Add safety checks and confirmation steps
- Include integration with monitoring and alerting systems
- Provide templates for communication and reporting

Create a runbook that enables reliable and repeatable deployments with clear emergency procedures.
```

**Notes:** Test runbook procedures regularly to ensure accuracy and completeness. Include both manual and automated deployment procedures. Consider different deployment scenarios: normal, emergency, and rollback.

---

## Generate Incident Response Playbook

### Purpose

Create detailed incident response playbooks for common infrastructure and application issues.

### Prompt

```
You are an expert DevOps engineer specializing in incident management and operational procedures.

Generate an incident response playbook for [INCIDENT_TYPE] including:

- Incident Classification: Severity levels, impact assessment, and escalation criteria
- Initial Response: Immediate actions, triage procedures, and team notification
- Investigation Procedures: Diagnostic steps, data collection, and root cause analysis
- Containment Actions: Immediate fixes, workarounds, and damage limitation
- Resolution Steps: Permanent fix procedures, testing, and validation
- Communication Plan: Status updates, stakeholder notifications, and reporting
- Post-incident Activities: Documentation, lessons learned, and improvement actions

Requirements:
- Include specific diagnostic commands and troubleshooting procedures
- Provide clear decision trees and escalation paths
- Include integration with monitoring and alerting systems
- Add communication templates and status update procedures
- Include compliance and audit trail requirements
- Provide metrics and KPIs for incident management

Create a playbook that enables rapid incident response with comprehensive documentation.
```

**Notes:** Include contact information and escalation procedures for different incident severities. Test playbook procedures through regular incident response drills. Update playbooks based on actual incident experiences and lessons learned.

---

## Generate Operational Procedures Manual

### Purpose

Create comprehensive operational procedures manual covering routine maintenance, monitoring, and administrative tasks.

### Prompt

```
You are an expert DevOps engineer specializing in operational procedures and system administration.

Generate an operational procedures manual for [SYSTEM_ENVIRONMENT] including:

- Routine Maintenance: Scheduled maintenance tasks, procedures, and checklists
- Monitoring Procedures: Health check routines, metric analysis, and alert response
- Backup Operations: Backup procedures, validation, and recovery testing
- Security Operations: Security monitoring, patch management, and compliance tasks
- Performance Management: Performance monitoring, optimization, and capacity planning
- Change Management: Change control procedures, approval workflows, and documentation
- Administrative Tasks: User management, access control, and system configuration

Requirements:
- Include specific procedures with step-by-step instructions
- Provide checklists and validation criteria for each procedure
- Include frequency and timing for routine tasks
- Add safety procedures and rollback options
- Include integration with ticketing and change management systems
- Provide templates for documentation and reporting

Create a manual that ensures consistent operational practices and system reliability.
```

**Notes:** Include procedures for both routine operations and emergency situations. Ensure procedures are tested and validated by operational teams. Consider automation opportunities for routine operational tasks.

---

## Generate API Documentation

### Purpose

Create comprehensive API documentation including endpoints, authentication, examples, and operational considerations.

### Prompt

```
You are an expert DevOps engineer specializing in API documentation and developer experience.

Generate comprehensive API documentation for [API_SERVICE] including:

- API Overview: Purpose, architecture, and integration patterns
- Authentication: Authentication methods, token management, and security requirements
- Endpoints Documentation: HTTP methods, parameters, request/response examples
- Error Handling: Error codes, error messages, and troubleshooting guidance
- Rate Limiting: Rate limits, quota management, and throttling policies
- Monitoring and Logging: API metrics, logging requirements, and observability
- Operational Information: SLA commitments, maintenance windows, and support procedures

Requirements:
- Include practical code examples in multiple languages
- Provide interactive examples and testing procedures
- Include performance characteristics and scaling information
- Add troubleshooting guides for common integration issues
- Include versioning strategy and backward compatibility information
- Provide operational metrics and monitoring guidance

Create documentation that enables effective API adoption and operational support.
```

**Notes:** Include both functional documentation and operational considerations. Provide examples that developers can copy and modify for their use cases. Keep documentation synchronized with API changes and versioning.

---

## Generate Security Configuration Guide

### Purpose

Create detailed security configuration guides covering hardening, compliance, and security best practices.

### Prompt

```
You are an expert DevOps engineer specializing in security configuration and compliance management.

Generate a comprehensive security configuration guide for [SECURITY_DOMAIN] including:

- Security Architecture: Security layers, defense-in-depth strategy, and component relationships
- Configuration Hardening: System hardening procedures, security settings, and baseline configurations
- Access Control: Authentication setup, authorization policies, and privilege management
- Network Security: Firewall rules, network segmentation, and traffic encryption
- Monitoring and Auditing: Security monitoring setup, log analysis, and compliance reporting
- Incident Response: Security incident procedures, forensics, and recovery processes
- Compliance Requirements: Regulatory compliance, audit procedures, and documentation requirements

Requirements:
- Include specific configuration examples and security settings
- Provide validation procedures and security testing guidance
- Include compliance mapping for relevant standards (PCI DSS, SOC 2, etc.)
- Add security monitoring and alerting configurations
- Include automated security scanning and validation procedures
- Provide security metrics and KPIs for ongoing management

Create a guide that ensures comprehensive security implementation and ongoing compliance.
```

**Notes:** Include both preventive and detective security controls. Provide specific compliance requirements for retail and payment processing. Include security automation and policy-as-code approaches.

---

## Generate Monitoring Setup Guide

### Purpose

Create comprehensive monitoring setup guides including tool configuration, dashboard creation, and alerting strategies.

### Prompt

```
You are an expert DevOps engineer specializing in observability and monitoring system implementation.

Generate a comprehensive monitoring setup guide for [MONITORING_SCOPE] including:

- Monitoring Architecture: Monitoring stack components, data flow, and integration patterns
- Tool Configuration: Installation procedures, configuration files, and setup validation
- Dashboard Creation: Dashboard design principles, visualization guidelines, and template creation
- Alert Configuration: Alert rule design, notification setup, and escalation procedures
- Data Collection: Metric definition, collection strategies, and data quality assurance
- Performance Optimization: Query optimization, data retention, and resource management
- Operational Procedures: Maintenance tasks, troubleshooting, and system health monitoring

Requirements:
- Include specific configuration examples and setup procedures
- Provide dashboard templates and visualization best practices
- Include alert rule examples with appropriate thresholds
- Add data retention and performance optimization guidance
- Include integration with external systems and tools
- Provide monitoring system backup and disaster recovery procedures

Create a guide that enables comprehensive monitoring implementation and effective observability.
```

**Notes:** Include both infrastructure and application monitoring considerations. Provide specific examples of effective dashboards and alert configurations. Consider monitoring system scalability and performance requirements.

---

## Generate Disaster Recovery Documentation

### Purpose

Create comprehensive disaster recovery documentation including procedures, testing plans, and recovery validation.

### Prompt

```
You are an expert DevOps engineer specializing in disaster recovery planning and business continuity.

Generate comprehensive disaster recovery documentation for [SYSTEM_CRITICAL] including:

- Recovery Objectives: RTO/RPO definitions, business impact analysis, and priority classification
- Recovery Procedures: Step-by-step recovery processes, dependency management, and validation steps
- Testing Framework: DR testing schedules, test scenarios, and success criteria
- Communication Plans: Notification procedures, status updates, and stakeholder management
- Resource Requirements: Infrastructure needs, personnel requirements, and vendor contacts
- Validation Procedures: System validation, data integrity checks, and performance verification
- Lessons Learned: Historical incident analysis, improvement recommendations, and plan updates

Requirements:
- Include specific recovery procedures with detailed commands and steps
- Provide testing procedures that can be executed without business impact
- Include communication templates for different stakeholder groups
- Add resource allocation and cost considerations
- Include compliance and regulatory requirements
- Provide metrics and KPIs for disaster recovery capabilities

Create documentation that ensures effective disaster recovery with comprehensive testing and validation.
```

**Notes:** Include both technical procedures and business continuity considerations. Provide regular testing schedules and validation procedures. Consider dependencies between systems and recovery sequencing.

---

## Generate Configuration Management Guide

### Purpose

Create detailed configuration management guides covering version control, change tracking, and environment management.

### Prompt

```
You are an expert DevOps engineer specializing in configuration management and infrastructure automation.

Generate a comprehensive configuration management guide for [CONFIGURATION_SCOPE] including:

- Configuration Strategy: Configuration management principles, version control, and change tracking
- Tool Implementation: Configuration management tool setup, workflow design, and integration patterns
- Environment Management: Environment definitions, promotion workflows, and consistency validation
- Change Control: Change approval processes, testing procedures, and rollback strategies
- Compliance Management: Configuration compliance, audit trails, and policy enforcement
- Automation Integration: CI/CD integration, automated testing, and deployment automation
- Operational Procedures: Configuration monitoring, drift detection, and remediation processes

Requirements:
- Include specific tool configurations and workflow examples
- Provide configuration templates and standardization guidelines
- Include testing and validation procedures for configuration changes
- Add compliance monitoring and reporting procedures
- Include integration with existing development and operations workflows
- Provide configuration backup and recovery procedures

Create a guide that ensures consistent configuration management with effective change control.
```

**Notes:** Include both infrastructure and application configuration management. Provide specific examples of effective configuration organization and versioning. Consider configuration security and secret management requirements.

---

## Generate Performance Optimization Guide

### Purpose

Create comprehensive performance optimization guides including analysis procedures, tuning strategies, and monitoring approaches.

### Prompt

```
You are an expert DevOps engineer specializing in performance optimization and capacity management.

Generate a comprehensive performance optimization guide for [PERFORMANCE_TARGET] including:

- Performance Baseline: Baseline establishment, metric definition, and measurement procedures
- Analysis Methodology: Performance analysis techniques, bottleneck identification, and profiling procedures
- Optimization Strategies: Tuning approaches, configuration optimization, and architectural improvements
- Testing Procedures: Load testing, stress testing, and performance validation
- Monitoring Implementation: Performance monitoring setup, alerting strategies, and trend analysis
- Capacity Planning: Growth projections, resource planning, and scaling strategies
- Continuous Improvement: Performance culture, optimization cycles, and feedback loops

Requirements:
- Include specific analysis tools and profiling techniques
- Provide optimization examples with before/after comparisons
- Include load testing procedures and realistic scenarios
- Add performance monitoring and alerting configurations
- Include cost-performance trade-off analysis
- Provide performance regression detection and prevention strategies

Create a guide that enables systematic performance optimization with measurable improvements.
```

**Notes:** Include both application and infrastructure performance optimization techniques. Provide specific examples of successful performance optimization initiatives. Consider business impact and cost considerations in optimization recommendations.

---

## Generate Advanced Architecture Design Document

### Purpose

Create comprehensive architecture design documents for complex enterprise systems with detailed technical specifications.

### Prompt

```
You are an expert DevOps engineer specializing in enterprise architecture design and technical documentation.

Generate a comprehensive architecture design document for [ARCHITECTURE_SYSTEM] including:

- Executive Summary: Business context, technical objectives, and strategic alignment
- System Architecture: Detailed component architecture, service interactions, and data flows
- Technical Specifications: Technology stack decisions, integration patterns, and protocol specifications
- Security Architecture: Security layers, threat modeling, and compliance requirements
- Scalability Design: Performance characteristics, scaling strategies, and capacity planning
- Operational Architecture: Deployment strategies, monitoring approach, and maintenance procedures
- Risk Analysis: Technical risks, mitigation strategies, and contingency planning

Requirements:
- Include detailed architectural diagrams with component relationships
- Provide technology decision rationale with alternative analysis
- Include non-functional requirements and quality attributes
- Add implementation phases with dependencies and milestones
- Include cost analysis and resource requirements
- Provide success metrics and acceptance criteria

Create documentation that serves as a comprehensive technical blueprint for complex system implementation.
```

**Notes:** Include both technical architecture and operational considerations. Provide specific technology choices with detailed justification. Consider enterprise constraints and integration requirements.

---

## Generate Advanced Compliance Documentation

### Purpose

Create detailed compliance documentation framework covering regulatory requirements, audit procedures, and evidence management.

### Prompt

```
You are an expert DevOps engineer specializing in compliance automation and regulatory documentation.

Generate comprehensive compliance documentation for [COMPLIANCE_FRAMEWORK] including:

- Compliance Overview: Regulatory requirements, scope definition, and compliance objectives
- Control Implementation: Technical controls, policy implementation, and automated compliance
- Evidence Management: Evidence collection, documentation procedures, and audit trail maintenance
- Assessment Procedures: Compliance testing, validation procedures, and gap analysis
- Reporting Framework: Compliance reporting, dashboard creation, and stakeholder communication
- Incident Management: Compliance incident procedures, reporting requirements, and remediation
- Continuous Improvement: Compliance maturity assessment, improvement planning, and program evolution

Requirements:
- Include specific control implementations with technical examples
- Provide audit procedures and evidence collection templates
- Include automated compliance monitoring and reporting
- Add compliance testing and validation procedures
- Include integration with existing security and operational tools
- Provide compliance metrics and KPIs for ongoing management

Create documentation that ensures comprehensive compliance with automated evidence collection and reporting.
```

**Notes:** Include both technical controls and organizational process requirements. Provide specific automation examples for compliance monitoring and reporting. Consider compliance as an ongoing operational practice with continuous improvement.

---

## Generate Advanced GitOps Documentation

### Purpose

Create comprehensive GitOps documentation covering workflow design, tool integration, and organizational adoption strategies.

### Prompt

```
You are an expert DevOps engineer specializing in GitOps implementation and organizational transformation.

Generate comprehensive GitOps documentation for [GITOPS_IMPLEMENTATION] including:

- GitOps Strategy: Workflow design, repository organization, and branching strategies
- Tool Implementation: GitOps operator configuration, integration patterns, and automation workflows
- Security Framework: RBAC implementation, policy enforcement, and secret management
- Environment Management: Multi-environment workflows, promotion strategies, and configuration management
- Monitoring Integration: Deployment monitoring, drift detection, and observability
- Incident Response: GitOps incident procedures, rollback strategies, and emergency protocols
- Organizational Adoption: Change management, training programs, and success measurement

Requirements:
- Include specific tool configurations and workflow examples
- Provide repository organization templates and branching strategies
- Include security implementation with policy-as-code examples
- Add monitoring and observability configurations
- Include organizational change management procedures
- Provide GitOps maturity assessment and improvement frameworks

Create documentation that enables successful GitOps adoption with comprehensive operational guidance.
```

**Notes:** Include both technical implementation and organizational transformation aspects. Provide specific examples of successful GitOps patterns and workflows. Consider enterprise constraints and integration with existing tools and processes.

---

## Generate Advanced Service Mesh Documentation

### Purpose

Create detailed service mesh documentation covering architecture, configuration, security, and operational procedures.

### Prompt

```
You are an expert DevOps engineer specializing in service mesh architecture and microservices communication.

Generate comprehensive service mesh documentation for [SERVICE_MESH_PLATFORM] including:

- Service Mesh Architecture: Control plane and data plane architecture, component relationships
- Configuration Management: Service mesh configuration, policy management, and version control
- Security Implementation: mTLS configuration, authentication policies, and authorization strategies
- Traffic Management: Routing strategies, load balancing, and traffic policies
- Observability Integration: Distributed tracing, metrics collection, and monitoring setup
- Performance Optimization: Service mesh performance tuning, resource optimization, and scaling
- Operational Procedures: Deployment strategies, troubleshooting guides, and maintenance procedures

Requirements:
- Include detailed configuration examples and implementation patterns
- Provide security policy templates and best practices
- Include observability configuration and dashboard templates
- Add performance tuning guidelines and optimization strategies
- Include troubleshooting procedures and common issue resolution
- Provide migration strategies and adoption roadmaps

Create documentation that enables effective service mesh implementation with comprehensive operational support.
```

**Notes:** Include both service mesh configuration and application integration considerations. Provide specific examples of effective service mesh policies and configurations. Consider service mesh complexity and operational overhead in recommendations.

---

## Generate Advanced Multi-Cloud Documentation

### Purpose

Create comprehensive multi-cloud documentation covering strategy, implementation, and operational considerations.

### Prompt

```
You are an expert DevOps engineer specializing in multi-cloud strategy and implementation.

Generate comprehensive multi-cloud documentation for [MULTICLOUD_STRATEGY] including:

- Multi-Cloud Strategy: Cloud provider selection, workload distribution, and integration strategies
- Architecture Design: Cloud-agnostic patterns, abstraction layers, and service mapping
- Data Management: Cross-cloud data strategies, synchronization, and consistency management
- Network Architecture: Inter-cloud connectivity, traffic management, and security considerations
- Operational Framework: Management tools, monitoring strategies, and unified operations
- Cost Management: Cross-cloud cost optimization, resource allocation, and billing management
- Risk Management: Vendor risk mitigation, disaster recovery, and business continuity

Requirements:
- Include specific implementation examples and architectural patterns
- Provide cloud provider comparison and selection criteria
- Include cost analysis and optimization strategies
- Add operational procedures for multi-cloud management
- Include disaster recovery and business continuity procedures
- Provide multi-cloud maturity assessment and improvement frameworks

Create documentation that enables effective multi-cloud implementation with comprehensive operational guidance.
```

**Notes:** Include both technical implementation and business strategy considerations. Provide specific examples of successful multi-cloud patterns and anti-patterns. Consider organizational readiness and skills requirements for multi-cloud operations.

---

## Generate Advanced Security Operations Manual

### Purpose

Create comprehensive security operations documentation covering threat detection, incident response, and continuous security monitoring.

### Prompt

```
You are an expert DevOps engineer specializing in security operations and incident response.

Generate a comprehensive security operations manual for [SECURITY_ENVIRONMENT] including:

- Security Architecture: Security layers, threat modeling, and defense-in-depth implementation
- Threat Detection: Security monitoring setup, threat intelligence integration, and anomaly detection
- Incident Response: Security incident procedures, forensics, and recovery processes
- Vulnerability Management: Vulnerability scanning, assessment, and remediation workflows
- Compliance Monitoring: Automated compliance checking, audit procedures, and reporting
- Security Automation: SOAR implementation, automated response, and security orchestration
- Continuous Improvement: Security metrics, maturity assessment, and program enhancement

Requirements:
- Include specific security tool configurations and integration patterns
- Provide incident response playbooks with detailed procedures
- Include vulnerability management workflows and automation
- Add compliance monitoring and reporting procedures
- Include security automation and orchestration examples
- Provide security metrics and KPIs for program management

Create documentation that enables effective security operations with automated threat detection and response.
```

**Notes:** Include both preventive and detective security controls with automated response capabilities. Provide specific examples of security automation and orchestration workflows. Consider regulatory requirements and compliance obligations in security operations.

---

## Generate Advanced Performance Engineering Guide

### Purpose

Create comprehensive performance engineering documentation covering analysis, optimization, and scalability strategies.

### Prompt

```
You are an expert DevOps engineer specializing in performance engineering and scalability optimization.

Generate a comprehensive performance engineering guide for [PERFORMANCE_SYSTEM] including:

- Performance Architecture: Performance-oriented design patterns, scalability strategies, and bottleneck prevention
- Analysis Methodology: Performance profiling, load testing, and capacity analysis techniques
- Optimization Framework: Multi-layer optimization strategies, performance tuning, and efficiency improvements
- Monitoring Strategy: Performance monitoring, alerting, and observability implementation
- Scalability Planning: Auto-scaling strategies, capacity planning, and growth management
- Testing Framework: Performance testing, chaos engineering, and resilience validation
- Continuous Optimization: Performance culture, optimization cycles, and improvement measurement

Requirements:
- Include detailed performance analysis techniques and tools
- Provide optimization strategies with specific implementation examples
- Include scalability patterns and auto-scaling configurations
- Add performance testing frameworks and realistic scenarios
- Include performance monitoring and alerting strategies
- Provide performance regression detection and prevention procedures

Create documentation that enables systematic performance engineering with measurable scalability improvements.
```

**Notes:** Include both application and infrastructure performance engineering considerations. Provide specific examples of successful performance optimization and scalability implementations. Consider cost-performance trade-offs and business impact in optimization strategies.

---

## Generate Advanced Infrastructure Automation Guide

### Purpose

Create comprehensive infrastructure automation documentation covering IaC, configuration management, and operational automation.

### Prompt

```
You are an expert DevOps engineer specializing in infrastructure automation and configuration management.

Generate comprehensive infrastructure automation documentation for [AUTOMATION_SCOPE] including:

- Automation Strategy: Infrastructure automation principles, tool selection, and workflow design
- Infrastructure as Code: IaC implementation, module design, and version management
- Configuration Management: Configuration automation, drift detection, and remediation strategies
- Deployment Automation: Automated deployment pipelines, testing, and validation procedures
- Operational Automation: Automated operations, self-healing systems, and intelligent automation
- Compliance Automation: Policy-as-code, automated compliance, and audit automation
- Continuous Improvement: Automation maturity, optimization opportunities, and enhancement strategies

Requirements:
- Include specific automation tool configurations and implementation patterns
- Provide IaC templates and module design examples
- Include automated testing and validation procedures
- Add operational automation and self-healing examples
- Include compliance automation and policy-as-code implementations
- Provide automation maturity assessment and improvement frameworks

Create documentation that enables comprehensive infrastructure automation with intelligent operational capabilities.
```

**Notes:** Include both infrastructure provisioning and operational automation considerations. Provide specific examples of successful automation implementations and patterns. Consider automation complexity and maintenance requirements in implementation strategies.

---

## Generate Advanced Observability Implementation Guide

### Purpose

Create comprehensive observability documentation covering distributed tracing, advanced monitoring, and intelligent alerting.

### Prompt

```
You are an expert DevOps engineer specializing in advanced observability and intelligent monitoring systems.

Generate comprehensive observability implementation guide for [OBSERVABILITY_PLATFORM] including:

- Observability Architecture: Three pillars of observability, correlation strategies, and data pipeline design
- Advanced Monitoring: Custom metrics, business KPIs, and intelligent alerting strategies
- Distributed Tracing: End-to-end tracing, service dependency mapping, and performance analysis
- Log Management: Structured logging, log aggregation, and intelligent log analysis
- AI-Powered Insights: Anomaly detection, predictive analytics, and automated root cause analysis
- Performance Analytics: Application performance monitoring, user experience tracking, and business impact analysis
- Operational Intelligence: Observability-driven operations, intelligent automation, and continuous optimization

Requirements:
- Include advanced observability tool configurations and integration patterns
- Provide custom metric and dashboard implementation examples
- Include distributed tracing setup and analysis procedures
- Add AI-powered monitoring and alerting configurations
- Include observability automation and intelligent response procedures
- Provide observability maturity assessment and improvement frameworks

Create documentation that enables advanced observability with AI-powered insights and automated operational intelligence.
```

**Notes:** Include both technical observability and business intelligence considerations. Provide specific examples of advanced observability implementations and AI integration. Consider observability data volume and cost optimization in implementation strategies. 