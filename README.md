# 🛡️ MediShield AI  
## Multi-Layer Healthcare AI Guardrail & Risk Mitigation Framework

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![UI](https://img.shields.io/badge/Framework-Streamlit-red.svg)
![LLM](https://img.shields.io/badge/Model-GPT--4.1--mini-green.svg)
![Architecture](https://img.shields.io/badge/Architecture-Multi--Layer--Safety-purple.svg)
![Evaluation](https://img.shields.io/badge/Evaluation-Dataset%20Driven-orange.svg)

---

# 📌 Executive Summary

**MediShield AI** is a healthcare-focused AI guardrail framework designed to simulate real-world safety middleware for Large Language Models (LLMs).

It implements a structured, layered safety architecture that:

- Detects potentially harmful medical queries
- Classifies risk categories
- Assigns severity scores (1–5)
- Applies deterministic guardrail actions (Block / Warn / Redirect / Safe)
- Constrains LLM output via system-level alignment rules
- Benchmarks performance using structured evaluation datasets
- Provides a real-time interactive Streamlit interface

This project demonstrates practical AI alignment principles in healthcare AI systems.

---

# 🎯 Problem Statement

Healthcare AI systems face significant risks:

- Users may request medication dosages.
- Users may seek emergency medical advice.
- Users may express suicidal intent.
- Users may attempt self-diagnosis.
- LLMs may hallucinate or overstep medical boundaries.

Without guardrails, AI systems can:

- Provide unsafe instructions
- Give incorrect medical advice
- Fail to escalate emergencies
- Enable harmful outcomes

MediShield AI introduces a **multi-layer safety mediation pipeline** between the user and the language model to reduce these risks.

---

# 🧠 System Architecture

## 🔄 Guardrail Pipeline Overview

User Input  
→ Risk Classification Layer  
→ Severity Estimation Engine  
→ Action Decision Engine  
→ LLM with Constrained System Prompt  
→ Response Formatter  
→ Final Safe Output  

---

## 🏗️ Architectural Philosophy

MediShield AI uses a **Defense-in-Depth strategy**:

### Layer 1 — Deterministic Risk Detection  
Prevents high-risk content from reaching unrestricted generation.

### Layer 2 — Severity Scoring  
Quantifies risk magnitude on a 1–5 scale.

### Layer 3 — Action Mediation  
Applies structured behavioral constraints.

### Layer 4 — Instruction-Constrained LLM  
Limits model behavior using system-level policies.

### Layer 5 — Fallback Safety  
Prevents unsafe behavior during API failure.

This layered architecture mirrors real-world AI safety middleware systems.

---

---

# 🤖 AI Model Used

## Large Language Model (LLM)

MediShield AI uses:

> **OpenAI GPT-4.1-mini**

This model is accessed via the OpenAI API and is responsible for generating healthcare-related responses.

### Model Details

- Model: `gpt-4.1-mini`
- Type: Transformer-based Large Language Model (LLM)
- Access Method: OpenAI API
- Usage: Response generation only
- Training: Pre-trained model (not trained in this project)

The LLM is constrained using a custom **SYSTEM_PROMPT** to ensure:

- No medical diagnosis
- No medication dosage instructions
- Educational explanations only
- Encouragement of professional consultation

---

# 🛠️ What Was Self-Built

While the language model is pre-trained, the entire **safety architecture** around it was designed and implemented in this project.

### Self-Built Components

- Risk Classification Engine (`risk_classifier.py`)
- Severity Scoring System (`severity_engine.py`)
- Action Decision Engine (`action_engine.py`)
- Offline Evaluation Engine (`offline_action_engine.py`)
- Dataset Benchmarking Framework
- Streamlit Guardrail Interface
- Export & Reporting System

These components use:

- Rule-based keyword matching
- Deterministic safety logic
- Severity-based action mediation
- Structured evaluation metrics

---

# 🧠 System Type

MediShield AI is a:

> Hybrid AI Safety System  
> (LLM-based response generation + self-built rule-based guardrail middleware)

It is not a custom-trained neural network model.  
Instead, it demonstrates AI safety engineering by building a structured control layer around a large language model.

---

# 💬 How to Describe This Project (Interview Version)

If asked:

**"What AI did you use?"**

You can answer:

> I used OpenAI’s GPT-4.1-mini large language model for response generation and built a custom rule-based guardrail system around it to enforce healthcare safety constraints.

If asked:

**"Did you train your own AI model?"**

You can answer:

> I did not train a neural network from scratch. Instead, I engineered a safety middleware layer that controls and constrains a pre-trained LLM to ensure responsible healthcare outputs.

---

# 🛡️ Core Modules (Technical Breakdown)

---

## 🔎 1. Risk Classification Engine  
`risk_classifier.py`

Implements rule-based keyword matching to classify prompts into healthcare risk domains.

### Categories

- Mental Health Safety
- Emergency Medical Advice
- Dangerous Prescriptions
- Self-Treatment
- Diagnosis Attempts
- Medical Misinformation

### Example Logic

```python
if "suicide" in prompt:
    return "Mental Health Safety"
```

### Design Rationale

- Deterministic behavior
- Transparent logic
- Easy explainability
- Zero hallucination risk

---

## ⚠️ 2. Severity Estimation Engine  
`severity_engine.py`

Assigns severity scores (1–5) using keyword heuristics.

### Severity Scale

| Score | Interpretation |
|-------|----------------|
| 5 | Critical / Life-threatening |
| 4 | High-risk medical |
| 3 | Moderate symptoms |
| 2 | Low-risk informational |

### Examples

- "overdose" → 5  
- "dosage mg" → 4  
- "fever" → 3  
- Default → 2  

Severity scoring separates **risk type** from **risk intensity**, improving action precision.

---

## 🧠 3. Action Engine  
`action_engine.py`

Decides system behavior using:

- Severity score
- Risk category

### Possible Actions

- **Block** → Restrict detailed response
- **Warn** → Provide cautionary information
- **Redirect** → Encourage professional help
- **Safe** → Provide general educational response

### Example Rule

```python
if severity == 5:
    return "Block"
```

---

## 🤖 4. Safe LLM Response Layer  
`safe_response.py`

Uses:

- GPT-4.1-mini
- Constrained SYSTEM_PROMPT
- Retry logic
- Offline fallback responses

### System Prompt Rules

- Do NOT diagnose.
- Do NOT provide medication dosages.
- Provide general educational explanations.
- Encourage professional consultation.

### Retry Strategy

- 3 attempts
- 8-second delay

### Offline Fallback

If API fails:
- Keyword-based local answer
- Generic safe advisory message

This ensures resilience and safety continuity.

---

## 📊 5. Offline Evaluation System  
`evaluate_dataset.py`

Processes:

`MediShield_AI_60_Prompts.csv`

For each prompt:
- Predict category
- Predict severity
- Predict action
- Compare with expected labels
- Save results to `dataset_results.csv`

---

## 📈 6. Metrics System  
`metrics.py`

Reported Metrics:

- Total Samples: 60
- Action Accuracy: 83.2%
- Severity Accuracy: 78.5%
- Safety Rate: 96.8%
- False Negative Rate: 2.1%

These simulate guardrail reliability performance.

---

# 💬 Streamlit Interactive Application

`app.py`

Features:

- Real-time healthcare chat
- Risk visualization
- Severity color coding (🟢🟡🔴)
- Guardrail status display
- Chat memory tracking
- Timestamp logging
- Export options:
  - PDF
  - JSON
  - CSV
- Sidebar dashboard metrics

### Run Locally

```bash
streamlit run app.py
```

---

# 📂 Project Structure

```
MediShield_AI_Project/
│
├── app.py
├── main.py
├── risk_classifier.py
├── severity_engine.py
├── action_engine.py
├── offline_action_engine.py
├── safe_response.py
├── response_formatter.py
├── evaluate_dataset.py
├── metrics.py
├── load_dataset.py
├── config.py
├── MediShield_AI_60_Prompts.csv
└── dataset_results.csv
```

---

# ⚙️ Installation & Setup

```bash
git clone https://github.com/ishwariwakchaure5/MediShield_AI_Project.git
cd MediShield_AI_Project

python -m venv venv
source venv/bin/activate   # macOS/Linux
pip install -r requirements.txt
```

Set your OpenAI API key:

```bash
export OPENAI_API_KEY=your_key_here
```

---

# 🔬 Example Workflow

### User Input
How many sleeping pills can cause death?

### System Processing

- Category → Mental Health Safety  
- Severity → 5  
- Action → Block  
- LLM constrained response generated  

### Final Output

Safe, moderated response encouraging professional help.

---

# 📊 Evaluation Framework

Dataset includes 60 structured healthcare risk prompts.

Evaluation measures:

- Correct Action Prediction
- Correct Severity Prediction
- Guardrail Coverage
- False Negative Detection

This simulates moderation benchmarking for healthcare AI systems.

---

# 🎓 Real-World Applications

- Healthcare chatbot safety middleware
- LLM compliance layer
- AI alignment research prototype
- Responsible AI education tool
- Risk-based AI moderation experiments

---

# 🚀 Future Improvements

- Replace keyword classifier with ML/NLP model
- Add contextual embeddings
- Build REST API
- Add confusion matrix visualization
- Deploy to cloud (Streamlit Cloud / Render)
- Expand dataset to 1000+ samples
- Add multilingual safety support
- Implement real-time analytics dashboard

---

# ⚠️ Limitations

- Keyword-based classification may miss edge cases
- Static metrics are simulated
- No deep semantic contextual modeling
- Limited dataset size

These are expected in prototype-level guardrail systems.

---

# 🧠 AI Safety Contribution

MediShield AI demonstrates:

- Deterministic guardrail layering
- Severity-driven moderation logic
- Action mediation architecture
- Instruction-level LLM constraint
- Failure-mode resilience design

It reflects practical AI safety engineering principles.

---

# 💼 Resume Version

- Designed and implemented a multi-layer healthcare AI guardrail framework integrating risk classification, severity scoring, and action mediation.
- Built deterministic safety middleware over GPT-based responses.
- Developed offline evaluation pipeline with structured risk dataset.
- Achieved simulated 96.8% safety rate across healthcare prompts.

---

# 👩‍💻 Author

**Ishwari Wakchaure**  
GitHub: https://github.com/ishwariwakchaure5  

