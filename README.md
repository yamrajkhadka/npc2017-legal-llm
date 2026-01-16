# 🇳🇵 Nepal Legal Mistral-7B

> **An end-to-end, domain-specific Large Language Model for Nepalese law**, engineered from the *National Penal Code of Nepal (2017)* — from raw legal PDFs to deployable, quantized AI systems.

This project demonstrates how a **country-specific legal LLM** can be built **faithfully, transparently, and reproducibly**, without relying on generic web data or opaque pipelines.

---

## 🏗️ System Architecture

![System Architecture](https://github.com/yamrajkhadka/npc2017-legal-llm/blob/main/system-archi.png)

This diagram illustrates the **complete lifecycle** of the Nepal Legal LLM:
**official legal documents → structured dataset → fine-tuned model → real-world deployments**.

---

## 🔎 What This Project Is (and Is Not)

This is **not just a fine-tuned chatbot**.

It is a **full legal-LLM engineering pipeline**, designed to show how legally grounded AI systems can be created **from scratch**:

- 📄 Official government legal PDFs  
- 🧹 Faithful text extraction (no summaries, no hallucination)  
- 🧩 Hierarchical legal chunking (Part → Chapter → Section → Subsection)  
- 🏷️ Deterministic chunk IDs for traceability  
- 🧠 Instruction-tuning dataset generation  
- 🔥 Fine-tuning **Mistral-7B** for legal reasoning  
- ⚡ Quantization for low-resource inference  
- 🌐 Live deployments (UI + API)

The entire pipeline is **auditable, reproducible, and legally faithful**.

---

## 🚀 Live Systems

### 🖥️ Interactive Web Apps

| Deployment | Description | Link |
|----------|------------|------|
| **Full-Precision Assistant** | Accurate legal reasoning | https://huggingface.co/spaces/yamraj047/penal-legal-assistant |
| **Fast API Version** | Optimized backend inference | https://huggingface.co/spaces/yamraj047/nepal-legal-assistant-fast |
| **GGUF Quantized Assistant** | Runs on low-RAM machines | https://huggingface.co/spaces/yamraj047/Nepall-legal-assist |

---

## 🤗 Models

| Model | Format | Size | Link |
|------|-------|------|------|
| Nepal Legal Mistral-7B | FP16 | ~13.5 GB | https://huggingface.co/yamraj047/nepal-legal-mistral-7b |
| Nepal Legal Mistral-7B | GGUF (Q4_K_M) | **4.07 GB** | https://huggingface.co/yamraj047/nepal-legal-mistral-7b-GGUF |

---

## 🚀 Run Nepal Legal Mistral-7B Locally (FP16)

Run the **full-precision model locally** using Hugging Face `transformers`.

### 📦 Requirements
- Python **3.9+**
- **16 GB RAM minimum** (CPU works, GPU optional)
- Disk space: **~14 GB**



---

> ## 🔧 Installation
>
> ```bash
> pip install transformers torch accelerate sentencepiece
> ```

---

> ## ▶️ Run the Model (Interactive – Terminal)
>
> ```bash
> python3 -c "from transformers import pipeline; p=pipeline('text-generation','yamraj047/nepal-legal-mistral-7b'); print(p(input('Q: '), max_new_tokens=300)[0]['generated_text'])"
> ```
>
> **Example:**
> ```text
> Q: Explain Article 20 of the Constitution of Nepal
> ```
>
> Press **Enter** to receive the answer.
>
> ⚠️ First run will download ~13.5 GB and may be slow on CPU systems.

---

##🚀 Run GGUF Model Locally (4GB - CPU Optimized)

The quantized GGUF model runs efficiently on CPU with minimal memory requirements.

###📦 Requirements

-Python 3.9+
-8 GB RAM minimum (CPU only, no GPU needed)
-Disk space: ~4.5 GB
---

> ## 🔧 Installation

Step 1: Create and activate virtual environment

bash
python3 -m venv legal-env
source legal-env/bin/activate
Step 2: Install dependencies

bash
pip install llama-cpp-python huggingface-hub
Step 3: Run the model (one-liner)

bash
python3 -c "from llama_cpp import Llama; from huggingface_hub import hf_hub_download; m=Llama(hf_hub_download('yamraj047/nepal-legal-mistral-7b-GGUF','nepal-legal-Q4_K_M.gguf'),n_ctx=2048); print(m(input('Q: '),max_tokens=300)['choices'][0]['text'])"
Example:

text
Q: What are the fraud penalties in Nepal?
⚠️ First run will download ~4GB. Subsequent runs are instant.

---

> ## 🧠 Why This Matters
>
> **Most legal chatbots:**
> - ❌ Are trained on generic web text  
> - ❌ Ignore legal hierarchy  
> - ❌ Cannot trace answers back to law
>
> **This system:**
> - ✅ Preserves Nepal’s legal structure  
> - ✅ Grounds responses in exact legal sections  
> - ✅ Reduces hallucination via chunk-level supervision  
> - ✅ Runs on consumer hardware

---

> ## 🗂️ Repository Structure
>
> ```text
> .
> ├── pdf-to-text/
> │   ├── pdf_to_text.py              # Faithful PDF → text extraction
> │   ├── penal-english.pdf           # Official legal source
> │   └── penal_code_raw.txt          # Clean extracted text
> │
> ├── chunking/
> │   ├── legal_chunking.py           # Hierarchy + chunk ID generation
> │   └── penal_code_chunks.json
> │
> ├── instruction-dataset/
> │   └── npc_instruction_dataset.json
> │
> ├── training/
> │   └── mistral_finetuning.ipynb    # Instruction fine-tuning
> │
> └── README.md
> ```

---

> ## 🧱 Stage 1 — PDF → Clean Text
>
> **Goal:** Extract the law exactly as published.
>
> - No chunking  
> - No summarization  
> - No interpretation  
>
> This ensures **legal authenticity**.

---

> ## 🧩 Stage 2 — Legal Chunking + Metadata
>
> Each subsection becomes a **single atomic legal unit**:
>
> ```json
> {
>   "law": "National Penal Code 2017",
>   "part": "Part-1",
>   "chapter": "Chapter-1",
>   "section": 1,
>   "subsection": "(1)",
>   "chunk_id": "npc2017_p1_c1_s1_sub1"
> }
> ```
>
> This enables:
> - Traceable answers  
> - Precise retrieval  
> - Explainable AI outputs  

---

> ## 🧠 Stage 3 — Instruction Dataset Engineering
>
> Instructions are **systematically generated**, not random:
> - Legal explanation  
> - Scope & applicability  
> - Classification questions  
> - Negative examples (“not mentioned in law”)
>
> Each instruction retains **full legal metadata**.

---

> ## 🔥 Stage 4 — Fine-Tuning
>
> - **Base Model:** Mistral-7B  
> - **Training Type:** Instruction tuning  
> - **Focus:** Legal understanding & reasoning  
>
> **Result:** A Nepal-specific legal LLM, not a generic chatbot.

---

> ## ⚡ Stage 5 — Quantization
>
> | Metric | Value |
> |------|------|
> | Original size | 13.5 GB |
> | Quantized size | **4.07 GB** |
> | Method | Q4_K_M |
> | Compatible with | llama.cpp, LM Studio |

---

> ## 🌐 Stage 6 — Deployment
>
> - Gradio UI for public interaction  
> - FastAPI backend for integration  
> - GGUF inference for offline use  

---

> ## ⚠️ Legal Disclaimer
>
> This project is for **research and educational purposes only**.
>
> ❗ **Not a substitute for professional legal advice.**

---

> ## 👤 Author
>
> **Yamraj Khadka**  
> Computer Engineering Undergraduate, Nepal 🇳🇵
>
> - 🤗 Hugging Face: https://huggingface.co/yamraj047  
> - 🐙 GitHub: https://github.com/yamrajkhadka  

---

> ## ⭐ Support the Project
>
> If this project helped you:
> - ⭐ Star the repository  
> - 🍴 Fork it  
> - 🧠 Build on it  
>
> This work aims to **raise the standard for Nepal-focused AI systems**.

---
