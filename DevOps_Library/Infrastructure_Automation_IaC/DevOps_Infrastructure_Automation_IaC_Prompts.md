# DevOps Infrastructure Automation & IaC Prompts

## 1. Generate Terraform Module for AWS VPC
**ID:** devops-terraform-vpc-module  
**Purpose:** Create a comprehensive Terraform module for AWS VPC with public/private subnets, NAT gateways, and security groups following best practices.

### Prompt:
You are an expert DevOps engineer specializing in Infrastructure as Code with Terraform and AWS networking.

Generate a complete Terraform module for AWS VPC infrastructure including:

- VPC Configuration: VPC with [CIDR_BLOCK] CIDR block and DNS resolution enabled
- Subnet Design: [PUBLIC_SUBNET_COUNT] public subnets and [PRIVATE_SUBNET_COUNT] private subnets across multiple AZs
- Internet Gateway: Configure internet gateway for public subnet access
- NAT Gateways: Deploy NAT gateways in public subnets for private subnet internet access
- Route Tables: Configure routing for public and private subnets with proper associations
- Security Groups: Default security groups for web tier, application tier, and database tier
- Network ACLs: Configure network ACLs for additional security layers

Requirements:
- Use proper variable validation and type constraints
- Include comprehensive outputs for VPC ID, subnet IDs, and security group IDs
- Implement consistent tagging strategy with environment and project tags
- Support multiple availability zones for high availability
- Include data sources for AMI lookup and AZ discovery
- Configure proper CIDR block calculations for subnet distribution

Provide the complete module structure with variables.tf, main.tf, outputs.tf, and README.md.

### Notes:
- Follow Terraform naming conventions and use descriptive resource names.
- Include examples directory with sample usage scenarios.
- Implement proper variable validation to prevent configuration errors.

### Placeholders:
- **CIDR_BLOCK**: VPC CIDR block (e.g., 10.0.0.0/16, 172.16.0.0/16)
- **PUBLIC_SUBNET_COUNT**: Number of public subnets (e.g., 2, 3)
- **PRIVATE_SUBNET_COUNT**: Number of private subnets (e.g., 3, 6)

---

## 2. Generate Ansible Playbook for Server Configuration
**ID:** devops-ansible-server-config  
**Purpose:** Create comprehensive Ansible playbooks for server configuration with security hardening, monitoring setup, and application deployment.

### Prompt:
You are an expert DevOps engineer specializing in configuration management with Ansible.

Generate an Ansible playbook for [SERVER_TYPE] configuration including:

- System Configuration: Base system setup with package management and system updates
- Security Hardening: SSH configuration, firewall rules, and user management
- Service Installation: Install and configure [APPLICATION_STACK] services
- Monitoring Setup: Configure monitoring agents and log collection
- SSL/TLS Configuration: Set up SSL certificates and secure communication
- Backup Configuration: Configure automated backup scripts and schedules
- Performance Tuning: Optimize system performance for the target workload

Requirements:
- Use Ansible roles for modular and reusable configuration
- Implement proper error handling and task validation
- Include handlers for service restarts and configuration reloads
- Support multiple environments (dev, staging, production)
- Use Ansible Vault for sensitive configuration data
- Include comprehensive task tags for selective execution
- Implement idempotent operations with proper conditionals

Provide the complete playbook structure with roles, handlers, and inventory examples.

### Notes:
- Test playbooks in staging environments before production deployment.
- Use Ansible Galaxy roles where appropriate to avoid reinventing common functionality.
- Implement proper logging and debugging for troubleshooting failed deployments.

### Placeholders:
- **SERVER_TYPE**: Type of server (e.g., web server, database server, application server, load balancer)
- **APPLICATION_STACK**: Application stack to install (e.g., NGINX + PHP, Apache + Python, Node.js, Java Tomcat)

---

## 3. Generate CloudFormation Template for EKS Cluster
**ID:** devops-cloudformation-eks  
**Purpose:** Create a production-ready CloudFormation template for Amazon EKS cluster with node groups, networking, and security configurations.

### Prompt:
You are an expert DevOps engineer specializing in AWS CloudFormation and Kubernetes infrastructure.

Generate a comprehensive CloudFormation template for EKS cluster deployment including:

