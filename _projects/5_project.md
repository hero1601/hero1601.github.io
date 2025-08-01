---
layout: page
title: Healthcare IT
description: Terminology management API for healthcare data, featuring gRPC acceleration and robust SQL backbone.
img: assets/img/healthcare-it.jpg
importance: 1
category: fun
---

This project is a **Healthcare IT Terminology Service** designed to provide fast, efficient, and standards-compliant access to healthcare coding systems (SNOMED, ICD, etc.), essential for modern healthcare applications. The service is built on a **three-layer architecture** to ensure scalability and maintainability.

The solution leverages:
- **MS SQL Server** as the backend, providing durable medical term storage and queries.
- **C#** for the business logic and server APIs.
- **gRPC** for performant, binary-serialization-based communication between service clients and backend.
- **Dapper** for high-efficiency object-relational mapping within the C# backend.

[🔗 View the code on GitHub](https://github.com/hero1601/Healthcare-IT)

---

### Project Goals

- Offer a reusable, modular terminology service for healthcare data integration.
- Provide **low-latency APIs** for querying and managing standard terminologies.
- Ensure high throughput and scalability for enterprise deployments.
- Simplify back-end integration for EHR (Electronic Health Records) and clinical applications.

---

### System Architecture

- **Presentation Layer:**  
  gRPC exposes a strongly-typed, high-efficiency API surface using Protocol Buffers for compact, binary serialization. This enables fast, low-latency communication between clients and the backend, making it ideal for performance-sensitive healthcare applications.

- **Application Layer:**  
  Implemented in C#, this layer manages business logic, request validation, and query orchestration. It acts as the intermediary that processes incoming requests and coordinates access to data repositories, ensuring modularity and maintainability.

- **Data Layer:**  
  SQL Server hosts a normalized schema of healthcare terminology concepts, supporting complex hierarchies and mappings. Dapper ORM is used for high-performance data access, efficiently translating SQL query results into C# models with minimal overhead.

---

### Implementation Details

- **gRPC APIs:** Enables lightweight, binary-serialized communications, minimizing latency for high-frequency use cases.
- **Dapper ORM:** Selected for its performance in mapping query results directly to C# models, outperforming heavier ORMs in read-intensive health data scenarios.
- **SQL Server Schema:** Carefully normalized to handle medical coding hierarchies and cross-mappings.
- **Security:** Designed with secure authentication endpoints and validation checks suitable for healthcare use.

---

### Challenges & Solutions

- **Performance:** Adopted gRPC for all major API surfaces, cutting serialization/deserialization overhead versus REST/JSON.
- **Scalability:** Three-tier separation allowed for horizontal scaling of the API server while offloading queries to SQL.
- **Data Mapping:** Used Dapper to eliminate bottlenecks of traditional ORMs when working with large medical vocabularies.
- **Extensibility:** Modular C# codebase makes it easy to plug in new terminology sets or switch out underlying database engines if required.

---

### Key Takeaways

- Combining **gRPC** and **Dapper** achieves modern cloud-ready data performance for healthcare IT workloads.
- Three-layer architecture enforces clean separation of presentation, business, and data access responsibilities.
- Efficient terminology management is essential for rapid development and regulatory compliance in healthcare software.
- Leveraging open protocols and lightweight libraries creates IT solutions that are both powerful and maintainable.

---