# Product Requirements Document (PRD)
## Project Name: National Multi-Agent System (MAS) for ERPNext & Frappe

### 1. Executive Summary
This document outlines the product requirements for a massive-scale, highly secure Multi-Agent System (MAS) built on top of the Frappe framework and ERPNext (Version 16). The objective is to connect and integrate various state departments, ministries, and institutions. Rather than manually building every specific integration and feature, the system will leverage a network of autonomous, specialized AI Agents. These agents will possess deep reasoning capabilities, maintain state/memory, execute real-time operations, and orchestrate sub-agents to achieve complex, long-running tasks.

### 2. Vision and Goals
- **National Knowledge Graph:** Create a comprehensive, real-time Knowledge Base that links all state entities, providing immediate insights for decision-makers.
- **Autonomous Operations:** Utilize specialized agents to customize, maintain, and interact with the ERP systems with minimal human intervention.
- **Security & Privacy First:** Ensure strict data confidentiality with the flexibility to use both open-source local LLMs (to keep data on-premise) and closed-source cloud LLMs based on security clearance and task requirements.
- **Modularity:** Ensure a decoupled architecture where agents act as independent applications/services communicating seamlessly with Frappe sites.

### 3. Architecture & Technology Stack
- **Core Frameworks:** Frappe Framework v16, ERPNext v16, and other official or custom Frappe modules.
- **Agent Orchestration:** **LangGraph** (preferred over standard LangChain for its robust state management, cyclic graphs, and multi-actor coordination capabilities required for MAS).
- **Vector Database (Knowledge Base):** **Weaviate** or **ChromaDB**. Weaviate is highly recommended for enterprise-grade scalability, advanced RBAC (Role-Based Access Control), and handling the massive scale of a national knowledge base.
- **Infrastructure:**
  - Independent repositories and distinct standalone services for each major Agent.
  - Inter-agent communication protocols (REST APIs, Webhooks, or message brokers like Redis/RabbitMQ).
  - Frappe API integrations and direct function calls where APIs fall short.
- **LLM Support:** Agnostic design supporting closed models (e.g., GPT-4, Claude, Gemini) and local open-source models (e.g., LLaMA-3 via vLLM/Ollama).

### 4. Core AI Agents

#### 4.1. The Developer Agent (The Backbone)
- **Role:** The highest-privileged technical agent responsible for system configuration, customization, and deployment.
- **Capabilities:**
  - **Environment Control:** Can create new Frappe sites, install applications, and develop custom apps for specific institutions.
  - **Intelligent Q&A:** Analyzes requirements and autonomously modifies ERPNext configurations or code to meet them.
  - **Deep Thinking & Persistence:** Possesses the concept of an "Objective." It does not stop until the task is fully completed, even if it requires running continuously for weeks.
  - **Sub-Agent Delegation:** Can spawn specialized sub-agents (e.g., a Database Schema Agent, a Frontend Agent) to divide and conquer complex tasks.
  - **Workflow (Crucial):** Operates strictly in a **Staging Environment**. Once modifications are complete, it generates a comprehensive review link/report for a Human Supervisor/Developer. Upon human approval, it deploys to the **Production Environment** and generates a final official report with all associated links.
  - **Isolation:** Can interact with all other agents, but no other agent can access or influence the Developer Agent.

#### 4.2. The Expert Agent (Consultant)
- **Role:** A senior-level consultant operating at the institutional or ministerial level.
- **Capabilities:**
  - **Deep System Access:** Has comprehensive access to system modules (HR, Accounting, Custom Apps, etc.) via Frappe APIs.
  - **Advisory:** Analyzes departmental data to provide strategic insights, identify inefficiencies, and suggest improvements.
  - **Interface:** Accessible via a dedicated Telegram Bot (similar to Hermes agent features) and native Frappe UI dashboards.
  - **Memory:** Utilizes long-term and short-term memory to maintain context of ongoing institutional strategies and past consultations.

#### 4.3. The Public Agent (Customer Service)
- **Role:** The citizen-facing interface handling inquiries, complaints, and general information.
- **Capabilities:**
  - **Interface:** Primarily accessed via a dedicated Telegram Bot for each specific institution, ensuring wide public accessibility.
  - **RAG Implementation:** Uses advanced Retrieval-Augmented Generation (RAG) to fetch accurate, public-facing information from the Knowledge Base.
  - **Escalation:** Capable of filtering and routing complex or highly sensitive issues to human operators or the Expert Agent.

#### 4.4. The Decision-Maker Agent
- **Role:** Strategic entity for top-level government officials.
- **Capabilities:**
  - **Global Insights:** Aggregates real-time data from the centralized/decentralized National Knowledge Base.
  - **Scenario Analysis:** Can simulate outcomes based on data points from multiple ministries.

#### 4.5. The Security & Compliance Agent
- **Role:** The system's internal auditor and security watchdog.
- **Capabilities:**
  - **Code & Action Review:** Automatically audits every change proposed by the Developer Agent in the staging environment before human review.
  - **Regulatory Compliance:** Ensures all data handling, modifications, and integrations strictly adhere to the state's cyber security laws, privacy regulations, and compliance frameworks.
  - **Anomaly Detection:** Continuously monitors all inter-agent communications and system logs to identify unauthorized access attempts or suspicious activities.

#### 4.6. The Data Analyst / BI Agent (Strategic Analyst)
- **Role:** Dedicated Business Intelligence and data specialist for ministers and top-tier decision-makers.
- **Capabilities:**
  - **Cross-Institutional Reporting:** Connects disparate data points across various ministries via the National Knowledge Base to generate comprehensive, holistic strategic reports.
  - **Advanced Visualizations:** Autonomously generates interactive charts, dashboards, and projections without requiring the user to open individual ERP modules.
  - **Predictive Analytics:** Identifies trends across government sectors to forecast potential economic or operational challenges.

### 5. System Features & Requirements

#### 5.1. Agent Capabilities (Universal)
- **Skill Creation & Utilization:** Agents can dynamically generate and utilize "Tools" or "Skills" (similar to MCPs - Model Context Protocols) to interact with new modules or external APIs.
- **Memory Systems:** Implementation of robust short-term (contextual) and long-term (vectorized) memory.
- **Multimodal Abilities:** Voice model integrations for voice-based interactions (especially for the Public and Expert agents).

#### 5.2. Inter-Agent Communication & Delegation
- A structured protocol allowing agents to pass contextual data, request assistance, and form ad-hoc task forces (e.g., Developer Agent asking Expert Agent for module specifications).

#### 5.3. Security & Access Control
- Absolute isolation of the Developer Agent's operational scope.
- Strict Role-Based Access Control (RBAC) on the Vector Database to ensure agents only retrieve data they are authorized to see.
- Audit logs for every action taken by an AI agent, especially system modifications.

### 6. User Interface (UI) Integration
- Custom Frappe workspaces designed to visualize Agent activity, displaying real-time reasoning processes, task queues, and human-in-the-loop approval requests (specifically for Staging-to-Production pipelines).
- Integration of modern, dynamic chat interfaces within ERPNext (inspired by seamless Claude/Gemini ERP integrations), allowing context-aware conversations based on the active screen/module the user is viewing.

### 7. Future Phases & Research Areas
- Implementing advanced self-reflection and self-correction loops within LangGraph to minimize hallucination in critical government data.
- Exploring decentralized Vector DB architecture (e.g., each ministry hosts its own Weaviate instance, queried by a federated Agent).

---
*End of PRD*
