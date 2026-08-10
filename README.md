# 🤖 AI Chat App

### 💬 A full-stack-ready AI conversation backend with authentication, persistent chat history, token tracking & intelligent conversation summarization.

<p align="center">
  <strong>⚡ AI • 🔐 Authentication • 💾 MongoDB • 🧠 Context Memory • 📊 Token Tracking</strong>
</p>

---

## 🌟 Overview

**AI Chat App** is an AI-powered conversational backend built with **Node.js, Express.js, MongoDB and OpenRouter**.

The application goes beyond sending a simple prompt to an AI model. It provides a structured backend for managing users, conversations, messages, authentication, AI context and token usage.

### 🔥 What makes it interesting?

> Instead of sending the entire conversation to the AI every time, the application can **summarize older conversation history** and use that summary as context — helping control the amount of data sent to the model.

---

## ✨ Features

|           Feature              |                  Description                            |
| ------------------------------ | ------------------------------------------------------- |
| 🤖 **AI Conversations**        | Send messages to AI models through OpenRouter           |
| 🔐 **JWT Authentication**      | Secure signup/login using JWT                           |
| 🍪 **HTTP-Only Cookies**       | Authentication token stored in HTTP-only cookies        |
| 🔒 **Password Hashing**        | Passwords protected using bcrypt                        |
| 💬 **Persistent Chats**        | Conversations stored in MongoDB                         |
| 🧠 **Conversation Memory**     | Previous messages and summaries are used as AI context  |
| 📝 **Automatic Summarization** | Older messages can be summarized to reduce context size |
| 📊 **Token Tracking**          | Prompt, completion and total tokens are tracked         |
| 🚦 **Token Limits**            | Per-user token usage limits                             |
| 🗑️ **Chat Management**         | Create, retrieve and delete chats                       |
| 👤 **User Management**         | Signup, login, profile and account deletion             |
| ✅ **Input Validation**        | Zod-based validation for authentication                 |
| ⚡ **REST APIs**               | Clean API structure using Express routers               |

---

# 🧠 How It Works

```text
                 ┌──────────────────┐
                 │      Client      │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │   Express API    │
                 └────────┬─────────┘
                          │
              ┌───────────┼───────────┐
              │           │           │
              ▼           ▼           ▼
         🔐 Auth      💬 Chat      👤 User
              │           │           │
              └───────────┼───────────┘
                          ▼
                  ┌───────────────┐
                  │    MongoDB    │
                  └───────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │ Context Builder│
                  └───────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │   OpenRouter  │
                  │   AI Models   │
                  └───────┬───────┘
                          │
                          ▼
                  🤖 AI Response
```

---

# 🏗️ Architecture

The backend follows a layered structure:

```text
Request
   │
   ▼
Routes
   │
   ▼
Authentication Middleware
   │
   ▼
Controllers
   │
   ├──────────────► Services
   │                    │
   │                    ▼
   │                OpenRouter
   │
   ▼
Models
   │
   ▼
MongoDB
```

---

# 📁 Project Structure

```text
AI-Chat-App/
│
├── config/
│   ├── database.js
│   └── openRouter.js
│
├── controllers/
│   ├── chatController.js
│   ├── messageController.js
│   └── userController.js
│
├── middlewares/
│   └── authUserMiddleware.js
│
├── model/
│   ├── chatSchema.js
│   ├── messageSchema.js
│   └── userSchema.js
│
├── routes/
│   ├── chatRouter.js
│   ├── messageRouter.js
│   └── userRouter.js
│
├── service/
│   ├── openRouterService.js
│   └── summaryService.js
│
├── utils/
│   ├── chatContext.js
│   ├── tokenUsage.js
│   └── userUsage.js
│
├── validators/
│   └── userValidators.js
│
├── TesterPlatform/
│   └── AI model experiments
│
├── .env.example
├── .gitignore
├── index.js
├── package.json
└── README.md
```

---

# 🔐 Authentication Flow

```text
                 Signup / Login
                       │
                       ▼
                Validate Input
                       │
                       ▼
                 Find User
                       │
                       ▼
              bcrypt Password Check
                       │
                       ▼
                  Create JWT
                       │
                       ▼
             HTTP-Only Cookie
                       │
                       ▼
              Protected Requests
                       │
                       ▼
             JWT Verification
                       │
                       ▼
                   req.user
```

Authentication includes:

* JWT-based authentication
* HTTP-only cookies
* bcrypt password hashing
* Protected user/chat/message routes
* User-specific chat access

---

# 💬 Chat Flow

When a user sends a message:

```text
User Message
     │
     ▼
Validate Request
     │
     ▼
Check Token Limit
     │
     ▼
Find/Create Chat
     │
     ▼
Load Previous Context
     │
     ▼
Add Conversation Summary
     │
     ▼
Build AI Messages
     │
     ▼
OpenRouter
     │
     ▼
AI Response
     │
     ├───────────────┐
     ▼               ▼
Save Message     Track Usage
     │               │
     └───────┬───────┘
             ▼
        Send Response
```

---

# 🧠 Conversation Summarization