- EKS Cluster: Configure EKS cluster with [KUBERNETES_VERSION] and proper IAM roles
- Node Groups: Create managed node groups with [INSTANCE_TYPES] instances and auto-scaling
- Networking: VPC configuration with public and private subnets across multiple AZs
- Security: Configure security groups, IAM roles, and RBAC policies
- Add-ons: Install essential cluster add-ons (VPC CNI, CoreDNS, kube-proxy)
- Logging: Enable CloudWatch logging for API server, audit, and authenticator
- Monitoring: Configure CloudWatch Container Insights and Prometheus metrics

Requirements:
- Use CloudFormation parameters for environment-specific configurations
- Implement proper resource dependencies and conditions
- Include comprehensive outputs for cluster endpoint and certificate authority
- Configure proper tagging for cost allocation and resource management
- Support spot instances for cost optimization in non-production environments
- Include cluster autoscaler configuration and IAM permissions
- Configure proper encryption for EBS volumes and secrets

Provide the complete CloudFormation template with parameter definitions and deployment instructions.

### Notes:
- Test cluster deployment in a development environment before production use.
- Consider using AWS CDK for more complex infrastructure requirements.
- Implement proper backup strategies for persistent volumes and cluster state.

### Placeholders:
- **KUBERNETES_VERSION**: Kubernetes version (e.g., 1.28, 1.29, 1.30)
- **INSTANCE_TYPES**: EC2 instance types for node groups (e.g., t3.medium, m5.large, c5.xlarge)

---

## 4. Generate Pulumi Infrastructure Stack
**ID:** devops-pulumi-infrastructure  
**Purpose:** Create a Pulumi infrastructure stack with multi-cloud capabilities, state management, and comprehensive resource provisioning.

### Prompt:
You are an expert DevOps engineer specializing in Infrastructure as Code with Pulumi and modern cloud architectures.

Generate a Pulumi stack for [INFRASTRUCTURE_TYPE] deployment including:

- Resource Definition: Define cloud resources using [PROGRAMMING_LANGUAGE] with type safety
- Stack Configuration: Configure stack settings with proper secret management
- Component Resources: Create reusable component resources for common patterns
- Cross-Stack References: Implement stack references for shared resources
- Policy Management: Include policy as code for compliance and governance
- Testing Framework: Implement unit tests and integration tests for infrastructure
- Deployment Automation: Configure CI/CD integration with automated deployments

Requirements:
- Use Pulumi best practices for resource organization and naming
- Implement proper error handling and resource cleanup
- Configure stack outputs for integration with other systems
- Support multiple environments with stack-specific configurations
- Include comprehensive documentation and examples
- Implement cost tracking and resource tagging strategies
- Configure proper state backend and encryption

Provide the complete Pulumi project structure with configuration files and deployment scripts.

### Notes:
- Leverage Pulumi's programming language features for complex logic and validation.
- Use Pulumi policy packs for enforcing organizational standards.
- Implement proper testing strategies including property-based testing.

