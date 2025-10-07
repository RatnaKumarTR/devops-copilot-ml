# Day 1: Setup & Installation

**Date**: October 7, 2025

## What I Did

- Set up Python 3.12 virtual environment
- Installed all 49 required packages (NumPy, Pandas, PyTorch, LangChain, etc.)
- Fixed dependency issues (torch, duckdb, httpx versions)
- Installed Ollama 0.12.3 with GPU support
- Downloaded llama3.1:8b model (4.7GB)
- Created project structure and documentation

## What I Learned

**Python Package Management**:
- Virtual environments prevent dependency conflicts
- Python 3.12 requires specific package versions
- Pre-built wheels install much faster than compiling from source

**Key Challenges Solved**:
- PyTorch 2.1.2 → 2.8.0 (Python 3.12 compatibility)
- DuckDB 0.9.2 → 1.4.1 (no wheels for 3.12, needed latest)
- httpx version conflict with Ollama (fixed with <0.26.0,>=0.25.2)

**Local LLM Setup**:
- Ollama runs LLMs locally without cloud dependencies
- GPU acceleration works automatically with Nvidia
- llama3.1:8b is suitable for development (4.7GB)

## Next

**Day 2 Focus**: ML Fundamentals
- Watch StatQuest videos (Bias/Variance, Confusion Matrix, Cross Validation)
- Read Hands-On ML Chapter 1
- Understand evaluation metrics for log classification
