# Prompt Library

A centralized, open-source collection of expertly crafted prompts for AI-assisted software development. This library is designed to boost productivity, maintain consistency, and provide ready-to-use prompts tailored for popular technology domains and common development tasks.

> **Use with:** GitHub Copilot, ChatGPT, Claude, Cursor, and other LLM-powered coding assistants.

---

##  Table of Contents

- [Overview](#-overview)
- [Getting Started](#-getting-started)
- [Library Structure](#-library-structure)
- [Available Domains](#-available-domains)
  - [Android Development](#-android-development)
  - [Backend API Development](#-backend-api-development)
  - [Data Analytics](#-data-analytics)
  - [DevOps & Infrastructure](#-devops--infrastructure)
  - [iOS Development](#-ios-development)
  - [Java Development](#-java-development)
  - [Node.js Development](#-nodejs-development)
  - [Python & SQL](#-python--sql)
  - [React Development](#-react-development)
- [Prompt Categories](#-prompt-categories)
- [How to Use](#-how-to-use)
- [Customizing Prompts](#-customizing-prompts)
- [Contributing](#-contributing)
- [License](#-license)

---

##  Overview

This Prompt Library provides **production-ready prompts** organized by technology stack and use case. Each prompt is designed to:

-  Generate high-quality, maintainable code
-  Follow industry best practices and design patterns
-  Be customizable through placeholder variables `[VARIABLE_NAME]`
-  Include context, purpose, and usage notes

Whether you're scaffolding a new feature, debugging complex issues, writing documentation, or generating unit tests—this library has you covered.

---

##  Getting Started

1. **Browse** the library by technology domain or use case
2. **Select** a prompt that matches your task
3. **Customize** placeholder variables (e.g., `[COMPONENT_NAME]`, `[API_ENDPOINT]`)
4. **Paste** into your preferred AI assistant
5. **Iterate** on the generated output as needed

---

##  Library Structure

Each technology domain follows a consistent folder structure:

```
Domain_Library/
├── Code_Generation/           # Prompts for generating new code
├── Debugging_and_Explanation/ # Prompts for debugging and code analysis
├── Documentation/             # Prompts for generating documentation
├── Refactoring_and_Optimisation/ # Prompts for improving existing code
└── Unit_Test_Generation/      # Prompts for creating tests
```

Some domains include additional specialized categories based on their unique needs.

---

##  Available Domains

###  Android Development
**Path:** `Android_Library/`

Prompts for modern Android development using Kotlin, Jetpack Compose, Room, Hilt, and MVI architecture.

| Category | Description |
|----------|-------------|
| Code Generation | Compose components, Room entities, ViewModels, Retrofit services |
| Debugging | Crash analysis, performance profiling, memory leaks |
| Documentation | KDoc generation, architecture documentation |
| Refactoring | Code modernization, architecture migration |
| Unit Tests | JUnit tests, Compose UI tests |

---

###  Backend API Development
**Path:** `Backend_API_Library/`

Prompts for building robust RESTful and GraphQL APIs across multiple languages and frameworks.

| Category | Description |
|----------|-------------|
| Code Generation | CRUD endpoints, controllers, schemas, OpenAPI specs |
| Debugging | API error analysis, performance bottlenecks |
| Documentation | API documentation, endpoint specifications |
| Refactoring | API versioning, code optimization |
| Unit Tests | Integration tests, mock services |

---

###  Data Analytics
**Path:** `Data_Analytics_Library/`

Prompts for data engineering, analytics, and business intelligence workflows.

| Category | Description |
|----------|-------------|
| Code Generation | ETL pipelines, data extraction, transformations, visualizations |
| Debugging | Data quality issues, pipeline failures |
| Documentation | Data dictionaries, pipeline documentation |
| Refactoring | Query optimization, pipeline improvements |
| Unit Tests | Data validation tests, pipeline tests |

---

###  DevOps & Infrastructure
**Path:** `DevOps_Library/`

Comprehensive prompts for CI/CD, infrastructure automation, and DevOps practices.

| Category | Description |
|----------|-------------|
| Code Generation | IaC templates, deployment scripts, configuration |
| CI/CD Pipeline Management | Pipeline design, automation workflows |
| Infrastructure Automation (IaC) | Terraform, CloudFormation, Ansible |
| Debugging | Pipeline failures, infrastructure issues |
| Documentation | Runbooks, infrastructure documentation |
| Refactoring | Pipeline optimization, security hardening |
| Unit Tests | Infrastructure tests, pipeline validation |

---

###  iOS Development
**Path:** `iOS_Library/`

Prompts for iOS development using Swift, VIPER architecture, and Apple frameworks.

| Category | Description |
|----------|-------------|
| Code Generation | VIPER modules, services, UI components |
| Debugging | Crash analysis, memory profiling |
| Documentation | Swift documentation, architecture guides |
| Refactoring | Architecture improvements, Swift modernization |
| Unit Tests | XCTest, UI tests |

---

###  Java Development
**Path:** `Java_Developers_Library/`

Prompts for Java enterprise development with Spring Boot, Kafka, and reactive programming.

| Category | Description |
|----------|-------------|
| Code Generation | Spring Boot projects, Kafka integration, REST APIs |
| Debugging | Exception handling, reactive debugging |
| Documentation | Javadoc, architecture documentation |
| Refactoring | Code modernization, pattern implementation |
| Unit Tests | JUnit, Mockito tests |

---

###  Node.js Development
**Path:** `NodeJS_Library/`

Prompts for Node.js and Express.js development with TypeScript, MongoDB, and modern patterns.

| Category | Description |
|----------|-------------|
| Code Generation | Express routers, Mongoose schemas, services, middleware |
| Debugging | Async debugging, memory leaks, performance |
| Documentation | JSDoc, API documentation |
| Refactoring | TypeScript migration, architecture improvements |
| Unit Tests | Jest tests, integration tests |

---

###  Python & SQL
**Path:** `Python_SQL_Library/`

Prompts for Python development and SQL database operations.

| Category | Description |
|----------|-------------|
| Code Generation | Python scripts, SQL queries, data processing |
| Debugging | Python debugging, SQL optimization |
| Documentation | Docstrings, database documentation |
| Refactoring | Code optimization, query improvements |
| Unit Tests | pytest, database tests |

---

###  React Development
**Path:** `React_Prompt_Library/`

Prompts for React application development with hooks, state management, and modern patterns.

| Category | Description |
|----------|-------------|
| Code Generation | Components, hooks, Zustand stores, API integration |
| Debugging | React debugging, performance issues |
| Documentation | Component documentation, Storybook |
| Refactoring | Hook migration, component optimization |
| Unit Tests | Jest, React Testing Library |

---

##  Prompt Categories

Each domain includes these standard categories:

| Category | Purpose |
|----------|---------|
| **Code Generation** | Create new code, features, and components |
| **Debugging & Explanation** | Analyze issues, understand code behavior |
| **Documentation** | Generate docs, comments, and guides |
| **Refactoring & Optimization** | Improve code quality and performance |
| **Unit Test Generation** | Create comprehensive test suites |

---

##  How to Use

### Basic Usage

1. Navigate to the relevant domain folder
2. Open the `.md` file for your use case
3. Find a prompt that matches your needs
4. Replace placeholder variables with your specific values

### Placeholder Variables

Prompts use `[PLACEHOLDER]` syntax for customization:

```
Generate a React component named [COMPONENT_NAME] that displays [DATA_TYPE] data...
```

Replace with your values:

```
Generate a React component named UserProfile that displays user account data...
```

### Example Workflow

**Task:** Create a new Express.js API endpoint

1. Go to `NodeJS_Library/Code_Generation/`
2. Open `NodeJS_Code_Generation_Prompts.md`
3. Find "Generate a Full CRUD Express.js Router"
4. Replace `[RESOURCE_NAME]` with `products`
5. Replace field placeholders with your schema fields
6. Paste into your AI assistant

---

##  Customizing Prompts

Prompts are designed to be adapted to your needs:

- **Add context:** Include your project's architecture, conventions, or constraints
- **Specify technology:** Replace generic references with your specific stack
- **Adjust scope:** Request more or fewer features based on your needs
- **Include examples:** Add sample code or data for better results

---

## Contributing

We welcome contributions! Here's how to help:

1. **Fork** the repository
2. **Create** a new branch for your changes
3. **Add** or improve prompts following the existing format
4. **Test** your prompts with AI assistants
5. **Submit** a pull request

### Prompt Guidelines

- Include a clear **Purpose** statement
- Provide **Usage Notes** with tips
- Use consistent `[PLACEHOLDER]` naming
- Follow the existing markdown structure
- Keep prompts focused and actionable

---

##  License

This project is open source and available under the [MIT License](LICENSE).

---

## > Quick Links

| Domain | Code Gen | Debug | Docs | Refactor | Tests |
|--------|----------|-------|------|----------|-------|
| Android | [→](Android_Library/Code_Generation/) | [→](Android_Library/Debugging_and_Explanation/) | [→](Android_Library/Documentation/) | [→](Android_Library/Refactoring_and_Optimisation/) | [→](Android_Library/Unit_Test_Generation/) |
| Backend API | [→](Backend_API_Library/Code_Generation/) | [→](Backend_API_Library/Debugging_and_Explanation/) | [→](Backend_API_Library/Documentation/) | [→](Backend_API_Library/Refactoring_and_Optimisation/) | [→](Backend_API_Library/Unit_Test_Generation/) |
| Data Analytics | [→](Data_Analytics_Library/Code_Generation/) | [→](Data_Analytics_Library/Debugging_and_Explanation/) | [→](Data_Analytics_Library/Documentation/) | [→](Data_Analytics_Library/Refactoring_and_Optimisation/) | [→](Data_Analytics_Library/Unit_Test_Generation/) |
| DevOps | [→](DevOps_Library/Code_Generation/) | [→](DevOps_Library/Debugging_and_Explanation/) | [→](DevOps_Library/Documentation/) | [→](DevOps_Library/Refactoring_and_Optimisation/) | [→](DevOps_Library/Unit_Test_Generation/) |
| iOS | [→](iOS_Library/Code_Generation/) | [→](iOS_Library/Debugging_and_Explanation/) | [→](iOS_Library/Documentation/) | [→](iOS_Library/Refactoring_and_Optimisation/) | [→](iOS_Library/Unit_Test_Generation/) |
| Java | [→](Java_Developers_Library/Code_Generation/) | [→](Java_Developers_Library/Debugging_and_Explanation/) | [→](Java_Developers_Library/Documentation/) | [→](Java_Developers_Library/Refactoring_and_Optimisation/) | [→](Java_Developers_Library/Unit_Test_Generation/) |
| Node.js | [→](NodeJS_Library/Code_Generation/) | [→](NodeJS_Library/Debugging_and_Explanation/) | [→](NodeJS_Library/Documentation/) | [→](NodeJS_Library/Refactoring_and_Optimisation/) | [→](NodeJS_Library/Unit_Test_Generation/) |
| Python/SQL | [→](Python_SQL_Library/Code_Generation/) | [→](Python_SQL_Library/Debugging_and_Explanation/) | [→](Python_SQL_Library/Documentation/) | [→](Python_SQL_Library/Refactoring_and_Optimisation/) | [→](Python_SQL_Library/Unit_Test_Generation/) |
| React | [→](React_Prompt_Library/Code_Generation/) | [→](React_Prompt_Library/Debugging_and_Explanation/) | [→](React_Prompt_Library/Documentation/) | [→](React_Prompt_Library/Refactoring_and_Optimisation/) | [→](React_Prompt_Library/Unit_Test_Generation/) |

---

<p align="center">
  <strong>Happy Prompting! 🎉</strong>
</p>
