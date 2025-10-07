# Day 1 Learning Guide - ML Fundamentals & Environment Setup

## 🎯 Learning Objectives

By the end of Day 1, you will understand:
1. What Machine Learning is and how it works
2. Key ML concepts (supervised/unsupervised learning, training, evaluation)
3. How Large Language Models (LLMs) work
4. Neural networks basics
5. Your development environment setup

---

## 📚 Required Learning Materials (4-5 hours total)

### Part 1: Introduction to Machine Learning (1.5 hours)

#### Watch: 3Blue1Brown - Neural Networks Series
**Link:** Search YouTube for "3Blue1Brown Neural Networks"

**Videos to watch:**
1. "But what is a neural network?" (20 min)
2. "Gradient descent, how neural networks learn" (20 min)
3. "What is backpropagation really doing?" (15 min)

**Key Concepts to Understand:**
- What is a neuron and how does it work?
- What are weights and biases?
- How does gradient descent optimize the network?
- What is backpropagation?

**Notes Template:**
```
Neural Networks Basics:
- Neuron: _______________________________________________
- Activation Function: ___________________________________
- Weights: ______________________________________________
- Bias: _________________________________________________
- Forward Pass: _________________________________________
- Backward Pass (Backpropagation): ______________________
```

---

### Part 2: Large Language Models (1 hour)

#### Watch: Andrej Karpathy - "Intro to Large Language Models"
**Link:** Search YouTube for "Andrej Karpathy LLM intro"

**Duration:** ~1 hour

**Key Concepts to Understand:**
- What are LLMs and how do they work?
- What is a transformer architecture?
- What are tokens and embeddings?
- How does training work?
- What are the limitations of LLMs?
- What is fine-tuning vs prompting?

**Notes Template:**
```
LLM Fundamentals:
- Token: ________________________________________________
- Embedding: ____________________________________________
- Transformer: __________________________________________
- Attention Mechanism: __________________________________
- Context Window: _______________________________________
- Temperature: __________________________________________
- Top-p/Top-k Sampling: _________________________________
```

---

### Part 3: Reading - ML Concepts (1.5 hours)

#### Book: "Hands-On Machine Learning" by Aurélien Géron

**Chapters to Read:**
1. **Chapter 1: The Machine Learning Landscape** (30 min)
   - Types of ML systems
   - Main challenges of ML
   - Testing and validating

2. **Chapter 2: End-to-End ML Project** (60 min)
   - Working with real data
   - Data exploration
   - Preparing data for ML
   - Training and evaluating models

**Key Concepts:**
```
ML System Types:
□ Supervised Learning: _________________________________
□ Unsupervised Learning: _______________________________
□ Reinforcement Learning: ______________________________

ML Workflow:
1. Define the problem: _________________________________
2. Get the data: _______________________________________
3. Explore the data: ___________________________________
4. Prepare the data: ___________________________________
5. Train models: _______________________________________
6. Evaluate models: ____________________________________
7. Deploy and monitor: _________________________________

Common Challenges:
□ Overfitting: _________________________________________
□ Underfitting: ________________________________________
□ Data quality issues: _________________________________
□ Insufficient training data: ___________________________
```

---

### Part 4: Practical - Python ML Libraries (1 hour)

#### Interactive Tutorial: Scikit-learn Basics

**Create a notebook:** `notebooks/00_ml_basics.ipynb`

```python
# Cell 1: Import libraries
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score
import matplotlib.pyplot as plt

print("Libraries imported successfully!")

# Cell 2: Create sample dataset
# Simulate CPU usage prediction
np.random.seed(42)
n_samples = 100

# Features: hour of day, day of week, number of pods
X = np.random.rand(n_samples, 3) * 100
# Target: CPU usage percentage
y = 20 + 0.5 * X[:, 0] + 0.3 * X[:, 1] + 0.2 * X[:, 2] + np.random.randn(n_samples) * 5

print(f"Dataset shape: X={X.shape}, y={y.shape}")

# Cell 3: Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

print(f"Training set: {X_train.shape}")
print(f"Test set: {X_test.shape}")

# Cell 4: Train model
model = LinearRegression()
model.fit(X_train, y_train)

print("Model trained!")
print(f"Coefficients: {model.coef_}")
print(f"Intercept: {model.intercept_}")

# Cell 5: Make predictions
y_pred = model.predict(X_test)

# Cell 6: Evaluate model
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f"Mean Squared Error: {mse:.2f}")
print(f"R² Score: {r2:.2f}")

# Cell 7: Visualize results
plt.figure(figsize=(10, 6))
plt.scatter(y_test, y_pred, alpha=0.5)
plt.plot([y_test.min(), y_test.max()], [y_test.min(), y_test.max()], 'r--', lw=2)
plt.xlabel('Actual CPU Usage')
plt.ylabel('Predicted CPU Usage')
plt.title('CPU Usage Prediction - Actual vs Predicted')
plt.tight_layout()
plt.savefig('data/ml_basics_prediction.png')
plt.show()

print("Visualization saved!")
```

