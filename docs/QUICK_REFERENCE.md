# Quick Reference Guide - DevOps Copilot ML

## 🚀 Daily Commands

### Activate Environment
```bash
cd ~/devops-copilot-ml
source venv/bin/activate
```

### Run Ollama
```bash
# Start Ollama service (if not running)
ollama serve

# In another terminal, use the model
ollama run llama3.1:8b
```

### Kubernetes Commands
```bash
# Get pods in QA namespace
kubectl get pods -n 207804-confirmation-qa

# Get logs from a pod
kubectl logs -n 207804-confirmation-qa <pod-name> --tail=100

# Follow logs in real-time
kubectl logs -n 207804-confirmation-qa <pod-name> -f

# Get all pods with labels
kubectl get pods -n 207804-confirmation-qa --show-labels
```

### Git Commands
```bash
# Check status
git status

# Add and commit
git add .
git commit -m "Your message"

# Push to GitHub
git push origin main

# Pull latest changes
git pull origin main
```

---

## 📁 Project Structure Quick Reference

```
devops-copilot-ml/
├── src/
│   ├── collectors/     # K8s log collection
│   ├── processors/     # Log processing & classification
│   ├── rag/           # RAG & LLM integration
│   └── api/           # FastAPI endpoints
├── data/
│   ├── logs/          # DuckDB databases
│   ├── documentation/ # Knowledge base docs
│   └── models/        # Trained ML models
├── notebooks/         # Jupyter notebooks for analysis
├── tests/            # Unit tests
├── docs/             # Documentation
└── docker/           # Docker configurations
```

---

## 🔧 Common Tasks

### Start Jupyter Notebook
```bash
source venv/bin/activate
jupyter notebook
```

### Run Tests
```bash
pytest tests/ -v
pytest --cov=src tests/
```

### Format Code
```bash
black src/
isort src/
flake8 src/
```

### Run API Server
```bash
uvicorn src.api.main:app --reload
```

### Run Streamlit UI
```bash
streamlit run ui/app.py
```

---

## 🐛 Troubleshooting

### Virtual Environment Issues
```bash
# Deactivate and reactivate
deactivate
source venv/bin/activate

# Recreate if needed
rm -rf venv
python3.11 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Ollama Issues
```bash
# Check if Ollama is running
ps aux | grep ollama

# Restart Ollama
pkill ollama
ollama serve

# List downloaded models
ollama list

# Remove and re-download model
ollama rm llama3.1:8b
ollama pull llama3.1:8b
```

### Kubernetes Access Issues
```bash
# Reconfigure kubectl
aws eks --region us-east-1 update-kubeconfig --name a208234-preprod-confirm-ot-useast1-plexus-cluster

# Check current context
kubectl config current-context

# Test permissions
kubectl auth can-i get pods -n 207804-confirmation-qa
```

---

## 📚 Key Documentation Files

- `README.md` - Project overview and setup
- `docs/DAY1_LEARNING_GUIDE.md` - Day 1 learning materials
- `docs/SETUP_COMPLETE.md` - Setup completion guide
- `docs/QUICK_REFERENCE.md` - This file
- `requirements.txt` - Python dependencies

---

## 🔗 Important Links

### Documentation
- LangChain: https://python.langchain.com/docs/
- Ollama: https://ollama.com/library
- Scikit-learn: https://scikit-learn.org/stable/
- DuckDB: https://duckdb.org/docs/
- Kubernetes Python: https://github.com/kubernetes-client/python

### Learning Resources
- 3Blue1Brown Neural Networks: YouTube
- Andrej Karpathy LLM Intro: YouTube
- Hands-On Machine Learning: O'Reilly
- Fast.ai: https://course.fast.ai/
- Hugging Face NLP Course: https://huggingface.co/learn/nlp-course

---

## 💡 Pro Tips

1. **Always activate venv** before running Python commands
2. **Commit often** to track your progress
3. **Use Jupyter notebooks** for experimentation
4. **Test incrementally** - don't write too much code before testing
5. **Document as you go** - future you will thank you

---

## 📊 Progress Tracking

### Week 1 Checklist
- [ ] Day 1: Setup & ML Fundamentals
- [ ] Day 2: K8s Log Collection
- [ ] Day 3-4: Log Processing
- [ ] Day 5-7: ML Classification

### Week 2 Checklist
- [ ] LangChain & ChromaDB setup
- [ ] RAG implementation
- [ ] LLM integration
- [ ] Q&A system

### Week 3 Checklist
- [ ] FastAPI backend
- [ ] Streamlit UI
- [ ] Docker deployment
- [ ] Documentation

---

## 🎯 Daily Workflow

1. **Morning:**
   - Review yesterday's work
   - Check todo list
   - Plan today's tasks

2. **Development:**
   - Activate venv
   - Write code
   - Test frequently
   - Commit changes

3. **Evening:**
   - Review what you built
   - Update documentation
   - Plan tomorrow
   - Push to GitHub

---

## 📞 Getting Help

### When Stuck:
1. Check this quick reference
2. Review relevant documentation
3. Search Stack Overflow
4. Check GitHub issues
5. Ask in ML communities

### Useful Search Terms:
- "langchain [your question]"
- "ollama [your question]"
- "kubernetes python client [your question]"
- "duckdb [your question]"

---

**Keep this file handy - you'll reference it often!**
