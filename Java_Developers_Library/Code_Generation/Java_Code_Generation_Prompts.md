# Prompts Library

## Generate a Spring Boot Project Structure
### Use Case  
Generate a complete Spring Boot project structure with Maven including basic configurations.

### Prompt  
Create a Spring Boot Maven project with the following modules:  
- `api`: for controllers  
- `service`: for business logic  
- `repository`: for JPA repository interfaces  
- `model`: for domain entities  
Include `application.properties` with an H2 database configuration.

---

## Create a Centralized Error Handler for a Spring Boot Application
### Use Case  
Create a centralized error handler for a Spring Boot application.

### Prompt  
Create a `@ControllerAdvice` class with `@ExceptionHandler` methods for handling:  
- `IllegalArgumentException`  
- `ResourceNotFoundException`  

Return custom error response objects.

---

## Create a Kafka Producer and Consumer in a Spring Boot Application
### Use Case  
Set up Kafka integration with a producer and a consumer in Spring Boot.

### Prompt  
Create a Spring Boot Kafka producer that sends `OrderEvent` messages to the topic `order-created`.  
Also, create a Kafka consumer that listens to the same topic and logs the order ID.

---

## Error Handling in Java Reactive Programming
### Use Case  
Handle errors in a reactive method using the `Mono` pipeline in Java.

### Prompt  
Handle errors in this reactive method using `Mono` pipeline in Java. Add error logging and retry logic using:  
- `doOnError`  
- `retryWhen` (limit to 3 retries with exponential backoff)  
Use `onErrorResume` to handle errors gracefully.

---

## Create a New Java Class Using JSON Payload
### Use Case  
Create a new Java class using a JSON payload.

### Prompt  
Create a Java class for `CustomerNotificationPayload` with the following string fields:  
- `metadata`  
- `schedule`  
- `url`  

The new Java class should construct `CustomerNotificationPayload` using the String Builder pattern.  
Ensure the class follows a structured approach, adhering to best practices in Java 17 with clear documentation.

---

## Generate Java Code for a Given DB Query (MongoDB Query or SQL)
### Use Case  
Generate Java code for a given DB query (MongoDB query or SQL).

### Prompt  
Given a Java class based on the MongoDB aggregation query:  
- Collect the result set data using Java streams and write it to a `Map` based on the key-value pair.  
- Identify the unique IDs and dump all the matching values into a list object.  
- Invoke this Java class using a controller and expose it as a REST API.