### Placeholders:
- **INFRASTRUCTURE_TYPE**: Infrastructure type (e.g., microservices platform, data pipeline, serverless application, hybrid cloud)
- **PROGRAMMING_LANGUAGE**: Programming language (e.g., TypeScript, Python, Go, C#)

---

## 5. Generate Azure Bicep Template for App Service
**ID:** devops-bicep-app-service  
**Purpose:** Create comprehensive Azure Bicep templates for App Service deployment with monitoring, security, and scaling configurations.

### Prompt:
You are an expert DevOps engineer specializing in Azure infrastructure and Bicep templates.

Generate a complete Bicep template for Azure App Service deployment including:

- App Service Plan: Configure App Service plan with [SKU_TIER] tier and appropriate scaling
- Web Application: Deploy web app with [RUNTIME_STACK] runtime and configuration
- Application Insights: Set up monitoring and performance tracking
- Key Vault Integration: Configure secure access to secrets and certificates
- Custom Domain: Set up custom domain with SSL certificate management
- Deployment Slots: Configure staging and production deployment slots
- Networking: Configure virtual network integration and private endpoints

Requirements:
- Use Bicep modules for reusable infrastructure components
- Implement proper parameter validation and default values
- Configure comprehensive diagnostic settings and logging
- Include auto-scaling rules based on CPU and memory metrics
- Set up continuous deployment from source control
- Configure proper backup and disaster recovery
- Implement security best practices with managed identities

Provide the complete Bicep template structure with modules and parameter files.

### Notes:
- Use Azure Policy integration for compliance and governance requirements.
- Implement proper cost management with budget alerts and recommendations.
- Consider using Azure Front Door for global load balancing and CDN.

### Placeholders:
- **SKU_TIER**: App Service plan SKU (e.g., S1, P1v2, P2v3)
- **RUNTIME_STACK**: Runtime stack (e.g., .NET 6, Node.js 18, Python 3.9, Java 11)

---

## 6. Generate Google Cloud Deployment Manager Template
**ID:** devops-gcp-deployment-manager  
**Purpose:** Create Google Cloud Deployment Manager templates for GKE cluster with networking, security, and monitoring components.

### Prompt:
You are an expert DevOps engineer specializing in Google Cloud Platform and infrastructure automation.

Generate a Deployment Manager template for GCP infrastructure including:

- GKE Cluster: Configure GKE cluster with [NODE_POOL_CONFIG] node pools and security settings
- Networking: Set up VPC, subnets, and firewall rules for cluster communication
- Identity Management: Configure service accounts and IAM bindings
- Storage: Set up persistent disk configurations and storage classes
- Monitoring: Configure Google Cloud Monitoring and logging
- Security: Implement Binary Authorization and Pod Security Policies
- Backup: Configure automated backup solutions for persistent data

Requirements:
- Use Deployment Manager templates with proper resource dependencies
- Implement template properties for environment-specific configurations
- Configure proper resource naming and labeling conventions
- Include comprehensive outputs for resource references
- Set up network policies for micro-segmentation
- Configure cluster autoscaling and node auto-provisioning
- Implement proper secret management with Google Secret Manager

Provide the complete Deployment Manager configuration with template files and deployment scripts.

### Notes:
- Consider migrating to Terraform or Pulumi for more advanced infrastructure automation.
- Use Google Cloud Config Connector for Kubernetes-native resource management.
- Implement proper monitoring and alerting for infrastructure health.

### Placeholders:
- **NODE_POOL_CONFIG**: Node pool configuration (e.g., e2-standard-4 with 3-10 nodes, n1-standard-2 with preemptible instances)

---

## 7. Generate Infrastructure Testing Framework
**ID:** devops-infrastructure-testing  
**Purpose:** Create comprehensive testing framework for infrastructure code with unit tests, integration tests, and compliance validation.

### Prompt:
You are an expert DevOps engineer specializing in infrastructure testing and validation frameworks.

Generate a complete testing framework for [INFRASTRUCTURE_TOOL] infrastructure including:

- Unit Testing: Test individual modules and components with mock resources
- Integration Testing: Test complete infrastructure deployments in isolated environments
- Compliance Testing: Validate infrastructure against security and compliance standards
- Performance Testing: Test infrastructure performance and scaling capabilities
- Security Testing: Validate security configurations and access controls
- Cost Testing: Validate infrastructure costs against budgets and optimization opportunities
- Documentation Testing: Ensure documentation accuracy and completeness

Requirements:
- Use appropriate testing frameworks for the chosen infrastructure tool
- Implement test data management with fixtures and test environments
- Configure automated test execution in CI/CD pipelines
- Include test reporting and metrics collection
- Implement proper test isolation and cleanup procedures
- Configure parallel test execution for performance
- Include test coverage reporting and quality gates

Provide the complete testing framework with test examples and CI/CD integration.

### Notes:
- Implement infrastructure testing as early as possible in the development lifecycle.
- Use test-driven development practices for infrastructure code.
- Consider using mutation testing for more comprehensive test validation.

### Placeholders:
- **INFRASTRUCTURE_TOOL**: Infrastructure tool (e.g., Terraform, CloudFormation, Ansible, Pulumi)

---

## 8. Generate Multi-Cloud Resource Provisioning
**ID:** devops-multi-cloud-provisioning  
**Purpose:** Create infrastructure automation for multi-cloud resource provisioning with consistent configurations across cloud providers.

### Prompt:
You are an expert DevOps engineer specializing in multi-cloud architectures and infrastructure abstraction.

Generate multi-cloud infrastructure provisioning for [APPLICATION_WORKLOAD] including:

- Cloud Abstraction: Create abstraction layer for common resources across [PRIMARY_CLOUD] and [SECONDARY_CLOUD]
- Resource Mapping: Define equivalent resources and configurations for each cloud provider
- Networking: Configure cross-cloud networking with VPN or private connectivity
- Data Synchronization: Set up data replication and synchronization between clouds
- Identity Federation: Configure federated identity management across cloud providers
- Monitoring: Implement unified monitoring and alerting across all cloud environments
- Cost Optimization: Configure cost management and optimization across multiple clouds

Requirements:
- Use infrastructure tools that support multiple cloud providers
- Implement provider-agnostic resource definitions where possible
- Configure proper disaster recovery and failover mechanisms
- Include compliance validation for different regulatory requirements
- Set up centralized logging and audit trails
- Implement automated cost reporting and optimization recommendations
- Configure proper secret management across cloud boundaries

Provide the complete multi-cloud infrastructure configuration with deployment automation.

### Notes:
- Consider vendor lock-in implications and mitigation strategies.
- Implement proper network security and encryption for cross-cloud communication.
- Plan for data sovereignty and compliance requirements in different regions.

### Placeholders:
- **APPLICATION_WORKLOAD**: Application workload type (e.g., web application, data processing pipeline, microservices platform)
- **PRIMARY_CLOUD**: Primary cloud provider (e.g., AWS, Azure, Google Cloud)
- **SECONDARY_CLOUD**: Secondary cloud provider (e.g., Azure, Google Cloud, AWS)

---

## 9. Generate Configuration Management Automation
**ID:** devops-config-management  
**Purpose:** Create comprehensive configuration management automation with drift detection, compliance monitoring, and automated remediation.

### Prompt:
You are an expert DevOps engineer specializing in configuration management and compliance automation.

Generate configuration management automation for [INFRASTRUCTURE_ENVIRONMENT] including:

- Configuration Baseline: Define standard configurations for different server types and environments
- Drift Detection: Implement automated detection of configuration drift from baselines
- Compliance Monitoring: Monitor compliance with [COMPLIANCE_FRAMEWORKS] requirements
- Automated Remediation: Configure automatic remediation for common configuration issues
- Change Management: Implement controlled change processes with approval workflows
- Audit Logging: Comprehensive logging of all configuration changes and access
- Reporting: Generate compliance reports and configuration status dashboards

Requirements:
- Use configuration management tools with proper version control
- Implement real-time monitoring and alerting for configuration changes
- Configure role-based access control for configuration management
- Include backup and rollback capabilities for configuration changes
- Set up integration with ticketing systems for change tracking
- Implement automated testing for configuration changes
- Configure proper encryption for sensitive configuration data

Provide the complete configuration management framework with monitoring and reporting.

### Notes:
- Implement gradual rollout strategies for configuration changes to minimize risk.
- Use infrastructure as code principles for configuration management.
- Consider using policy engines for advanced compliance validation.

### Placeholders:
- **INFRASTRUCTURE_ENVIRONMENT**: Infrastructure environment (e.g., hybrid cloud, on-premises data center, Kubernetes platform)
- **COMPLIANCE_FRAMEWORKS**: Compliance frameworks (e.g., SOC 2, PCI DSS, HIPAA, CIS Benchmarks)

---

## 10. Generate Infrastructure Scaling Automation
**ID:** devops-infrastructure-scaling  
**Purpose:** Create intelligent infrastructure scaling automation with predictive scaling, cost optimization, and performance monitoring.

### Prompt:
You are an expert DevOps engineer specializing in infrastructure scaling and performance optimization.

Generate infrastructure scaling automation for [WORKLOAD_TYPE] including:

- Auto-Scaling Configuration: Configure horizontal and vertical scaling policies
- Predictive Scaling: Implement machine learning-based scaling predictions
- Resource Optimization: Optimize resource allocation based on actual usage patterns
- Cost-Aware Scaling: Balance performance requirements with cost constraints
- Performance Monitoring: Monitor scaling triggers and performance metrics
- Capacity Planning: Forecast future capacity requirements and costs
- Emergency Scaling: Implement rapid scaling for unexpected load spikes

Requirements:
- Configure multiple scaling metrics including CPU, memory, and custom metrics
- Implement proper cooling periods and scaling protection
- Set up integration with monitoring and alerting systems
- Include cost budgets and spending alerts for scaling operations
- Configure proper health checks and failover mechanisms
- Implement scaling event logging and audit trails
- Set up automated testing for scaling scenarios

Provide the complete scaling automation configuration with monitoring and cost controls.

### Notes:
- Test scaling policies thoroughly with load testing and chaos engineering.
- Implement proper safeguards to prevent runaway scaling costs.
- Consider using spot instances and preemptible instances for cost optimization.

### Placeholders:
- **WORKLOAD_TYPE**: Workload type (e.g., web application, batch processing, streaming data, machine learning)

---

## 11. Generate Infrastructure Security Automation
**ID:** devops-infrastructure-security  
**Purpose:** Create comprehensive infrastructure security automation with vulnerability scanning, compliance validation, and automated remediation.

### Prompt:
You are an expert DevOps engineer specializing in infrastructure security and automated compliance.

Generate infrastructure security automation for [SECURITY_SCOPE] including:

- Vulnerability Scanning: Automated scanning of infrastructure components and configurations
- Security Baseline: Define and enforce security baselines for different infrastructure types
- Compliance Validation: Automated validation against [SECURITY_STANDARDS] standards
- Access Control: Implement and monitor role-based access control and least privilege
- Threat Detection: Real-time detection of security threats and anomalies
- Incident Response: Automated response to security incidents and breaches
- Security Reporting: Comprehensive security dashboards and compliance reports

Requirements:
- Implement continuous security monitoring and alerting
- Configure automated patching with proper testing and rollback
- Set up integration with SIEM and security orchestration tools
- Include certificate management and rotation automation
- Configure network security monitoring and intrusion detection
- Implement proper audit logging and forensic capabilities
- Set up security training and awareness automation

Provide the complete security automation framework with monitoring and incident response.

### Notes:
- Implement defense in depth strategies with multiple security layers.
- Use infrastructure as code for consistent security configurations.
- Regularly update security automation based on emerging threats.

### Placeholders:
- **SECURITY_SCOPE**: Security scope (e.g., cloud infrastructure, Kubernetes cluster, hybrid environment, microservices platform)
- **SECURITY_STANDARDS**: Security standards (e.g., CIS Benchmarks, NIST Framework, ISO 27001, PCI DSS)

---

## 12. Generate Infrastructure Backup Automation
**ID:** devops-infrastructure-backup  
**Purpose:** Create comprehensive infrastructure backup automation with automated scheduling, verification, and disaster recovery capabilities.

### Prompt:
You are an expert DevOps engineer specializing in backup strategies and disaster recovery automation.

Generate infrastructure backup automation for [INFRASTRUCTURE_COMPONENTS] including:

- Backup Scheduling: Automated backup scheduling with different frequencies for different data types
- Backup Verification: Automated testing and verification of backup integrity
- Cross-Region Replication: Geographic distribution of backups for disaster recovery
- Retention Policies: Automated lifecycle management with compliance-based retention
- Recovery Testing: Regular automated testing of recovery procedures
- Monitoring and Alerting: Comprehensive monitoring of backup success and failures
- Documentation: Automated generation of recovery runbooks and procedures

Requirements:
- Implement incremental and differential backup strategies for efficiency
- Configure proper encryption for backups at rest and in transit
- Set up backup deduplication and compression for storage optimization
- Include metadata management and backup cataloging
- Configure proper access controls and audit logging for backup systems
- Implement backup performance monitoring and optimization
- Set up integration with disaster recovery orchestration tools

Provide the complete backup automation framework with recovery procedures and monitoring.

### Notes:
- Regularly test recovery procedures to ensure they work when needed.
- Implement proper backup monitoring to detect failures early.
- Consider using cloud-native backup services for improved reliability and cost efficiency.

### Placeholders:
- **INFRASTRUCTURE_COMPONENTS**: Infrastructure components to backup (e.g., databases, file systems, container volumes, configuration data)

---

## 13. Generate Infrastructure Monitoring and Observability
**ID:** devops-infrastructure-observability  
**Purpose:** Create comprehensive infrastructure monitoring and observability framework with metrics, logs, traces, and intelligent alerting.

### Prompt:
You are an expert DevOps engineer specializing in infrastructure observability and performance monitoring.

Generate infrastructure observability framework for [MONITORING_SCOPE] including:

- Metrics Collection: Comprehensive collection of infrastructure and application metrics
- Log Aggregation: Centralized logging with structured log processing and analysis
- Distributed Tracing: End-to-end request tracing across infrastructure components
- Synthetic Monitoring: Proactive monitoring with synthetic transactions and health checks
- Anomaly Detection: Machine learning-based detection of performance anomalies
- Alerting and Escalation: Intelligent alerting with proper escalation procedures
- Dashboards and Visualization: Comprehensive dashboards for different stakeholder needs

Requirements:
- Implement observability using OpenTelemetry standards for vendor neutrality
- Configure proper data retention and storage optimization strategies
- Set up correlation between metrics, logs, and traces for effective troubleshooting
- Include capacity planning and trend analysis capabilities
- Configure proper sampling and filtering to manage data volume and costs
- Implement automated incident response and escalation workflows
- Set up integration with business metrics and SLA monitoring

Provide the complete observability framework with configuration and deployment automation.

### Notes:
- Balance observability depth with cost and performance impact.
- Implement proper data governance and privacy controls for observability data.
- Use observability data for continuous improvement and optimization.

### Placeholders:
- **MONITORING_SCOPE**: Monitoring scope (e.g., Kubernetes cluster, microservices architecture, hybrid cloud infrastructure, edge computing platform)

---

## 14. Generate Infrastructure Cost Management Automation
**ID:** devops-infrastructure-cost-management  
**Purpose:** Create intelligent infrastructure cost management automation with optimization recommendations, budget controls, and financial reporting.

### Prompt:
You are an expert DevOps engineer specializing in cloud cost optimization and FinOps practices.

Generate infrastructure cost management automation for [COST_SCOPE] including:

- Cost Tracking: Real-time cost tracking with detailed resource attribution
- Budget Management: Automated budget monitoring with alerts and spending controls
- Optimization Recommendations: AI-powered recommendations for cost optimization
- Resource Rightsizing: Automated analysis and recommendations for resource optimization
- Lifecycle Management: Automated lifecycle policies for unused and idle resources
- Chargeback and Showback: Cost allocation and reporting for different business units
- Financial Forecasting: Predictive cost modeling and capacity planning

Requirements:
- Implement comprehensive tagging strategies for accurate cost allocation
- Configure automated policies for cost optimization and resource cleanup
- Set up integration with procurement and financial systems
- Include cost optimization workflows with approval and governance
- Configure proper cost anomaly detection and alerting
- Implement automated reporting with customizable dashboards
- Set up integration with reserved capacity and savings plan management

Provide the complete cost management framework with automation and reporting capabilities.

### Notes:
- Implement cost optimization as a continuous process, not a one-time activity.
- Balance cost optimization with performance and availability requirements.
- Use cost data to drive architectural and operational decisions.

### Placeholders:
- **COST_SCOPE**: Cost management scope (e.g., multi-cloud environment, Kubernetes platform, serverless applications, data processing pipelines)

---

## 15. Generate Infrastructure Disaster Recovery Automation
**ID:** devops-infrastructure-disaster-recovery  
**Purpose:** Create comprehensive disaster recovery automation with automated failover, data synchronization, and recovery orchestration.

### Prompt:
You are an expert DevOps engineer specializing in disaster recovery planning and business continuity automation.

Generate disaster recovery automation for [DR_SCOPE] including:

- Recovery Planning: Automated disaster recovery planning with RTO/RPO requirements
- Failover Automation: Automated failover procedures with health monitoring
- Data Synchronization: Real-time and batch data replication across regions
- Recovery Orchestration: Coordinated recovery of dependent services and systems
- Testing Automation: Regular disaster recovery testing with minimal business impact
- Communication Automation: Automated stakeholder communication during disasters
- Recovery Validation: Automated validation of recovered systems and data integrity

Requirements:
- Implement cross-region and cross-cloud disaster recovery capabilities
- Configure automated health checks and failover triggers
- Set up proper data consistency and integrity validation
- Include automated rollback capabilities for failed recovery attempts
- Configure proper monitoring and alerting during disaster scenarios
- Implement automated capacity scaling for disaster recovery environments
- Set up integration with business continuity and crisis management systems

Provide the complete disaster recovery automation with testing and validation procedures.

### Notes:
- Regular testing is essential to ensure disaster recovery procedures work when needed.
- Consider cascading failure scenarios and implement proper isolation mechanisms.
- Document clear escalation procedures and communication plans.

### Placeholders:
- **DR_SCOPE**: Disaster recovery scope (e.g., critical business applications, entire data center, multi-cloud platform, edge computing infrastructure)