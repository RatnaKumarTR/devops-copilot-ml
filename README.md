# DevOps Copilot - Intelligent Log Analysis & Troubleshooting Assistant

[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

## 🎯 Overview

Production-ready AI assistant for DevOps troubleshooting that combines:
- **LLM-powered analysis** using Llama 3.1 (8B) for natural language understanding
- **RAG (Retrieval Augmented Generation)** for context-aware responses from documentation
- **ML classification** for automated log categorization and error detection
- **Real-time Kubernetes log collection** from production EKS clusters

Built to reduce MTTR (Mean Time To Resolution) and automate common troubleshooting tasks in enterprise Kubernetes environments.

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      DevOps Copilot System                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────┐    ┌──────────────┐    ┌─────────────────┐  │
│  │ K8s Log      │───▶│ ML Classifier│───▶│   LLM Engine    │  │
│  │ Collector    │    │ (Scikit)     │    │ (Llama 3.1 8B)  │  │
│  └──────────────┘    └──────────────┘    └─────────────────┘  │
│         │                    │                     │           │
│         ▼                    ▼                     ▼           │
│  ┌──────────────────────────────────────────────────────────┐ │
│  │         DuckDB (Log Storage & Analytics)                 │ │
│  └──────────────────────────────────────────────────────────┘ │
│         │                                                      │
│         ▼                                                      │
│  ┌──────────────────────────────────────────────────────────┐ │
│  │    RAG System (ChromaDB + Documentation Embeddings)      │ │
│  └──────────────────────────────────────────────────────────┘ │
│         │                                                      │
│         ▼                                                      │
│  ┌──────────────────────────────────────────────────────────┐ │
│  │         FastAPI Backend + Streamlit UI                   │ │
│  └──────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

## 🚀 Features

### Core Capabilities
- ✅ **Real-time Log Collection** from Kubernetes (AWS EKS)
- ✅ **Intelligent Error Categorization** (Orleans, Istio, RabbitMQ, PostgreSQL, etc.)
- ✅ **Root Cause Prediction** using ML classification models
- ✅ **Context-Aware Troubleshooting** via RAG with documentation
- ✅ **Natural Language Interface** for queries and troubleshooting
- ✅ **Production-Ready Deployment** (Docker + Kubernetes)

### Supported Error Categories
- Orleans cluster communication issues
- Istio service mesh routing problems
- RabbitMQ TLS/connection failures
- PostgreSQL database connectivity
- Resource limit violations (OOM, CPU throttling)
- ArgoCD sync failures
- General Kubernetes pod issues

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **LLM** | Llama 3.1 (8B) via Ollama | Natural language understanding & generation |
| **RAG Framework** | LangChain + ChromaDB | Context retrieval from documentation |
| **ML Classification** | Scikit-learn | Log categorization & pattern recognition |
| **NLP** | Transformers (HuggingFace) | Text processing & embeddings |
| **Database** | DuckDB | High-performance log storage & analytics |
| **API** | FastAPI | RESTful endpoints for integrations |
| **UI** | Streamlit | Interactive web interface |
| **K8s Client** | kubernetes-python | Real-time log collection |
| **Deployment** | Docker + Kubernetes | Production containerized deployment |

## 📦 Installation

### Prerequisites
- Python 3.11 or higher
- Ollama (for local LLM inference)
- kubectl configured with EKS access
- 8GB+ RAM (for running Llama 3.1 8B model)
- AWS credentials configured

### Quick Setup

```bash
# 1. Clone repository
git clone https://github.com/RatnaKumarTR/devops-copilot-ml.git
cd devops-copilot-ml

# 2. Create virtual environment
python3.11 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Install Ollama and download model
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3.1:8b

# 5. Configure Kubernetes access
aws eks --region us-east-1 update-kubeconfig --name a208234-preprod-confirm-ot-useast1-plexus-cluster

# 6. Verify setup
python -c "import ollama; print('Ollama ready!')"
kubectl get pods -n 207804-confirmation-qa
```

## 🎯 Quick Start

### Collect Logs from Kubernetes
```bash
# Collect logs from QA namespace
python src/collectors/k8s_log_collector.py --namespace 207804-confirmation-qa

# Collect logs with specific label selector
python src/collectors/k8s_log_collector.py --namespace 207804-confirmation-qa --label app=my-service
```

### Start the API Server
```bash
# Development mode with auto-reload
uvicorn src.api.main:app --reload --host 0.0.0.0 --port 8000

# Production mode
uvicorn src.api.main:app --host 0.0.0.0 --port 8000 --workers 4
```

### Launch Interactive UI
```bash
streamlit run ui/app.py
```

### Query via Python API
```python
from src.rag.knowledge_base import DevOpsKnowledgeBase

# Initialize knowledge base
kb = DevOpsKnowledgeBase()
kb.create_vector_store()

# Ask questions
result = kb.query("How do I fix Orleans silo connection issues with Istio?")
print(result['answer'])
```

## 📊 Project Structure

```
devops-copilot-ml/
├── data/
│   ├── logs/              # Log storage (DuckDB databases)
│   ├── documentation/     # Knowledge base documentation
│   └── models/            # Trained ML models
├── src/
│   ├── collectors/        # Kubernetes log collectors
│   │   └── k8s_log_collector.py
│   ├── processors/        # Log processing pipeline
│   │   ├── log_parser.py
│   │   └── log_classifier.py
│   ├── rag/              # RAG implementation
│   │   ├── knowledge_base.py
│   │   └── embeddings.py
│   └── api/              # FastAPI endpoints
│       └── main.py
├── notebooks/            # Jupyter notebooks for analysis
│   ├── 01_data_exploration.ipynb
│   ├── 02_model_training.ipynb
│   └── 03_rag_evaluation.ipynb
├── tests/               # Unit and integration tests
│   ├── test_collectors.py
│   ├── test_processors.py
│   └── test_rag.py
├── docker/              # Docker configurations
│   ├── Dockerfile
│   └── docker-compose.yml
├── docs/                # Additional documentation
│   ├── ARCHITECTURE.md
│   ├── API.md
│   └── DEPLOYMENT.md
├── .gitignore
├── requirements.txt
├── README.md
└── LICENSE
```

## 🧪 Testing

```bash
# Run all tests
pytest tests/ -v

# Run with coverage report
pytest --cov=src tests/ --cov-report=html

# Run specific test file
pytest tests/test_collectors.py -v

# Run with markers
pytest -m "not slow" tests/
```

## 🚀 Deployment

### Docker Deployment
```bash
# Build image
docker build -t devops-copilot:latest -f docker/Dockerfile .

# Run container
docker run -p 8000:8000 -v ~/.kube:/root/.kube devops-copilot:latest
```

### Kubernetes Deployment
```bash
# Apply manifests
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml

# Check status
kubectl get pods -l app=devops-copilot
kubectl logs -f deployment/devops-copilot
```

## 📈 Learning Progress

**Start Date**: October 7, 2025  
**Current Status**: Day 1/21 Complete ✅  
**Progress**: 5%

### Quick Links
- [📅 Progress Tracker](docs/progress/README.md) - Daily logs and metrics
- [📖 Learning Path](docs/ML_LEARNING_PATH.md) - 3-week structured plan
- [📝 Day 1 Log](docs/progress/DAY01.md) - Setup & Installation

### 3-Week Plan

**Week 1: ML Fundamentals** (Days 1-7) - 1/7 complete
- Learn core ML concepts for log classification
- Understand model evaluation metrics

**Week 2: Neural Networks & LLMs** (Days 8-14)
- Understand LLMs and RAG systems
- Learn LangChain and embeddings

**Week 3: Build the Project** (Days 15-21)
- Implement K8s log collector
- Train ML classifier
- Build RAG system with LLM
- Create API and UI

## 🎓 Learning Resources

This project was built following industry best practices and modern ML/MLOps patterns. Key learning resources:

### Books
- "Hands-On Machine Learning" by Aurélien Géron
- "Natural Language Processing with Transformers" by Lewis Tunstall
- "Designing Machine Learning Systems" by Chip Huyen

### Courses
- DeepLearning.AI - LangChain for LLM Application Development
- Fast.ai - Practical Deep Learning
- Hugging Face NLP Course

## 👤 Author

**Ratna Kumar**
- Role: Senior DevOps Engineer
- Focus: ML/AI for DevOps Automation & AIOps
- Expertise: Kubernetes, Istio, Orleans, MLOps
- GitHub: [@RatnaKumarTR](https://github.com/RatnaKumarTR)
- LinkedIn: [Connect with me](https://www.linkedin.com/in/ratnakumar)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with guidance from industry best practices in MLOps and AIOps
- Inspired by modern DevOps automation and AI-assisted troubleshooting patterns
- Uses open-source LLMs for cost-effective, privacy-preserving deployment
- Designed for real-world enterprise Kubernetes environments

## 📞 Support

For questions, issues, or feature requests:
- Open an issue on GitHub
- Contact: [your-email@example.com]

---

**⭐ If you find this project helpful, please consider giving it a star!**
