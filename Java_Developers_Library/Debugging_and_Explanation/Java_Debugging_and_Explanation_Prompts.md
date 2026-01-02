# Troubleshooting and Optimization Prompts

## Troubleshoot an Error
### Use Case  
Analyze the provided Java exception error log to identify root causes and suggest best practices for resolution.

### Prompt  
Ensure the analysis includes:  
- A breakdown of key error messages and stack traces  
- Possible causes, including code issues, configuration errors, or dependency conflicts  
- Recommended best practices to fix and prevent similar issues in the future  

Please paste the error log below for detailed analysis.

---

## Identify Performance Bottleneck
### Use Case  
Analyze any performance bottlenecks in a Java method and suggest optimizations.

### Prompt  
Identify and analyze performance bottlenecks in the highlighted Java method, explaining their root causes.  
Provide specific optimizations to improve efficiency, including potential improvements in:  
- Algorithm choice  
- Memory usage  
- Execution speed  

---

## Spring Boot Startup Issue
### Use Case  
Identify causes for a Spring Boot application termination right after startup.

### Prompt  
Analyze why the Spring Boot application terminates immediately after startup.  
Identify potential causes such as:  
- Missing dependencies  
- Configuration errors  
- Memory constraints  
- Unhandled exceptions  

Provide debugging strategies to resolve the issue.

---

## Spring Bean Creation Failures
### Use Case  
Troubleshoot the `BeanCreationException` error that occurs during application startup.

### Prompt  
Investigate the causes of the `BeanCreationException` occurring during Spring Boot application startup.  
Identify potential issues such as:  
- Misconfigurations  
- Missing dependencies  
- Circular dependencies  
- Incorrect bean definitions  
