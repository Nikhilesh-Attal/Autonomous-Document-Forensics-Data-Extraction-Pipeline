<img width="1152" height="252" alt="image" src="https://github.com/user-attachments/assets/62c47edc-09d4-45fc-8a0c-6c87d8f865d0" />

Autonomous Document Forensics & Data Extraction Pipeline

Designed as an enterprise-grade automation solution, this Autonomous Document Forensics pipeline solves the critical challenge of LLM unpredictability in production data workflows. Built entirely on n8n, the system automatically ingests unstructured documents from cloud storage and processes them using high-speed AI models (Groq/Gemini) engineered with strict, forensic-level prompts.

Rather than relying on fragile "happy path" logic, this architecture features a robust, custom-built validation layer. A JavaScript interceptor evaluates the AI's JSON output against a strict schema. If the AI hallucinates, omits required fields, or breaks formatting, the system triggers an autonomous self-correction loop. The broken payload and exact error logs are fed back into the AI agent, forcing it to self-repair the output. To ensure absolute stability, a built-in circuit-breaker mechanism limits retry attempts, gracefully routing persistent failures to an error log while the main batch processing continues uninterrupted.

By guaranteeing that only perfectly structured, strictly validated data reaches the destination database, this project demonstrates a highly resilient approach to AI orchestration. It bridges the gap between basic API integrations and reliable, fault-tolerant product building.

## 🛠 Core Technologies
* **Workflow Orchestration:** n8n
* **AI / LLM:** Groq (Llama 3) / Google Gemini
* **Validation Layer:** Custom JavaScript (JSON Schema parsing)
* **Data Ingestion:** Google Drive API
* **Database Destination:** Airtable (MVP) / Supabase

## ⚙️ Architecture & Key Features

### 1. Dynamic Batch Processing
Utilizes n8n's looping infrastructure to handle bulk document ingestion, ensuring each file is processed, validated, and logged individually without bottlenecking the entire workflow.

### 2. Autonomous Self-Correction Loop
If the LLM fails to output valid JSON, the system intercepts the error, bundles the original broken output with the specific JavaScript syntax error, and dynamically prompts the AI to fix its own mistake.

### 3. Circuit Breaker Mechanism
Prevents infinite LLM hallucination loops by enforcing a strict maximum retry limit (e.g., 3 attempts). If a document fails repeatedly, it is safely quarantined in an error log while the pipeline automatically moves on to the next item.

### 4. Advanced Prompt Engineering
Employs strictly constrained system instructions designed specifically for data extraction APIs, preventing conversational filler and enforcing exact schema adherence.
