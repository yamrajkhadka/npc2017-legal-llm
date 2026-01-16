# 🇳🇵 Nepal Legal Mistral 7B

> **An end‑to‑end, domain‑specific Large Language Model for Nepalese law**, trained on the *National Penal Code of Nepal (2017)* — from raw legal PDF to deployable, quantized AI systems.

---

## 🏗️ System Architecture

![System Architecture](https://github.com/yamrajkhadka/npc2017-legal-llm/blob/main/system-archi.png)

This diagram illustrates the complete lifecycle of the **Nepal Legal LLM**, from raw legal documents to real-world deployment.
___

## 🔎 What This Project Really Is

This is **not just a fine‑tuned model**.

It is a **complete legal‑LLM engineering pipeline**, built to demonstrate how a country‑specific, legally grounded AI system can be created **from scratch**:

* 📄 Raw government legal PDF
* 🧹 Clean text extraction (no hallucinated summaries)
* 🧩 Hierarchical legal chunking (Part → Chapter → Section → Subsection)
* 🏷️ Deterministic chunk IDs for traceability
* 🧠 Instruction‑tuning dataset generation
* 🔥 Fine‑tuning Mistral‑7B for legal reasoning
* ⚡ Quantization for low‑resource inference
* 🌐 Real deployments (UI + API)

This project is designed to be **auditable, reproducible, and legally faithful**.

---

## 🚀 Live Systems

### 🖥️ Interactive Web Apps

| Deployment                   | Description                 | Link                                                                                                                                     |
| ---------------------------- | --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Full‑Precision Assistant** | Accurate legal reasoning    | [https://huggingface.co/spaces/yamraj047/penal-legal-assistant](https://huggingface.co/spaces/yamraj047/penal-legal-assistant)           |
| **Fast API Version**         | Optimized backend inference | [https://huggingface.co/spaces/yamraj047/nepal-legal-assistant-fast](https://huggingface.co/spaces/yamraj047/nepal-legal-assistant-fast) |
| **GGUF Quantized Assistant** | Runs on low‑RAM machines    | [https://huggingface.co/spaces/yamraj047/Nepall-legal-assist](https://huggingface.co/spaces/yamraj047/Nepall-legal-assist)               |

---

## 🤗 Models

| Model                  | Format        | Size        | Link                                                                                                                         |
| ---------------------- | ------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Nepal Legal Mistral‑7B | FP16          | ~13.5 GB    | [https://huggingface.co/yamraj047/nepal-legal-mistral-7b](https://huggingface.co/yamraj047/nepal-legal-mistral-7b)           |
| Nepal Legal Mistral‑7B | GGUF (Q4_K_M) | **4.07 GB** | [https://huggingface.co/yamraj047/nepal-legal-mistral-7b-GGUF](https://huggingface.co/yamraj047/nepal-legal-mistral-7b-GGUF) |

---

## 🧠 Why This Matters

Most legal chatbots:

* Are trained on **generic web text**
* Lose **legal hierarchy**
* Cannot cite or trace answers

This system:

✅ Preserves **Nepal’s legal structure**
✅ Grounds answers in **exact law sections**
✅ Reduces hallucination through **chunk‑level supervision**
✅ Can be deployed on **consumer hardware**

---

## 🗂️ Repository Structure

```text
.
├── pdf->text_nochunk/
│   ├── pdf->txt_nochunk.py        # Faithful PDF → text extraction
│   ├── penal-english.pdf          # Official legal source
│   ├── penal_code_input.txt       # Clean raw text
│
├── chunk_id-add/
│   ├── chunk_id-add.py            # Legal hierarchy + chunk IDs
│   └── pdf->txt-with_chunk_id.json
│
├── instruction-dataset/
│   └── npc_instruction_dataset.json
│
├── training/
│   └── fast-fine-tuning.ipynb     # Mistral‑7B fine‑tuning
│
└── README.md
```

---

## 🧱 Stage 1 — PDF → Clean Text

**Objective:** Extract the law *as‑is*.

* No chunking
* No summarization
* No interpretation

This ensures the dataset remains **legally authentic**.

---

## 🧩 Stage 2 — Legal Chunking + Metadata

Each subsection becomes a **single atomic legal unit**:

```json
{
  "law": "National Penal Code 2017",
  "part": "Part‑1",
  "chapter": "Chapter‑1",
  "section": 1,
  "subsection": "(1)",
  "chunk_id": "npc2017_p1_c1_s1_sub1"
}
```

This enables:

* Traceable answers
* Precise retrieval
* Explainable AI outputs

---

## 🧠 Stage 3 — Instruction Dataset Engineering

Instead of random prompts, instructions are **systematically generated**:

* Legal explanation
* Scope & applicability
* Classification questions
* Negative examples ("not mentioned")

Each sample retains **full metadata** linking back to the law.

---

## 🔥 Stage 4 — Fine‑Tuning

* Base Model: **Mistral‑7B**
* Training Type: Instruction tuning
* Focus: Legal comprehension & reasoning

Result: a **Nepal‑specific legal LLM**, not a generic chatbot.

---

## ⚡ Stage 5 — Quantization

| Metric          | Value                |
| --------------- | -------------------- |
| Original size   | 13.5 GB              |
| Quantized size  | **4.07 GB**          |
| Method          | Q4_K_M               |
| Compatible with | llama.cpp, LM Studio |

This allows deployment on **laptops & low‑RAM servers**.

---

## 🌐 Stage 6 — Deployment

* Gradio UI for public interaction
* FastAPI backend for integration
* GGUF inference for offline use

---

## ⚠️ Legal Disclaimer

This project is for **research and educational purposes only**.

❗ **Not a substitute for professional legal advice.**

---

## 👤 Author

**Yamraj Khadka**
Computer Engineering Undergraduate
AI / Machine Learning / Legal NLP
Nepal 🇳🇵

* Hugging Face: [https://huggingface.co/yamraj047](https://huggingface.co/yamraj047)
* GitHub: *(add link)*

---

## ⭐ If This Project Helped You

Give it a **star**, fork it, or build on it.

This project is meant to **raise the bar for Nepal‑focused AI systems**.
