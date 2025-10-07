# 📚 Day 2: ML Fundamentals & First Code

**Date**: October 8, 2025  
**Focus**: Understanding ML basics + First hands-on experiments  
**Time**: 3-4 hours total  
**Goal**: Learn core concepts and train your first model

---

## 🎯 Learning Objectives

By end of Day 2, you will:
- ✅ Understand what Machine Learning is (and isn't)
- ✅ Know the difference between regression and classification
- ✅ Understand bias/variance tradeoff
- ✅ Read and interpret a confusion matrix
- ✅ Have collected real Kubernetes logs
- ✅ Trained your first ML classifier
- ✅ Seen an LLM explain a K8s error

---

## 📅 Hour-by-Hour Schedule

### **Morning Session: Theory (1.5 hours)**

#### **Phase 1: ML Fundamentals (45 minutes)**

**9:00 - 9:06** | Watch: [Machine Learning Fundamentals: Bias and Variance](https://www.youtube.com/watch?v=EuBBz3bI-aA)
- **Key Concepts**: Underfitting vs Overfitting
- **DevOps Application**: Model that's too simple vs too complex for log classification
- **Take Notes**: What is bias? What is variance?

**9:06 - 9:15** | Watch: [The Confusion Matrix](https://www.youtube.com/watch?v=Kdsp6soqA7o)
- **Key Concepts**: True Positives, False Positives, True Negatives, False Negatives
- **DevOps Application**: How many real errors did we catch? How many false alarms?
- **Take Notes**: Precision vs Recall - which matters more for security alerts?

**9:15 - 9:21** | Watch: [Cross Validation](https://www.youtube.com/watch?v=fSytzGwwBVw)
- **Key Concepts**: Training set vs Test set
- **DevOps Application**: Don't test on the same logs you trained on!
- **Take Notes**: Why do we need to split data?

**9:21 - 9:45** | Read: Hands-On ML Chapter 1 (skim, focus on key concepts)
- What is Machine Learning?
- Types of ML: Supervised, Unsupervised, Reinforcement
- Main challenges: Overfitting, Underfitting, Bad data
- Testing and Validating
- **Skip**: Heavy math sections, just understand concepts

#### **Phase 2: Simple Models (45 minutes)**

**9:45 - 9:54** | Watch: [Linear Regression, Clearly Explained](https://www.youtube.com/watch?v=nk2CQITm_eo)
- **Key Concepts**: Predicting continuous values
- **DevOps Application**: Predict CPU usage, memory consumption
- **Take Notes**: When to use linear regression?

**9:54 - 10:03** | Watch: [Logistic Regression, Clearly Explained](https://www.youtube.com/watch?v=yIYKR4sgzI8)
- **Key Concepts**: Predicting categories (yes/no, ERROR/WARNING/INFO)
- **DevOps Application**: Classify log severity
- **Take Notes**: Difference between linear and logistic regression

**10:03 - 10:30** | Read: Hands-On ML Chapter 4 - Linear Models section
- How models learn from data
- Loss functions and optimization
- Regularization basics
- **Skip**: Advanced math, focus on intuition

**10:30 - 10:35** | Break & Reflect
- Review your notes
- Think: How would you classify logs in your QA namespace?
- What features would you use? (keywords, timestamp, pod name?)

---

### **Afternoon Session: Hands-On (1.5-2 hours)**

#### **Phase 3: Setup & First Experiments (90 minutes)**

**11:00 - 11:10** | Download LLM Model
```bash
cd ~/devops-copilot-ml
source venv/bin/activate

# Download llama3.1:8b (this takes 5-10 minutes, ~4.7GB)
ollama pull llama3.1:8b

# Verify
ollama list

# Quick test
ollama run llama3.1:8b "What is a Kubernetes pod?"
# Press Ctrl+D to exit
```

**11:10 - 11:25** | Run: Simple Log Collection Test
```bash
# Run the log collector
python src/collectors/simple_log_test.py

# You should see:
# - List of pods from your QA namespace
# - Pod names, status, namespace
# - Data saved to DataFrame
```

**11:25 - 12:10** | Jupyter Notebook: First ML Experiment
```bash
# Start Jupyter
jupyter notebook

# Open: notebooks/day2_first_experiment.ipynb
# Follow the notebook step-by-step:
# 1. Create sample log dataset
# 2. Extract features from logs
# 3. Train logistic regression classifier
# 4. Understand confusion matrix
# 5. Make predictions on new logs
```

**12:10 - 12:25** | Run: Test Ollama with K8s Error
```bash
# Test LLM with a real K8s error
python src/rag/test_ollama.py

# You should see:
# - Sample K8s error log
# - LLM's explanation of the error
# - Suggested solutions
```

**12:25 - 12:30** | Review & Celebrate! 🎉
- You've trained your first ML model!
- You've seen an LLM explain a K8s error!
- You understand the basics of ML!

---

## 📖 Learning Resources

### **StatQuest Videos (YouTube)**
All videos by Josh Starmer - simple, clear explanations

1. [Bias and Variance](https://www.youtube.com/watch?v=EuBBz3bI-aA) - 6 min
2. [Confusion Matrix](https://www.youtube.com/watch?v=Kdsp6soqA7o) - 9 min
3. [Cross Validation](https://www.youtube.com/watch?v=fSytzGwwBVw) - 6 min
4. [Linear Regression](https://www.youtube.com/watch?v=nk2CQITm_eo) - 9 min
5. [Logistic Regression](https://www.youtube.com/watch?v=yIYKR4sgzI8) - 9 min

**Total Video Time**: 39 minutes

### **Reading Material**
- Hands-On Machine Learning (Aurélien Géron)
  - Chapter 1: The Machine Learning Landscape (skim - 20 min)
  - Chapter 4: Training Models - Linear Models section (20 min)

**Total Reading Time**: 40 minutes

---

## 🎓 Key Concepts to Master

### **1. Bias vs Variance**
```
High Bias (Underfitting):
- Model too simple
- Doesn't capture patterns
- Example: Classifying all logs as "INFO"

High Variance (Overfitting):
- Model too complex
- Memorizes training data
- Example: Model that only works on logs it's seen before

Goal: Balance between bias and variance
```

### **2. Confusion Matrix**
```
                Predicted
                ERROR  INFO
Actual ERROR    [TP]   [FN]
       INFO     [FP]   [TN]

TP (True Positive): Correctly identified errors
FP (False Positive): False alarms
TN (True Negative): Correctly identified normal logs
FN (False Negative): Missed errors (dangerous!)

Precision = TP / (TP + FP)  # Of predicted errors, how many were real?
Recall = TP / (TP + FN)     # Of real errors, how many did we catch?
```

### **3. Linear vs Logistic Regression**
```
Linear Regression:
- Predicts continuous values
- Example: Predict CPU usage (0-100%)
- Output: Any number

Logistic Regression:
- Predicts categories
- Example: Classify log severity (ERROR/WARNING/INFO)
- Output: Probability (0-1), then threshold to category
```

### **4. Training vs Testing**
```
Why split data?

Training Set (80%):
- Model learns patterns from this data
- Adjusts weights to minimize errors

Test Set (20%):
- Model has never seen this data
- Measures real-world performance
- Prevents overfitting

Never test on training data!
```

---

## 💻 Code You'll Run Today

### **File 1: `src/collectors/simple_log_test.py`**
```python
# What it does:
# - Connects to your K8s cluster
# - Lists pods in QA namespace
# - Collects basic pod information
# - Saves to pandas DataFrame

# Expected output:
# DataFrame with columns: pod_name, status, namespace, timestamp
```

### **File 2: `notebooks/day2_first_experiment.ipynb`**
```python
# What you'll learn:
# 1. Create synthetic log dataset
# 2. Extract features (word count, keywords, etc.)
# 3. Split into train/test sets
# 4. Train logistic regression
# 5. Make predictions
# 6. Evaluate with confusion matrix

# Expected result:
# A working classifier that predicts log severity!
```

### **File 3: `src/rag/test_ollama.py`**
```python
# What it does:
# - Takes a sample K8s error log
# - Sends to Ollama LLM
# - Gets explanation and solutions

# Expected output:
# LLM explains the error in plain English
# Suggests troubleshooting steps
```

---

## ✅ Success Criteria

By end of Day 2, you should be able to:

### **Theoretical Understanding**
- [ ] Explain bias vs variance in your own words
- [ ] Interpret a confusion matrix
- [ ] Know when to use linear vs logistic regression
- [ ] Understand why we split data into train/test sets

### **Practical Skills**
- [ ] Collected logs from K8s cluster
- [ ] Created a simple dataset
- [ ] Trained a logistic regression model
- [ ] Made predictions on new data
- [ ] Evaluated model with confusion matrix
- [ ] Used Ollama to explain a K8s error

### **DevOps Application**
- [ ] Can think about log classification features
- [ ] Understand model evaluation in production context
- [ ] See how LLMs can help with troubleshooting

---

## 🚧 Common Challenges & Solutions

### **Challenge 1: "I don't understand the math"**
**Solution**: Focus on intuition, not formulas
- You don't need to derive equations
- Understand what the model does, not how it calculates
- The libraries handle the math for you

### **Challenge 2: "My model accuracy is low"**
**Solution**: That's normal for Day 2!
- 60-70% accuracy is fine for first attempt
- You'll improve with feature engineering (later)
- Focus on understanding, not perfect results

### **Challenge 3: "Ollama is slow"**
**Solution**: First run is always slower
- Model loads into memory first time
- Subsequent runs are faster
- Be patient, it's running locally

### **Challenge 4: "K8s connection fails"**
**Solution**: Check your kubeconfig
```bash
# Verify K8s access
kubectl get pods -n 207804-confirmation-qa

# If fails, check config
kubectl config current-context
```

---

## 📝 Notes Template

Use this template while learning:

```markdown
# Day 2 Learning Notes

## Bias vs Variance
- Bias means: ___
- Variance means: ___
- In log classification: ___

## Confusion Matrix
- True Positive: ___
- False Positive: ___
- For security alerts, I care more about: ___ (precision/recall)

## Linear vs Logistic Regression
- Use Linear when: ___
- Use Logistic when: ___
- For log classification, I'll use: ___

## My First Model Results
- Accuracy: ___%
- Precision: ___%
- Recall: ___%
- What surprised me: ___
- What I'll improve: ___

## Questions for Tomorrow
1. ___
2. ___
3. ___
```

---

## 🎯 End of Day Checklist

- [ ] Watched all 5 StatQuest videos (39 min)
- [ ] Read Hands-On ML chapters (40 min)
- [ ] Downloaded llama3.1:8b model
- [ ] Ran simple_log_test.py successfully
- [ ] Completed day2_first_experiment.ipynb
- [ ] Tested Ollama with K8s error
- [ ] Took notes on key concepts
- [ ] Can explain bias/variance to someone
- [ ] Understand confusion matrix
- [ ] Excited about Day 3! 🚀

---

## 🚀 What's Next: Day 3

**Tomorrow's Focus**: Decision Trees & Better Classification

**You'll Learn**:
- How decision trees work
- Random Forests for better accuracy
- Feature importance
- Improve your log classifier

**You'll Build**:
- Better log classifier with decision trees
- Feature importance analysis
- Model comparison (Logistic vs Tree vs Forest)

**Time**: 3-4 hours

---

## 💡 Tips for Success

1. **Don't Rush**: Understanding > Speed
2. **Take Breaks**: 25 min work, 5 min break
3. **Ask Questions**: Write them down for later
4. **Experiment**: Change code, see what happens
5. **Have Fun**: ML is powerful and exciting!

---

**Remember**: You're not trying to become an ML expert in one day. You're building practical skills for DevOps. Focus on understanding concepts and how to apply them to real problems.

**You've got this! 💪**

---

**Previous**: [Day 1 Setup Complete](DAY1_SETUP_COMPLETE.md)  
**Next**: Day 3 Plan (will be created tomorrow)
