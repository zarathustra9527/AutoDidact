# **AutoDidact: Bootstrapping Search Through Self-Verification**

**Research exploring how small LLMs can autonomously enhance their own research and reasoning capabilities by generating, researching, and answering self-created question-answer pairs, learning agentic search via reinforcement learning. All running on a single RTX 4090!**

**Credits:** This project was built using [Unsloth's Efficient GRPO code](https://unsloth.ai/blog/r1-reasoning), and adds support for function calling and agentic loops.

---

## 🚀 **Key Features**

- **Self-Bootstrapping with Llama-8B:** Llama-8B autonomously generates meaningful question-answer pairs from documents, then trains itself to search the corpus effectively to answer these self-generated questions.
- **Autonomous Self-Verification:** Llama-8B evaluates the accuracy of its own answers, creating a self-improving feedback loop.
- **GRPO Reinforcement Learning:** Implements Group Relative Policy Optimization (GRPO) to refine Llama-8B’s ability to research, search, and reason effectively.
- **Fully Autonomous Open-Source Pipeline:**
  Every step, including question generation, answer research, verification, embedding creation, and reinforcement learning, runs locally using open-source models.

---
## 📊 **Demonstrated Results**

After just **100 steps of GRPO training** (1 hour on a single RTX 4090 GPU), Llama-8B significantly improved its ability to research and answer questions from the Apollo 13 mission report.

On a validation set of 68 questions, **accuracy more than doubled from 23% to 59%**.

---

## 🔍 **Example: Adaptive Search Trajectory**

At the start of training, the model frequently **misused the search tool**, often:

- Formatting tool calls incorrectly.
- Hallucinating responses instead of actually querying the corpus.
- Generating entire sequences where it **role-played both** the search engine and itself, responding to imaginary search results.

Through training, however, the model **learned to reason and search effectively**. It began issuing **well-formed queries**, refining its searches based on partial results, and successfully retrieving accurate answers.

The following example demonstrates this learned adaptive search behavior **after training**.

---

## 📈 **Quickstart**

### **Installation**

```bash
pip install -r requirements.txt
```

### **Data Generation & Training**

Begin by generating the embeddings, questions, and answers:

```bash
python generate_data.py  # Generate QA pairs and embeddings for your documents
```

Now, run `autodidact.ipynb` and watch your research agent learn!

---

## 🛠️ **Code Structure**

- **`generate_data.py`** – Automates QA pair generation and indexing.
- **`search_module.py`** – Enables semantic search over document corpus.
- **`embeddings.py`** – Manages document/query embedding generation.
- **`rl_helpers.py`** – Controls agent interactions and reward logic.
- **`autodidact.ipynb`** – Full training pipeline example.

---

## 🔬 **Customizing the Dataset**

Replace the existing Apollo 13 mission report (`data/mission_report.md`) with your own markdown file. Then, rerun:

```bash
python generate_data.py
```

This will generate new question-answer pairs and build a search index, allowing you to train a research agent on **any dataset**.

---
