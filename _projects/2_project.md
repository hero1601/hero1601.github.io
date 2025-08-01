---
layout: page
title: Food Delivery
description: Real-time, containerized food delivery system built during OpenSoft at IIT Kharagpur.
img: assets/img/FD.png
importance: 1
category: work
---

As the **Project Lead** of a food delivery platform developed during **OpenSoft 2022 at IIT Kharagpur**, I coordinated a team of **20+ developers** working across multiple microservices — including authentication, orders, notifications, payments, metadata, management, and frontend.

In addition to my leadership role, I was **personally responsible** for designing and building the **Delivery Microservice**, which managed real-time delivery agent assignment, live tracking, and communication with the Orders and Notification services. The system handled over **500+ active users** and was built for real-time performance and modular scalability.

---

### Project Overview

- **Collaborative Architecture** — Multiple teams developed dedicated microservices such as Authentication, Orders, Notifications, Payments, Metadata, Management, and Frontend under a unified event-driven architecture.
- **Scalable Microservices** — Each service was independently developed and deployed, enabling modular scalability and parallel development.
- **Dockerized Deployment** — All microservices were containerized using Docker to ensure fast setup, consistent environments, and seamless CI/CD integration.
- **Real-Time Data Flow** — Kafka and Redis powered event streaming and low-latency queries, enabling timely updates and smooth inter-service communication.
- **Intelligent Workflow** — Business logic such as dynamic agent assignment, payment processing, and notifications were implemented within respective services for clean separation of concerns.

---

### Architecture Overview

The platform followed a modular, microservice-based design with clean interfaces between services. Each team worked independently but adhered to shared API contracts.

- **Authentication Service** — Manages user login, registration, and secure access control.
- **Orders Service** — Handles order creation, updates, and status tracking.
- **Delivery Service** — Assigns delivery agents, manages live tracking, and coordinates with Orders and Notifications.
- **Notification Service** — Sends real-time alerts and updates to customers and delivery agents via multiple channels.
- **Payments Service** — Processes transactions, refunds, and payment verification.
- **Metadata Service** — Maintains static and dynamic data such as restaurant info, menus, and location segments.
- **Management Service** — Provides administrative tools and monitoring dashboards for overall platform health.
- **Frontend** — Offers the user interface with live updates, order tracking, and agent location visualization

---

### Real-Time Workflow

1. Authentication Service verifies user sign-in.
2. Orders Service creates order and notifies Delivery Service.
3. Delivery Service assigns agent with least recent delivery.
4. Notification Service alerts assigned agent.
5. Delivery Service pushes status updates to Kafka.
6. Backend sends real-time status to frontend via WebSocket.
7. Delivery Service notifies Orders Service when delivery is complete.

---

### My Contributions

- Designed & implemented the **Delivery Microservice** from scratch
- Built REST APIs (`/delivery`, `/newdelivery`) using **Flask**
- **Containerized** the service using **Docker** — reduced deployment time by 80%
- Developed agent-assignment logic with queue-based fairness
- Integrated with Kafka and Redis for **event-based coordination**
- Led daily standups, handled cross-group coordination, and reviewed PRs

#### API Endpoints

| Endpoint          | Description                                      |
|-------------------|--------------------------------------------------|
| `POST /delivery`  | Add a new delivery agent                         |
| `GET /delivery/{id}` | Fetch latest assigned order for agent         |
| `PUT /delivery/{id}` | Mark delivery as complete + notify Orders MS  |
| `POST /newdelivery` | Triggered by Orders MS; assigns best-fit agent |

---

### Tech Stack

| Component        | Technology                          |
|------------------|-------------------------------------|
| API Framework    | Flask (Python)                      |
| Containerization | Docker                              |
| Event Streaming  | Apache Kafka                        |
| Real-time Cache  | Redis                               |
| Frontend         | Javascript                          |

---

### Impact

- Deployed a real-time system with **500+ users** during OpenSoft
- Cut deployment setup time by **80%** via Dockerized services
- Enabled seamless coordination between 7+ services and a unified frontend
- Built a production-grade backend for real-time delivery management

---

### Key Takeaways

- Microservice teams can **scale independently** with shared contracts
- Containerization is key for fast iteration in hackathons or production
- **Leadership under tight deadlines** requires both technical and people skills
