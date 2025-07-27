
# Money Lens Agent
---

## Quickstart: Setup & Run

### Prerequisites
- Python 3.9+ (for backend)
- Node.js 18+ and npm (for frontend)
- (Optional) Google API keys and MCP server credentials for production use

---

### Backend Setup (fi-mcp-client/)
1. **Install dependencies:**
   ```bash
   cd fi-mcp-client
   pip install -r requirements.txt
   ```
2. **Configure environment:**
   - Copy `.env.example` to `.env` and fill in required values (API keys, secrets, etc).
3. **Run the API server:**
   ```bash
   python api_server_new.py
   # or for legacy: python api_server.py
   ```
   - The server will start on `http://localhost:8001` by default.

---

### Frontend Setup (shadcn-ui/)
1. **Install dependencies:**
   ```bash
   cd shadcn-ui
   npm install
   ```
2. **Configure API endpoint:**
   - (Optional) Set `REACT_APP_API_BASE_URL` in a `.env` file if backend is not on default `localhost:8001`.
3. **Start the development server:**
   ```bash
   npm start
   ```
   - The app will be available at `http://localhost:3000`.

---

## Overview

Money Lens Agent is an advanced, modular financial intelligence platform that orchestrates AI-driven workflows for personal finance management, analytics, and advisory. It integrates backend financial data aggregation, AI-powered analysis, and a modern frontend dashboard to deliver actionable insights and personalized recommendations to users.

---

## Architecture

**1. Backend (fi-mcp-client/):**
  - **API Server:** Python FastAPI server (`api_server_new.py`, `api_server.py`) orchestrates workflows, manages sessions, and routes user requests to the appropriate financial tools and AI models.
  - **Tool Layer:** Implements financial data retrieval, market analysis, portfolio analytics, and web search as modular tools (see `financial_tools.py`, `web_search.py`).
  - **Agent Orchestration:** Supports multiple workflow types (simple response, parallelization, prompt chaining, orchestrator-workers) for flexible, context-aware financial reasoning.
  - **Session & Context Management:** Tracks user sessions, conversation turns, tool executions, and maintains a financial context for each user.
  - **Integration:** Connects to external MCP (Model Context Protocol) servers and Google Gemini AI for advanced reasoning and data enrichment.

**2. Frontend (shadcn-ui/):**
  - **React App:** Modern dashboard and chat UI built with React, TailwindCSS, and shadcn/ui components.
  - **Dashboard Components:** Visualizes net worth, investments, spending, goals, and recent transactions (`FinancialDashboard_new.jsx`, `DashboardTest.jsx`).
  - **Authentication & Session:** Handles user authentication and session management for secure data access.

**3. Static Assets:**
  - HTML, CSS, and JS for legacy and demo UIs (`fi-mcp-client/static/`).

---

## Key Workflows

### 1. Simple Response
For direct queries (e.g., "What is my net worth?"), the agent fetches data from connected accounts and returns a concise answer.

### 2. Parallelization
For complex, multi-entity queries (e.g., "Analyze these 3 stocks and my mutual funds"), the agent decomposes the request, runs tools in parallel, and synthesizes results.

### 3. Prompt Chaining
For multi-step reasoning (e.g., "How should I rebalance my portfolio based on current market trends?"), the agent chains prompts: gathers data, analyzes in context, and generates recommendations.

### 4. Orchestrator-Workers
For advanced scenarios, an orchestrator agent decomposes tasks, delegates to specialized worker agents (e.g., market analysis, risk assessment), and integrates their outputs for a comprehensive response.

---

## End-to-End Implementation

### 1. Session Creation
- User initiates a session via the frontend or API (`/session/create`).
- Backend creates a session, initializes context, and (optionally) authenticates with the MCP server.

### 2. Data Aggregation & Tool Execution
- User requests (via chat or dashboard) are routed to the agent.
- The agent selects the optimal workflow, invokes relevant tools (e.g., fetch bank transactions, analyze stocks), and aggregates results.

### 3. AI Reasoning & Synthesis
- Results from tools are passed to Google Gemini or other LLMs for reasoning, synthesis, and personalized recommendations.
- The agent maintains conversation and financial context for continuity.

### 4. Dashboard Visualization
- The frontend fetches structured dashboard data via API (`/session/{session_id}/dashboard`).
- Data is visualized in real time: net worth, investments, spending, goals, and categorized transactions.

### 5. User Feedback Loop
- Users interact with the chat or dashboard, triggering new workflows and refining insights.

---



## Motive & Vision

Money Lens Agent aims to democratize advanced financial intelligence by:
- Automating data aggregation from multiple financial sources
- Providing AI-driven, actionable insights and recommendations
- Enabling secure, privacy-preserving personal finance management
- Supporting extensible workflows for future financial tools and analytics