One of the core ideas of the project is **conversation context management**.

Instead of allowing the conversation history to grow indefinitely, the application keeps track of summarized messages.

```text
Message 1
Message 2
Message 3
...
Message 20
      │
      ▼
🧠 Generate Summary
      │
      ▼
Store Summary in MongoDB
      │
      ▼
Use Summary + New Messages
      │
      ▼
Send Context to AI
```

This helps maintain relevant context while controlling the amount of conversation history sent to the model.

---

# 📊 Token Usage Tracking

The application tracks:

```text
Prompt Tokens
       +
Completion Tokens
       =
Total Tokens
```

Token usage is maintained at both:

### 👤 User level

```text
tokenUsed
tokenLimit
totalTokenUsed
resetAt
```

### 💬 Chat level

```text
promptTokens
completionTokens
totalTokens
```

This allows the application to enforce usage limits and monitor AI consumption.

---

# 🛠️ Tech Stack

### Backend

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge\&logo=node.js\&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-000000?style=for-the-badge\&logo=express\&logoColor=white)

### Database

![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge\&logo=mongodb\&logoColor=white)
![Mongoose](https://img.shields.io/badge/Mongoose-880000?style=for-the-badge\&logo=mongoose\&logoColor=white)

### AI

![OpenRouter](https://img.shields.io/badge/OpenRouter-AI-purple?style=for-the-badge)
![Google Gemini](https://img.shields.io/badge/Google%20Gemini-AI-4285F4?style=for-the-badge\&logo=google)

### Security & Validation

![JWT](https://img.shields.io/badge/JWT-Authentication-black?style=for-the-badge\&logo=jsonwebtokens)
![Bcrypt](https://img.shields.io/badge/bcrypt-Password%20Hashing-orange?style=for-the-badge)
![Zod](https://img.shields.io/badge/Zod-Validation-3E67B1?style=for-the-badge)

---

# 🚀 API Endpoints

## 👤 User APIs

| Method   | Endpoint        | Description      | Auth |
| -------- | --------------- | ---------------- | ---- |
| `POST`   | `/user/signup`  | Create account   | ❌    |
| `POST`   | `/user/login`   | Login            | ❌    |
| `POST`   | `/user/logout`  | Logout           | ❌    |
| `GET`    | `/user/profile` | Get current user | 🔐   |
| `DELETE` | `/user/delete`  | Delete account   | 🔐   |

---

## 💬 Chat APIs

| Method   | Endpoint              | Description         | Auth |
| -------- | --------------------- | ------------------- | ---- |
| `POST`   | `/chat/createChat`    | Create a chat       | 🔐   |
| `GET`    | `/chat/getRecentChat` | Get recent chats    | 🔐   |
| `GET`    | `/chat/:chatId`       | Get a specific chat | 🔐   |
| `DELETE` | `/chat/:chatId`       | Delete a chat       | 🔐   |

---

## 🤖 Message APIs

| Method | Endpoint       | Description                 | Auth |
| ------ | -------------- | --------------------------- | ---- |
| `POST` | `/msg`         | Start a new AI conversation | 🔐   |
| `POST` | `/msg/:chatId` | Continue a conversation     | 🔐   |
| `GET`  | `/msg/:chatId` | Get conversation messages   | 🔐   |

---

# ⚙️ Environment Variables

Create a `.env` file locally:

```env
PORT=3000

MONGO_URL=your_mongodb_connection_string

JWT_SECRET=your_jwt_secret

OPENROUTER_API_KEY=your_openrouter_api_key

GEMINI_API_KEY=your_gemini_api_key
```

> ⚠️ **Never commit your real `.env` file or API keys to GitHub.**

Use `.env.example` as a template.

---

# 📦 Installation

### 1️⃣ Clone the repository

```bash
git clone https://github.com/ankitanand21/AI-Chat-App.git
```

### 2️⃣ Enter the project

```bash
cd AI-Chat-App
```

### 3️⃣ Install dependencies

```bash
npm install
```

### 4️⃣ Create environment variables

Create:

```text
.env
```

and add your credentials.

### 5️⃣ Start the server

```bash
npm start
```

Or use your development script if configured:

```bash
npm run dev
```

---

# 🧪 Development Experiments

The `TesterPlatform` directory contains experiments used while exploring different AI providers and conversation approaches.

Examples include:

* Google Gemini API
* OpenRouter API
* OpenRouter SDK
* Maintaining conversation history

These experiments helped validate AI integration before building the main application architecture.

---

# 🔮 Future Improvements

* 🎨 Build a dedicated React frontend
* ⚡ Streaming AI responses
* 📎 File/document uploads
* 🧠 More advanced conversation memory
* 🔍 Chat search
* 🌐 Production deployment
* 📈 Usage analytics dashboard
* 🧪 Automated API testing
* 🛡️ Improved production security configuration

---

# 👨‍💻 Author

### Ankit Anand

Backend / Full-Stack Developer focused on building scalable web applications and AI-powered products.

---

<p align="center">

### ⭐ If you find this project interesting, consider giving it a star!

**Built with ☕ + JavaScript + AI**

</p>
