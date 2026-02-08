# 🧠 Hackathon II – Phase III  
## **Evolution of Todo: AI Chatbot**

Phase III evolves the **Phase II full-stack Todo app** into an **AI-powered chatbot** capable of managing tasks via natural language.  

All features are implemented **via Claude Code + Spec-Kit Plus**. No manual coding allowed.  

---

## 🎯 Phase III Goal

- Conversational interface for all basic Todo features  
- AI logic powered by **OpenAI Agents SDK**  
- **MCP Server** exposes task operations as tools (stateless)  
- Conversation state persisted in **Neon PostgreSQL**  

💡 **Development Approach:** Agentic Dev Stack → Spec → Plan → Tasks → Claude Code implementation.

---

## ✨ Features

- ➕ Add tasks via natural language  
- 📋 List tasks  
- ✅ Mark tasks complete  
- ❌ Delete tasks  
- ✏️ Update tasks  
- Maintains conversation history (stateless server)  
- Friendly confirmations & graceful error handling  

---

## 🖥️ Technology Stack

| Component      | Technology |
|----------------|------------|
| Frontend       | OpenAI ChatKit |
| Backend        | FastAPI |
| AI Framework   | OpenAI Agents SDK |
| MCP Server     | Official MCP SDK |
| ORM            | SQLModel |
| Database       | Neon Serverless PostgreSQL |
| Authentication | Better Auth (JWT) |

---

## 🔗 Chat API Endpoint

**POST** `/api/{user_id}/chat` – Send user message & get AI response  

**Request:**  
- `conversation_id` (optional) – Existing conversation  
- `message` (string, required) – User message  

**Response:**  
- `conversation_id` – ID of conversation  
- `response` – AI assistant reply  
- `tool_calls` – MCP tools invoked  

---

## 🛠️ MCP Tools

| Tool          | Purpose | Parameters | Example Output |
|---------------|---------|-----------|----------------|
| add_task      | Create new task | user_id, title, description | `{"task_id":5,"status":"created","title":"Buy groceries"}` |
| list_tasks    | Retrieve tasks | user_id, status | `[{"id":1,"title":"Buy groceries","completed":false}]` |
| complete_task | Mark complete | user_id, task_id | `{"task_id":3,"status":"completed","title":"Call mom"}` |
| delete_task   | Delete task | user_id, task_id | `{"task_id":2,"status":"deleted","title":"Old task"}` |
| update_task   | Update task | user_id, task_id, title, description | `{"task_id":1,"status":"updated","title":"Buy groceries and fruits"}` |

**Agent Behavior:**  
- Detects user intent and calls appropriate MCP tool  
- Confirms all actions to user  
- Handles errors gracefully  

---

## 🏗️ Architecture

ChatKit UI (Frontend)
│
▼
FastAPI Chat Endpoint (/api/chat)
│
▼
OpenAI Agents SDK (Agent + Runner)
│
▼
MCP Server (Stateless Tools)
│
▼
Neon PostgreSQL (tasks, conversations, messages)


**Stateless server benefits:**  
- Scalable & resilient  
- Horizontal scaling possible  
- Each request independent & reproducible  

---

## 💡 Conversation Flow

1. User sends message  
2. Fetch conversation history from DB  
3. Store user message  
4. Run agent with MCP tools  
5. Store assistant response  
6. Return response to frontend  

**Natural language examples:**  
- `"Add a task to buy groceries"` → `add_task`  
- `"Show me all my tasks"` → `list_tasks`  
- `"Mark task 3 as complete"` → `complete_task`  
- `"Delete the meeting task"` → `delete_task`  
- `"Change task 1 to 'Call mom tonight'"` → `update_task`  

---

## 🌐 Frontend Deployment & ChatKit Setup

1. Deploy frontend (Vercel/GitHub Pages/custom domain)  
2. Add domain to **OpenAI domain allowlist**  
3. Obtain domain key → `NEXT_PUBLIC_OPENAI_DOMAIN_KEY`  
4. Use key in ChatKit configuration  

**Note:** Local development (`localhost`) works without domain allowlist.

---

## ▶️ How to Run

**Frontend (ChatKit):**  
```bash
cd frontend
npm install
npm run dev

Backend (FastAPI + MCP):

cd backend
uvicorn main:app --reload --port 8000


Or run both using Docker:

docker-compose up

🚀 Deliverables

Working AI chatbot UI using OpenAI ChatKit

FastAPI backend with Agents SDK + MCP tools

Conversation state persisted in Neon PostgreSQL

Specs in /specs for AI behavior, MCP tools, and features
