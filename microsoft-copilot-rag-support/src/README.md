# Introduction

---

# **1️⃣ Does Microsoft Copilot Use Retrieval‑Augmented Generation (RAG)?**

### **Core Insight**

Copilot _does_ use RAG, but the retrieval sources and grounding layers vary across the different Copilot experiences.

### **Where RAG is used**

- **Copilot for Microsoft 365**  
  Full enterprise RAG: retrieves from emails, documents, Teams chats, SharePoint, OneDrive.  
  Uses semantic indexing + vector search.

- **Copilot Studio**  
  Custom knowledge-base RAG with embeddings, connectors, and structured grounding.

- **Copilot+ PCs**  
  Local semantic RAG using on-device models and Windows AI components.

- **Windows Copilot**  
  Restricted RAG focused on system state, settings, device capabilities, and local context.

- **Copilot Web**  
  Web-search RAG with citation grounding.

### **Why this matters**

Copilot is not a single model — it’s a _family_ of experiences.  
Each one blends retrieval and generation differently depending on privacy, context, and available data.

---

# **2️⃣ How Windows Copilot Uses Local AI Components**

### **High-Level Pipeline**

Windows Copilot processes queries through a multi-stage grounding pipeline:

#### **1. Copilot Orchestrator**

Interprets intent and decides whether the query needs:

- Local grounding
- Local inference
- Cloud reasoning
- Web search

#### **2. Windows Context Engine**

Retrieves system-level information:

- Settings
- Device capabilities
- Active windows
- Installed apps
- Local AI metadata

#### **3. Local AI Components**

Activated depending on the task:

- **Phi Silica (local LLM)**  
  Lightweight reasoning, summarization, privacy-preserving tasks.

- **Semantic Embeddings + Vector Search**  
  Maps natural language → Windows features.  
  Enables “change my wallpaper,” “open Bluetooth,” etc.

- **Image Extraction Engine**  
  OCR, object detection, screenshot understanding.

#### **4. Cloud LLM (when needed)**

Used for:

- Deep reasoning
- Long-form generation
- External knowledge
- Web-grounded answers

#### **5. Response Synthesis**

Combines:

- Local grounding
- Local inference
- Cloud reasoning
- Web search (if applicable)

### **Why this matters**

Windows Copilot is a _hybrid AI system_ — part local, part cloud — optimized for privacy, latency, and device intelligence.

---

# **3️⃣ When Copilot Uses the PC’s NPU**

### **NPU Usage (via Windows AI components)**

Copilot uses the NPU indirectly through Windows AI services when tasks match models optimized for NPU acceleration:

- Vision models
- OCR
- Object detection
- Layout extraction
- Semantic grounding
- Embeddings
- Certain Phi Silica operations

The NPU provides:

- Extremely low power consumption
- High throughput for supported operators
- Fast inference for small transformer blocks

### **What Copilot _does not_ use the NPU for**

- Large LLMs
- Cloud reasoning
- IDE coding assistants
- GPU-class workloads
- Models requiring unsupported operators (attention, KV cache, etc.)

### **Why this matters**

Copilot’s NPU usage is selective and tied to Windows AI components — not direct LLM execution.

---

# **4️⃣ Initial NPU vs GPU vs CPU Comparison (Based on Assumed Hardware)**

_(This section reflects the **initial** hardware assumption: Ryzen 7 8845HS + Radeon 780M + XDNA 3 NPU.)_

### **NPU — Best For**

- Small transformer models
- Embeddings
- Vision workloads
- Semantic grounding
- Lightweight reasoning
- Background AI tasks

**Strengths:** ultra-efficient, low power, fast for supported ops  
**Limitations:** cannot run large LLMs, limited operator coverage

---

### **GPU — Best For**

- Medium LLMs (3B–7B)
- ONNX transformer models
- Diffusion models
- Quantized inference

**Strengths:** good FP16/INT8 throughput, broader operator support  
**Limitations:** VRAM limits model size, higher power draw

---

### **CPU — Best For**

- Large LLMs (13B+)
- High-precision inference
- Fallback operators
- Multi-threaded workloads

**Strengths:** most flexible, supports all operators  
**Limitations:** slower for attention-heavy models, highest power usage

---
