# Studymate
📚 StudyMate – AI-Powered Learning Platform

StudyMate is a full-stack web application designed to help learners explore, understand, and interact with online courses.
It combines a React frontend, a FastAPI backend, and an integrated AI assistant powered by OpenAI to answer questions about the available courses.

🚀 Features
🧠 AI-Powered Assistant

Chatbot assistant helps users learn about courses in real-time.

Understands course details (name, description, instructor, difficulty, duration, price).

Fetches all course data directly from the database — answers are always up-to-date.

📘 Course Management

Browse all available courses.

View detailed information about each course (description, difficulty, duration, instructor, and price).

⚡ Modern Full Stack Architecture

React frontend with a responsive, ChatGPT-style chat interface.

FastAPI backend with PostgreSQL/SQLite database support.

CORS-enabled communication between frontend and backend.

🧩 Tech Stack
Layer	Technology
Frontend	React (TypeScript or JS)
UI Styling	Bootstrap / Tailwind CSS
Backend	FastAPI (Python 3.11+)
Database	PostgreSQL (default)
ORM	SQLAlchemy
AI Integration	OpenAI API
Environment Variables	python-dotenv
HTTP Client (Frontend)	Axios
🏗️ Project Structure
studymate/
│
├── backend/
│   ├── main.py                # FastAPI entry point
│   ├── models.py              # SQLAlchemy models
│   ├── routes/
│   │   ├── courses.py         # CRUD routes for courses
│   ├── db.py                  # Database connection and session setup
│   ├── ai.py (optional)       # AI assistant routes (if modularized)
│   ├── .env                   # Contains OpenAI API key, DB URL
│   └── __init__.py
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── CourseCard.tsx
│   │   │   ├── AIAssistant.tsx
│   │   ├── pages/
│   │   │   ├── Home.tsx
│   │   ├── services/
│   │   │   ├── api.ts         # Axios calls to FastAPI backend
│   │   ├── App.tsx
│   │   ├── index.tsx
│   ├── package.json
│
└── README.md
