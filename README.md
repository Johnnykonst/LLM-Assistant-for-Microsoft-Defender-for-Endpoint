# LLM-Assisted MITRE-Aware KQL Generation for Microsoft Defender for Endpoint

This repository accompanies a diploma thesis titled **“LLM Assistant for Model-Driven Engineering”** and contains a Python-based prototype that combines structured threat intelligence with a Large Language Model (LLM) to automatically generate **Kusto Query Language (KQL)** detection rules for **Microsoft Defender for Endpoint (MDE)**.

The assistant enriches LLM prompts with **MITRE ATT&CK** technique metadata retrieved from **OpenCTI**, post-processes generated queries to ensure schema correctness, and supports iterative human-in-the-loop refinement.

---

## 📌 Project Motivation

Writing high-quality detection queries is time-consuming and requires:

* Deep knowledge of the MITRE ATT&CK framework
* Familiarity with MDE’s proprietary telemetry schema
* Careful tuning to reduce false positives

This project explores how **LLMs can be safely constrained and augmented with structured threat intelligence** to assist SOC analysts in generating detection logic more efficiently, while keeping humans in control.

---

## 🧠 Key Features

* **MITRE ATT&CK–aware detection generation**
  Automatically retrieves technique metadata (ID, name, tactic, platforms, description) from OpenCTI.

* **Constrained LLM prompting**
  Injects structured ATT&CK context and environment hints into prompts to reduce hallucinations and improve relevance.

* **MDE schema normalization**
  Post-processes LLM output to fix common field naming errors and ensure required fields (`DeviceId`, `ReportId`) are present.

* **Human-in-the-loop refinement**
  Analysts can iteratively refine generated KQL using environment-specific exclusions (accounts, devices, processes).

* **Deterministic output**
  LLM temperature is set to zero to improve reproducibility.

---

## 🏗 Architecture Overview

1. User provides a MITRE ATT&CK technique name or ID
2. Technique metadata is fetched from OpenCTI via GraphQL
3. A constrained prompt is constructed using ATT&CK context
4. The LLM generates an initial KQL detection query
5. The query is normalized for MDE schema compatibility
6. Optional interactive refinement loop with the analyst

---

## ⚙️ Requirements

* Python 3.10+
* An OpenAI-compatible API key
* An OpenCTI instance with ATT&CK data loaded
* Access to Microsoft Defender for Endpoint telemetry schema

### Python Dependencies

```bash
pip install requests python-dotenv langchain-openai
```

---

## 🔐 Environment Configuration

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_openai_api_key
OPENCTI_API_KEY=your_opencti_api_key
OPENCTI_URL=https://your-opencti-instance
```

---

## ▶️ Usage

Run the assistant from the command line:

```bash
python assistant_mitre.py
```

You will be prompted to enter a MITRE ATT&CK technique name or ID (e.g. `T1003`, `Credential Dumping`).

The assistant will:

1. Generate an initial KQL query
2. Display it for review
3. Allow optional refinement (e.g., excluding accounts)
4. Output the final KQL ready for use in MDE custom detections

---

## 📎 Scope and Limitations

* This is a **research prototype**, not a production-ready tool
* Generated detections must be **reviewed and validated by analysts**
* Schema mappings reflect common MDE fields but may require adjustment
* Detection quality depends on available telemetry and environment context

---

## 📄 Academic Context

This implementation supports the diploma thesis:

> **LLM Assistant for Model-Driven Engineering**
> Exploring the use of LLMs as constrained assistants in security detection engineering through structured threat intelligence integration.

The goal is not full automation, but **augmentation of expert workflows**.

---

## 📜 License

This project is provided for **research and educational purposes**.
No warranty is expressed or implied.
