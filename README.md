# AI-Native Reader

**Swipe through books like Shorts — an AI-native reader that turns every page into a conversation.**

AI-Native Reader is a lightweight, extensible ebook and document reader enhanced with local LLM intelligence. It transforms traditional reading into an interactive, insight-driven experience — powered entirely by models running on your own machine.

This project is based on the original *reader3* by Andrej Karpathy, and extends it with AI-assisted reading, local model integration, PDF/OCR support, and an interactive analysis workflow.

---

## 🚀 Features (MVP)

### **🔍 AI-Assisted Reading**

* Select any text or analyze the entire chapter with a single click.
* Plug-and-play prompt files for summaries, explanations, translations, and more.
* Local LLM support (Llama, Qwen, DeepSeek, OpenAI-compatible models).

### **📖 Multi-Format Support**

* Full EPUB3 reading and navigation.
* **PDF support via OCR** (DeepSeek OCR pipeline included in MVP).
* Each document is normalized into a structured, book-like format for consistent reading.

### **🧠 Local LLM Backend**

* Modular backend design (`LLMClient`) supporting:

  * Ollama
  * OpenAI-compatible HTTP endpoints
  * Custom model servers
* Easily switch models via environment variables or configuration.

### **⚡ Instant Analysis UI**

* Clean, minimal UI on top of the original reader.
* "Ask LLM" panel with prompt selector.
* Automatically falls back to chapter-wide analysis when no text is selected.

---

## 🛠️ Architecture Overview

The system consists of three core components:

### **1. Document Processor**

* EPUB: extracted into a `_data/` folder with HTML chapters and metadata.
* PDF: processed through DeepSeek OCR → normalized into chapter-like HTML pages.

### **2. Web Server**

* Lightweight FastAPI-based backend.
* Serves chapters, static assets, and LLM inference API.
* Renders templates for reading and interaction.

### **3. LLM Engine**

* Unified client with swappable backends.
* Prompt templating system in `prompts/`.
* Customizable workflows (summary, QA, reasoning).

---

## 🧩 Prompt System

Prompts are simple text or Markdown files placed in `prompts/`, e.g.:

```text
#name: Short Summary
Please summarize the following text in a concise way:
{text}
```

These appear automatically in the prompt dropdown inside the reader.

---

## 📦 Installation (MVP)

### **1. Clone the Repository**

```bash
git clone https://github.com/yourname/ai-native-reader.git
cd ai-native-reader
```

### **2. Install Dependencies**

Using **uv**:

```bash
uv sync
```

### **3. Start the Server**

```bash
uv run server.py
```

Then open:

```
http://127.0.0.1:8123
```

### **4. Process a Book**

EPUB:

```bash
uv run reader3.py mybook.epub
```

PDF:

```bash
uv run pdf_reader3.py mybook.pdf
```

---

## 🔧 Configuration

Set your preferred local model and backend:

```bash
export LLM_BACKEND=ollama
export LLM_MODEL=llama3
export LLM_BASE_URL=http://localhost:11434
```

For DeepSeek or OpenAI-compatible servers:

```bash
export LLM_BACKEND=openai_compatible
export LLM_MODEL=deepseek-chat
export LLM_BASE_URL=http://localhost:8000
```

---

## 📚 Roadmap

* Better PDF segmentation & TOC reconstruction
* Inline floating action button when selecting text
* Vector-based semantic search
* Book-level memory & long-context understanding
* Optional cloud-model mode
* Multi-user web version

---

## 📝 License

MIT License — includes original portions from *reader3* by Andrej Karpathy.

---

## 🙌 Acknowledgements

* **Andrej Karpathy** for the original [reader3](https://github.com/karpathy/reader3) project that inspired this work.
* DeepSeek for OCR models.
* The open-source LLM ecosystem for model and tooling support.