**Exercise Questions:**
1. What does the R² score tell you about the model?
2. What would happen if you increased the test_size to 0.5?
3. How would you improve this model?

---

## 🛠️ Practical Setup Tasks

### Task 1: Install Dependencies (30 min)

```bash
# Activate virtual environment
source venv/bin/activate

# Upgrade pip
pip install --upgrade pip

# Install requirements (this will take 10-15 minutes)
pip install -r requirements.txt

# Verify installations
python -c "import numpy; print(f'NumPy: {numpy.__version__}')"
python -c "import pandas; print(f'Pandas: {pandas.__version__}')"
python -c "import sklearn; print(f'Scikit-learn: {sklearn.__version__}')"
python -c "import langchain; print(f'LangChain: {langchain.__version__}')"
```

### Task 2: Install Ollama (15 min)

```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Verify installation
ollama --version

# Download Llama 3.1 8B model (this will take 10-15 minutes, ~4.7GB)
ollama pull llama3.1:8b

# Test the model
ollama run llama3.1:8b "Explain what DevOps is in one sentence"
```

### Task 3: Verify Kubernetes Access (5 min)

```bash
# Configure kubectl
aws eks --region us-east-1 update-kubeconfig --name a208234-preprod-confirm-ot-useast1-plexus-cluster

# Verify access
kubectl get pods -n 207804-confirmation-qa

# Check if you can see logs
kubectl logs -n 207804-confirmation-qa <pod-name> --tail=10
```

---

## ✅ Day 1 Completion Checklist

### Learning
- [ ] Watched 3Blue1Brown neural networks videos
- [ ] Watched Andrej Karpathy LLM introduction
- [ ] Read "Hands-On ML" Chapters 1-2
- [ ] Completed ML basics notebook
- [ ] Understand key ML concepts

### Setup
- [ ] Created project structure
- [ ] Created .gitignore
- [ ] Created README.md
- [ ] Created requirements.txt
- [ ] Installed Python dependencies
- [ ] Installed Ollama
- [ ] Downloaded Llama 3.1 model
- [ ] Verified Kubernetes access

### Understanding Check
Answer these questions to verify your understanding:

1. **What is the difference between supervised and unsupervised learning?**
   ```
   Your answer:
   
   
   ```

2. **What is overfitting and how can you prevent it?**
   ```
   Your answer:
   
   
   ```

3. **How do LLMs generate text?**
   ```
   Your answer:
   
   
   ```

4. **What is RAG (Retrieval Augmented Generation)?**
   ```
   Your answer:
   
   
   ```

5. **Why are we using DuckDB instead of PostgreSQL for this project?**
   ```
   Your answer:
   
   
   ```

---

## 📖 Additional Resources (Optional)

### For Deeper Understanding:
1. **StatQuest with Josh Starmer** (YouTube)
   - "Machine Learning Fundamentals" playlist
   - Great for visual learners

2. **Fast.ai Course** (Free)
   - "Practical Deep Learning for Coders"
   - Hands-on approach

3. **Hugging Face NLP Course** (Free)
   - Chapter 1: Transformer Models
   - Interactive and practical

### For DevOps + ML:
1. **"Machine Learning for DevOps"** - Blog series
2. **MLOps.community** - Best practices and case studies
3. **Weights & Biases** - MLOps tutorials

---

## 🎯 Tomorrow's Preview (Day 2)

Tomorrow we'll build the Kubernetes log collector:
- Connect to EKS cluster
- Collect logs from QA namespace
- Parse and store logs in DuckDB
- Create initial data exploration notebook

**Preparation:**
- Review Kubernetes Python client documentation
- Understand DuckDB basics
- Think about what log patterns you want to detect

---

## 💡 Tips for Success

1. **Don't rush** - Understanding concepts is more important than speed
2. **Take notes** - Write down key concepts in your own words
3. **Ask questions** - If something is unclear, research it
4. **Practice** - Run the code examples and modify them
5. **Connect to your work** - Think about how ML can solve your DevOps problems

---

## 📝 Daily Log Template

```markdown
# Day 1 - [Date]

## What I Learned
1. 
2. 
3. 

## What I Built
1. 
2. 
3. 

## Challenges Faced
1. 
2. 

## Questions for Tomorrow
1. 
2. 

## Time Spent
- Learning: ___ hours
- Coding: ___ hours
- Setup: ___ hours
- Total: ___ hours
```

---

**Remember:** This is a marathon, not a sprint. Take your time to understand the concepts deeply. The goal is not just to build a project, but to truly understand ML and be able to apply it to other problems in your DevOps work.

Good luck! 🚀
