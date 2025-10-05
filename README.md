# Momentum - Flow-State Engineering Agent 🚀

[![Version](https://img.shields.io/badge/version-1.0-blue.svg)](https://github.com/striver-24/Momentum)
[![Python](https://img.shields.io/badge/python-3.12+-green.svg)](https://python.org)
[![Next.js](https://img.shields.io/badge/Next.js-14.0-black.svg)](https://nextjs.org)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

An autonomous software development agent that transforms high-level business requirements into production-ready code through automated development loops.

## 🎯 Overview

Momentum is designed to radically accelerate software development by automating the entire inner development loop. Simply provide natural language requirements, and receive fully tested, documented, and production-ready code in the form of a pull request.

### ✨ Current Status
- ✅ **Backend API**: FastAPI server running on port 8000
- ✅ **Frontend**: Next.js React application on port 3000  
- ✅ **Configuration System**: Centralized YAML-based configuration
- ✅ **LLM Integration**: Custom Cerebras model support (llama-4-scout-17b-16e-instruct)
- ✅ **Development Environment**: Fully functional with live reloading
- 🚧 **Agent Orchestration**: In development
- 🚧 **GitHub Integration**: Planned

### Key Features

- **Natural Language Input**: Submit requirements in plain English
- **Centralized Configuration**: YAML-based configuration system for easy customization
- **Modern Stack**: FastAPI backend + Next.js frontend with TypeScript
- **Autonomous Code Generation**: From a single prompt, Momentum generates a plan, writes code, and creates tests.
- **Isolated Execution**: Docker-based containerization for safe code execution
- **Self-Correction**: Automatic bug fixing based on AI feedback
- **Vector Memory**: Long-term codebase understanding and consistency

## 🏗️ System Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Frontend      │───▶│  FastAPI Backend │───▶│   LLM Core      │
│  (Next.js)      │    │   (Port 8000)    │    │ (Cerebras AI)   │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                │                        │
                                ▼                        ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│ Vector Database │    │ Config System    │    │  Code Quality   │
│ (ChromaDB)      │    │ (config.yaml)    │    │ & Verification  │
│                 │    │                  │    │ (CodeRabbitAI)  │
└─────────────────┘    └──────────────────┘    └─────────────────┘
```

## 🛠️ Technology Stack

- **Backend**: Python 3.12+, FastAPI, Uvicorn
- **Frontend**: Next.js 14, React 18, TypeScript, Tailwind CSS  
- **Configuration**: YAML-based centralized config system
- **LLM & Compute**: Custom Cerebras model (llama-4-scout-17b-16e-instruct)
- **Vector Database**: ChromaDB (local)
- **Development**: Hot reloading, CORS enabled for local development

## 🚀 Quick Start

### Prerequisites

- Python 3.12 or higher
- Node.js 18+ and npm
- Git
- GitHub account (for future integration)

### Installation & Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/striver-24/Momentum.git
   cd Momentum
   ```

2. **Backend Setup**
   ```bash
   cd backend
   
   # Create and activate virtual environment
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   
   # Install dependencies
   pip install -r requirements.txt
   ```

3. **Frontend Setup**
   ```bash
   cd apps/frontend
   
   # Install dependencies
   npm install
   ```

4. **Configuration**
   
   The application uses a centralized configuration system. Main config is in `backend/config.yaml`:
   
   ```yaml
   # Key configurations (automatically loaded)
   models:
     llm:
       name: "llama-4-scout-17b-16e-instruct"  # Custom Cerebras model
       max_tokens: 500
       temperature: 0.5
     embedding:
       name: "all-MiniLM-L6-v2"
   
   vector_db:
     type: "chromadb"
     path: "backend/chroma_db"
   
   # See backend/config.yaml for full configuration options
   ```

### Running the Application

1. **Start the Backend** (Terminal 1)
   ```bash
   cd backend
   source venv/bin/activate
   uvicorn main:app --host 0.0.0.0 --port 8000 --reload
   ```
   Backend will be available at: http://localhost:8000

2. **Start the Frontend** (Terminal 2)
   ```bash
   cd apps/frontend
   npm run dev
   ```
   Frontend will be available at: http://localhost:3000

3. **Verify Setup**
   - Backend API docs: http://localhost:8000/docs
   - Configuration test: http://localhost:8000/config
   - Frontend interface: http://localhost:3000

## 📖 API Reference

### Backend Endpoints

#### Health Check
```http
GET http://localhost:8000/
```
Response: `{"status": "ok", "message": "Orchestrator is running"}`

#### Configuration Info
```http
GET http://localhost:8000/config
```
Returns current configuration including LLM model and settings.

#### Agent Execution
```http
POST http://localhost:8000/agent/run
Content-Type: application/json

{
  "prompt": "Create a simple hello world function"
}
```

## 🔧 Configuration System

### Centralized Config (`backend/config.yaml`)

The application features a comprehensive YAML-based configuration system:

```yaml
# Model Configuration
models:
  llm:
    name: "llama-4-scout-17b-16e-instruct"
    max_tokens: 500
    temperature: 0.5
    timeout: 60
  embedding:
    name: "all-MiniLM-L6-v2"
    show_progress: true

# Vector Database
vector_db:
  type: "chromadb"
  path: "backend/chroma_db"
  collection_name: "codebase_memory"

# File System Settings
file_system:
  default_code_file: "src/new_feature.py"
  default_test_file: "tests/test_new_feature.py"

# Prompts and Templates
prompts:
  planning:
    system: "You are an expert software engineer..."
    template: "Task: {task}"
  
# See full config.yaml for all available options
```

### Config Access in Code

```python
from config.config_loader import ConfigLoader

config = ConfigLoader()
llm_model = config.get("models.llm.name")
max_tokens = config.get("models.llm.max_tokens")
vector_db_path = config.get("vector_db.path")
```

## 🔄 Development Workflow

### Current Implementation Status

#### ✅ **Working Features**
1. **Configuration Management**: Centralized YAML config system
2. **Backend API**: FastAPI server with live reloading
3. **Frontend Interface**: Next.js React application
4. **API Integration**: Frontend can communicate with backend
5. **Custom LLM Support**: Cerebras model integration ready

#### 🚧 **In Development**
1. **Agent Orchestration**: Task planning and execution
2. **Code Generation**: Automated code creation workflow
3. **GitHub Integration**: PR creation and management
4. **Vector Database**: Codebase memory and search

### 1. Current Workflow

```
User Input (Frontend) → Agent API → Configuration → Mock Response
```

### 2. Planned Automated Process

## 📁 Project Structure

```
Momentum/
├── backend/                     # FastAPI backend server
│   ├── src/
│   │   ├── config/             # Configuration management
│   │   │   └── config_loader.py
│   │   ├── agent/              # Core agent logic
│   │   │   ├── orchestrator.py
│   │   │   └── state_machine.py
│   │   ├── api/                # FastAPI endpoints
│   │   │   ├── main.py
│   │   │   └── websocket_manager.py
│   │   └── connectors/         # External service integrations
│   │       ├── llm_connector.py
│   │       ├── vector_db_connector.py
│   │       ├── slack_connector.py
│   │       ├── github_connector.py
│   │       ├── git_connector.py
│   │       └── docker_connector.py
│   ├── config.yaml             # Centralized configuration
│   ├── main.py                 # Application entry point
│   ├── requirements.txt        # Python dependencies
│   └── .env                    # Environment variables
├── apps/
│   └── frontend/               # Next.js web interface
│       ├── app/
│       │   ├── page.tsx        # Main chat interface
│       │   ├── layout.tsx      # App layout
│       │   └── globals.css     # Global styles
│       ├── package.json
│       ├── next.config.js
│       ├── tailwind.config.js
│       ├── tsconfig.json
│       └── postcss.config.js
├── .gitignore
├── package.json                # Root package.json
└── README.md
```

## 🧩 Core Components

### Configuration System (`backend/src/config/`)

Centralized YAML-based configuration management:
- **ConfigLoader**: Handles loading and accessing configuration with dot notation
- **Validation**: Ensures all required configuration sections are present
- **Environment Support**: Seamless integration with environment variables

### Backend API (`backend/main.py`)

FastAPI server with:
- **CORS Support**: Enabled for frontend development
- **Configuration Integration**: Live config loading and testing endpoints
- **Agent Endpoints**: RESTful API for agent interaction

### Frontend Interface (`apps/frontend/`)

Modern Next.js application featuring:
- **TypeScript**: Full type safety
- **Tailwind CSS**: Modern styling framework
- **React 18**: Latest React features with SSR support
- **Real-time UI**: Chat interface with workflow visualization

### Agent System (`backend/src/agent/`)

Core orchestration components:
- **Orchestrator**: Main agent coordination logic
- **State Machine**: Workflow state management
- **Connectors**: External service integrations

## 🎛️ Configuration

### Agent Behavior

Customize the agent's behavior through configuration files:

```python
# backend/config/agent_config.py
AGENT_CONFIG = {
    "max_iterations": 5,
    "test_coverage_threshold": 80,
    "code_review_strictness": "high",
    "auto_merge_approved": False,
    "documentation_level": "comprehensive"
}
```

### LLM Parameters

```python
# backend/config/llm_config.py
LLM_CONFIG = {
    "model": "llama3-70b",
    "temperature": 0.1,
    "max_tokens": 4096,
    "context_window": 32768
}
```

## 🔌 API Reference

### REST Endpoints

#### Submit Feature Request

```http
POST /api/v1/features
Content-Type: application/json

{
  "description": "Feature description in natural language",
  "priority": "high|medium|low",
  "target_branch": "main"
}
```

#### Get Feature Status

```http
GET /api/v1/features/{feature_id}/status
```

#### List Features

```http
GET /api/v1/features?status=pending|in_progress|completed|failed
```

## 🧪 Testing

### Run Backend Tests

```bash
cd backend
python -m pytest tests/ -v --coverage
```

### Run Frontend Tests

```bash
cd apps/frontend
npm test
```

### Integration Tests

```bash
# Run full end-to-end tests
python -m pytest tests/integration/ -v
```

## 🚀 Deployment

### Docker Deployment

```bash
# Build and run with Docker Compose
docker-compose up -d
```

### Cloud Deployment

```bash
# Deploy to your preferred cloud provider
# Configuration files provided for AWS, GCP, Azure
```

## 🐛 Troubleshooting

### Common Issues

#### Backend Won't Start

```bash
# Check Python virtual environment
cd backend
source venv/bin/activate
python --version  # Should be 3.12+

# Verify dependencies
pip list | grep fastapi

# Check configuration
python -c "from src.config.config_loader import ConfigLoader; print('Config OK')"
```

#### Frontend Build Issues

```bash
# Clear cache and reinstall
cd apps/frontend
rm -rf node_modules package-lock.json
npm install

# Check Next.js version
npx next --version  # Should be 14.0+
```

#### Configuration Problems

```bash
# Test configuration loading
cd backend
python -c "
from src.config.config_loader import ConfigLoader
config = ConfigLoader()
print(f'LLM Model: {config.get(\"models.llm.name\")}')
"
```

#### Port Conflicts

```bash
# Check if ports are in use
lsof -i :8000  # Backend port
lsof -i :3000  # Frontend port

# Kill processes if needed
kill -9 <PID>
```

#### API Connection Issues

```bash
# Test backend API directly
curl http://localhost:8000/
curl http://localhost:8000/config

# Check CORS settings in main.py
# Ensure frontend URL is in allow_origins
```

### Development Tips

#### Live Reloading
- Backend: Uvicorn automatically reloads on file changes
- Frontend: Next.js hot reloads on component changes
- Config: Changes to `config.yaml` require backend restart

#### Debugging
- Backend logs: Check terminal running uvicorn
- Frontend logs: Check browser developer console
- API testing: Use http://localhost:8000/docs for Swagger UI

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes and add tests
4. Run the test suite: `npm test` or `pytest`
5. Commit your changes: `git commit -m 'Add amazing feature'`
6. Push to the branch: `git push origin feature/amazing-feature`
7. Open a Pull Request

## 📋 Roadmap

### Phase 1: Foundation ✅

- [x] Basic orchestration engine setup
- [x] Centralized configuration system (YAML-based)
- [x] FastAPI backend with CORS support
- [x] Next.js frontend with TypeScript
- [x] Configuration loading and validation
- [x] Project structure setup
- [x] Environment configuration support
- [x] Git repository setup with proper .gitignore
- [x] Comprehensive documentation
- [x] Development environment with live reloading
- [x] API endpoint structure (/config, /agent/run)
- [x] Frontend-backend integration testing

### Phase 2: Core Agent Features 🚧

- [x] Basic agent API endpoints
- [x] Configuration system integration
- [x] Custom LLM model support (Cerebras)
- [ ] Vector database integration (ChromaDB)
- [ ] Complete LLM connector implementation
- [ ] Task decomposition and planning logic
- [ ] Code generation workflows
- [ ] Agent orchestration engine
- [ ] State machine implementation

### Phase 3: Advanced Capabilities �

- [ ] GitHub integration and PR creation
- [ ] CodeRabbitAI review integration
- [ ] Docker containerization for code execution
- [ ] Advanced prompt engineering
- [ ] Self-correction mechanisms
- [ ] Multi-language support
- [ ] Advanced testing strategies
- [ ] Performance optimization
- [ ] Security scanning integration

### Phase 4: Production Features 📋

- [ ] Slack integration
- [ ] WebSocket real-time updates
- [ ] Database integration
- [ ] Logging and monitoring
- [ ] Advanced web interface features
- [ ] Team collaboration tools
- [ ] Analytics and reporting
- [ ] CLI interface enhancements
- [ ] Performance optimization
- [ ] Security scanning integration
- [ ] Database integration
- [ ] Logging and monitoring

### Phase 4: User Experience 📋

- [ ] Complete web interface
- [ ] Real-time progress tracking
- [ ] Advanced configuration options
- [ ] Team collaboration features
- [ ] CLI interface
- [ ] Dashboard and analytics

## 🐛 Troubleshooting

### Common Issues

#### Docker Connection Issues

```bash
# Check Docker daemon status
docker info

# Restart Docker Desktop
# On macOS: restart Docker Desktop app
# On Linux: sudo systemctl restart docker
```

#### API Key Configuration

```bash
# Verify environment variables
python -c "import os; print('CEREBRAS_API_KEY' in os.environ)"
```

#### GitHub Integration

```bash
# Test GitHub token permissions
curl -H "Authorization: token $GITHUB_TOKEN" https://api.github.com/user
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Meta AI for the Llama language model
- Cerebras Systems for high-performance AI infrastructure
- CodeRabbitAI for automated code review capabilities
- The open-source community for foundational tools and libraries

## 📞 Support

- **Documentation**: [Wiki](https://github.com/striver-24/Momentum/wiki)
- **Issues**: [GitHub Issues](https://github.com/striver-24/Momentum/issues)
- **Discussions**: [GitHub Discussions](https://github.com/striver-24/Momentum/discussions)
- **Email**: support@momentum-agent.dev

---

**Built with ❤️ by Deivyansh Singh**
