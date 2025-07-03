# DebugXpress - AI-Powered Express.js Debugging Assistant

![Project Status](https://img.shields.io/badge/Status-Active-green)
![Python](https://img.shields.io/badge/Python-FastAPI-blue)
![Next.js](https://img.shields.io/badge/Frontend-Next.js%2015-black)
![Database](https://img.shields.io/badge/Database-PostgreSQL-blue)
![Vector DB](https://img.shields.io/badge/Vector%20DB-Pinecone-orange)
![AI Model](https://img.shields.io/badge/AI-Llama%203--8B-purple)

## 🚀 Overview

DebugXpress is an intelligent debugging assistant specifically designed for **Express.js** developers. It leverages **Retrieval-Augmented Generation (RAG)** architecture to provide contextual, accurate debugging solutions by combining a curated knowledge base of Express.js issues with the power of **Llama 3-8B** language model through **Groq API**.

The application helps developers quickly identify, understand, and resolve Express.js-related issues by retrieving similar problems from a vector database and generating tailored solutions using AI.

## ✨ Key Features

### 🔍 **Intelligent Debugging**

- **Context-Aware Solutions**: Retrieves similar issues from a curated database of Express.js problems
- **AI-Powered Responses**: Uses Llama 3-8B model for generating detailed, formatted solutions
- **Markdown Support**: Provides well-formatted responses with code syntax highlighting

### 🗃️ **Vector Database Integration**

- **Pinecone Integration**: Utilizes Pinecone for efficient similarity search
- **Semantic Embeddings**: Uses sentence transformers for generating 384-dimensional embeddings
- **Express.js Issue Repository**: Pre-loaded with Express.js GitHub issues and solutions

### 💾 **Data Persistence**

- **PostgreSQL Database**: Stores user queries and responses for analytics
- **Session Management**: Tracks user interactions and debugging history
- **Docker Support**: Easy deployment with PostgreSQL containerization

### 🎨 **Modern Frontend**

- **Next.js 15**: React-based frontend with modern UI components
- **Tailwind CSS**: Responsive, modern styling
- **Radix UI**: Accessible, customizable components
- **TypeScript**: Type-safe development experience

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Next.js UI   │────│   FastAPI API    │────│   PostgreSQL   │
│                 │    │                  │    │                 │
│ • Query Input   │    │ • REST Endpoints │    │ • User Queries  │
│ • Response View │    │ • CORS Config    │    │ • Responses     │
│ • Markdown      │    │ • Session Mgmt   │    │ • Analytics     │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                │
                                │
                    ┌──────────────────┐    ┌─────────────────┐
                    │   Pinecone DB    │    │   Groq API      │
                    │                  │    │                 │
                    │ • Vector Search  │    │ • Llama 3-8B    │
                    │ • Embeddings     │    │ • Text Gen      │
                    │ • Express Issues │    │ • Chat API      │
                    └──────────────────┘    └─────────────────┘
```

## 🛠️ Tech Stack

### Backend

- **FastAPI**: High-performance Python web framework
- **SQLAlchemy**: ORM for database operations
- **Pydantic**: Data validation and serialization
- **Pinecone**: Vector database for similarity search
- **Sentence Transformers**: Text embedding generation
- **Groq API**: Access to Llama 3-8B model
- **PostgreSQL**: Primary database with psycopg2 adapter
- **Uvicorn**: ASGI server for FastAPI

### Frontend

- **Next.js 15**: React framework with App Router
- **TypeScript**: Type-safe JavaScript
- **Tailwind CSS**: Utility-first CSS framework
- **Radix UI**: Accessible component primitives
- **Axios**: HTTP client for API communication
- **React Markdown**: Markdown rendering with syntax highlighting
- **Lucide React**: Modern icon library

### DevOps & Deployment

- **Docker Compose**: Container orchestration for PostgreSQL
- **Environment Variables**: Secure configuration management
- **CORS Configuration**: Cross-origin resource sharing setup

## 📋 Prerequisites

Before running the project, ensure you have:

- **Python 3.8+** installed
- **Node.js 18+** and npm/yarn
- **Docker** and **Docker Compose**
- **Pinecone Account** with API key
- **Groq Account** with API key

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd DebugXpress
```

### 2. Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Edit .env with your API keys:
# PINECONE_API_KEY=your_pinecone_api_key
# GROQ_API_KEY=your_groq_api_key
# POSTGRES_USER=your_db_user
# POSTGRES_PASSWORD=your_db_password
# POSTGRES_DB=your_db_name

# Start PostgreSQL with Docker
docker-compose up -d

# Initialize Pinecone data (run once)
cd app/services
python pinecone_service.py
```

### 3. Frontend Setup

```bash
cd ../frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

### 4. Start the Application

```bash
# Terminal 1: Start FastAPI backend
cd backend
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# Terminal 2: Start Next.js frontend (if not already running)
cd frontend
npm run dev
```

The application will be available at:

- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8000
- **API Documentation**: http://localhost:8000/docs

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the `backend` directory:

```env
# Pinecone Configuration
PINECONE_API_KEY=your_pinecone_api_key

# Groq API Configuration
GROQ_API_KEY=your_groq_api_key

# Database Configuration
POSTGRES_USER=your_username
POSTGRES_PASSWORD=your_password
POSTGRES_DB=DebugXpress_db
```

## 📖 Usage

1. **Open the application** in your browser at `http://localhost:3000`
2. **Enter your Express.js issue** or question in the input field
3. **Click Submit** to get an AI-powered solution
4. **View the response** with formatted code snippets and explanations
5. **Browse similar issues** that were used to generate the response

### Example Queries:

- "How to handle CORS errors in Express.js?"
- "Express middleware not executing in correct order"
- "Setting up authentication with Express and JWT"
- "Express route parameters not working"

## 🗄️ Database Schema

### User Interactions Table

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    query TEXT NOT NULL,
    response TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 🔍 API Endpoints

### POST `/generate-response`

Generate a debugging solution for an Express.js issue.

**Request Body:**

```json
{
  "query": "How to fix CORS errors in Express.js?"
}
```

**Response:**

```json
{
  "response": "# CORS Error Solution\n\nTo fix CORS errors in Express.js...",
  "related_issues": [...],
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Groq** for providing access to Llama 3-8B model
- **Pinecone** for vector database services
- **Express.js Community** for the wealth of GitHub issues used in training data
- **FastAPI** and **Next.js** teams for excellent frameworks

## 📞 Support

If you encounter any issues or have questions:

1. Check the [Issues](https://github.com/your-repo/issues) page
2. Create a new issue with detailed information
3. Join our community discussions

---

**Built with ❤️ for the Express.js developer community**
