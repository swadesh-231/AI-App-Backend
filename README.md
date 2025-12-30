# Lovable Clone - AI-Powered Full-Stack Application Generator

> **Note:** This project is a clone of the "Lovable" platform, designed to generate, execute, and preview full-stack web applications using LLMs, RAG, and sandboxed execution environments.

## 📖 Overview

This project is an advanced AI coding assistant that allows users to generate web applications through natural language prompts. It features a microservices architecture that handles real-time code generation, file management, and live previews of generated applications within isolated environments.

 The system utilizes **Spring Cloud**, **Kubernetes**, and **Vector Search (RAG)** to provide accurate context-aware code generation.

---

## 🏗️ System Architecture

The system is built on a scalable microservices architecture orchestrated via Kubernetes.

### Core Workflow
1.  **User Interaction:** Users interact via a chat interface, sending prompts to the server.
2.  [cite_start]**Gateway:** A **Spring Cloud API Gateway** routes requests to specific services[cite: 14].
3.  **Intelligence Service:** Orchestrates the LLM interaction. [cite_start]It utilizes **RAG (Retrieval-Augmented Generation)** by querying a **Qdrant Vector DB** to retrieve relevant codebase context[cite: 18, 39, 40].
4.  **Code Generation:** The LLM generates code, which is chunked, embedded, and stored. [cite_start]Generated files (e.g., `index.html`) are buffered and stored in **MinIO**[cite: 46, 47].
5.  **Execution & Preview:**
    * [cite_start]The **Execution Service** provisions a new namespace/pod in **Kubernetes**[cite: 10, 50].
    * [cite_start]Code is executed in a **Micro VM/Independent Pod** or **WebContainer** environment[cite: 26, 36].
    * [cite_start]Users receive a live **Preview URL** to interact with their generated app[cite: 11].
6.  [cite_start]**Streaming:** Content and logs are streamed back to the user via **SSE (Server-Sent Events)**[cite: 15].

---

## ✨ Key Features

### 🤖 AI & Code Generation
* **Natural Language to Code:** Generate full-stack React/Node applications from simple prompts.
* [cite_start]**Context-Aware RAG:** Uses **Qdrant Vector DB** to store and retrieve codebase context for accurate generation[cite: 39].
* [cite_start]**Streaming Chat:** Real-time chat stream with the AI, including retry mechanisms for failed requests[cite: 65, 66].
* [cite_start]**Session Management:** Save and load full chat history (last 10 messages memory)[cite: 20, 64].

### 🛠️ Project & File Management
* [cite_start]**Project Operations:** Create, list, and manage multiple projects[cite: 55].
* [cite_start]**File System Access:** View file trees, get file metadata, and read file content[cite: 68, 69].
* [cite_start]**Export:** Download all project files as a `.zip` archive[cite: 70].

### 🚀 Execution & Preview
* [cite_start]**Live Preview:** Instantly preview generated applications via a unique URL[cite: 72].
* [cite_start]**Sandboxed Environment:** Secure execution using Kubernetes and Micro VMs[cite: 36].
* [cite_start]**Logs Streaming:** Real-time log streaming from the execution container to the client[cite: 73].

### 🔐 Auth & Monetization
* [cite_start]**Authentication:** Secure Login, Sign Up, and Profile management[cite: 58, 59].
* [cite_start]**Subscription Plans:** Tiered access (FREE vs. PRO)[cite: 79].
* [cite_start]**Quota Management:** Limits on token usage and running previews[cite: 80].
* [cite_start]**Payments:** Integration with **Stripe**[cite: 77].

---

## 💻 Tech Stack

### Backend & Infrastructure
* **Spring Cloud Gateway:** API Gateway.
* **Microservices:** Intelligence Service, Chat Service, Workspace Service, Execution Service.
* **Database:** PostgreSQL (Relational data), Qdrant (Vector DB).
* **Storage:** MinIO (Object storage for generated files).
* **Orchestration:** Kubernetes (K8s).
* [cite_start]**Observability:** Zipkin Tracing[cite: 82].
* [cite_start]**Caching/Rate Limiting:** Redis[cite: 81].

### Frontend (Generated Apps)
* [cite_start]**Framework:** React[cite: 30].
* [cite_start]**Bundler:** Vite[cite: 32].
* **Styling:** CSS/Tailwind.

---

## 🗄️ Database Schema

The project uses a relational schema to manage users and projects, alongside a Vector DB for AI context.
* **Users:** Handles authentication and plan details.
* **Projects:** Links users to their generated applications.
* **Chats/Messages:** Stores conversation history with the LLM.
* **Files:** Metadata for generated code files.

---

## 🚀 Getting Started

### Prerequisites
* Docker & Kubernetes Cluster (Minikube or Cloud Provider)
* Java JDK 17+ (for Spring Boot services)
* Node.js (for frontend/execution service)
* MinIO & Qdrant instances

### Installation

1.  **Clone the repository**
    ```bash
    git clone [https://github.com/yourusername/lovable-clone.git](https://github.com/yourusername/lovable-clone.git)
    cd lovable-clone
    ```

2.  **Start Infrastructure (Docker Compose)**
    ```bash
    docker-compose up -d postgres qdrant minio redis zipkin
    ```

3.  **Deploy Microservices**
    * Navigate to each service directory (`intelligence-service`, `chat-service`, etc.) and run:
    ```bash
    ./mvnw spring-boot:run
    ```

4.  **Start the Frontend**
    ```bash
    cd frontend
    npm install
    npm run dev
    ```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:
1.  Fork the project.
2.  Create your feature branch (`git checkout -b feature/AmazingFeature`).
3.  Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4.  Push to the branch (`git push origin feature/AmazingFeature`).
5.  Open a Pull Request.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.
