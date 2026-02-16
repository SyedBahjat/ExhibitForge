<div align="center">

# ExhibitForge - AI-Powered Legal Document Exhibit Bundler

### Automate exhibit bundling with AI that reads, extracts, and organizes your legal PDFs in seconds.

[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.45+-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io)
[![Google Gemini](https://img.shields.io/badge/Google%20Gemini-AI-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://ai.google.dev)
[![LangChain](https://img.shields.io/badge/LangChain-Agent-1C3C3C?style=for-the-badge&logo=chainlink&logoColor=white)](https://langchain.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

<br />

[Features](#features) &bull; [Demo](#demo) &bull; [Quick Start](#quick-start) &bull; [How It Works](#how-it-works) &bull; [Tech Stack](#tech-stack) &bull; [Contributing](#contributing) &bull; [Contact](#connect-with-me)

<br />

<img src="https://img.shields.io/github/stars/SyedBahjat/document-analyzer?style=social" alt="GitHub Stars" />
<img src="https://img.shields.io/github/forks/SyedBahjat/document-analyzer?style=social" alt="GitHub Forks" />
<img src="https://img.shields.io/github/watchers/SyedBahjat/document-analyzer?style=social" alt="GitHub Watchers" />

</div>

---

## The Problem

Legal professionals spend **hours manually organizing exhibit bundles** — uploading documents, extracting client names, numbering pages, creating cover sheets, and merging everything into one PDF. It's repetitive, error-prone, and painfully slow.

## The Solution

**ExhibitForge** uses an AI agent powered by **Google Gemini** and **LangChain** to automate the entire process. Upload your PDFs, arrange the order, click one button — and get a professionally formatted exhibit bundle with an auto-generated cover page, client names, form numbers, and correct page indexing.

> What used to take 30+ minutes now takes under 30 seconds.

---

## Features

- **AI-Powered Metadata Extraction** — Gemini reads each document's first page and intelligently extracts client names and form numbers using agentic reasoning
- **Drag-and-Drop Document Upload** — Upload multiple PDFs at once through a clean Streamlit interface
- **Custom Document Ordering** — Arrange exhibits in your preferred order before bundling
- **Auto-Generated Cover Page** — Professional exhibit list cover page with client names, form numbers, and starting page references
- **Smart Page Indexing** — Automatically tracks and labels page numbers across all merged documents
- **One-Click PDF Export** — Download the final exhibit bundle as a single, organized PDF
- **Agentic Reasoning** — Uses LangChain's ReAct agent pattern for intelligent document analysis, not simple prompt chaining
- **Graceful Error Handling** — Falls back to safe defaults if AI extraction encounters issues

---

## Demo

```
Upload PDFs ──> Arrange Order ──> Click Generate ──> Download Bundle
     |               |                   |                  |
  Multiple      Drag & Drop      AI extracts          Single PDF
   files        reordering      client names &       with cover +
  at once                       form numbers         page index
```

**Example Output — Cover Page:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
          Client Exhibit List
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Exhibit 1: Client: John Doe — Form: I-130 — Starts on Page 2
Exhibit 2: Client: Jane Smith — Form: I-485 — Starts on Page 15
Exhibit 3: Client: Ahmed Hassan — Form: I-765 — Starts on Page 28
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Quick Start

### Prerequisites

- Python 3.9 or higher
- A [Google AI API Key](https://aistudio.google.com/apikey) (free tier available)

### Installation

**1. Clone the repository**

```bash
git clone https://github.com/SyedBahjat/document-analyzer.git
cd document-analyzer
```

**2. Create a virtual environment**

```bash
python -m venv venv
source venv/bin/activate        # macOS / Linux
venv\Scripts\activate           # Windows
```

**3. Install dependencies**

```bash
pip install -r requirements.txt
```

**4. Set up environment variables**

Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_google_api_key_here
GENAI_MODEL=gemini-1.5-flash
```

**5. Run the application**

```bash
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`

---

## How It Works

```
                    ┌──────────────────────┐
                    │   Upload PDF Files   │
                    └──────────┬───────────┘
                               │
                    ┌──────────▼───────────┐
                    │  Arrange Doc Order   │
                    └──────────┬───────────┘
                               │
                    ┌──────────▼───────────┐
                    │  For Each Document:  │
                    │                      │
                    │  1. Extract text     │
                    │     (pdfplumber)     │
                    │                      │
                    │  2. AI Agent reads   │
                    │     first page &     │
                    │     extracts:        │
                    │     • Client name    │
                    │     • Form number    │
                    │                      │
                    │  3. Track page count │
                    └──────────┬───────────┘
                               │
                    ┌──────────▼───────────┐
                    │  Generate Cover Page │
                    │  (ReportLab)         │
                    └──────────┬───────────┘
                               │
                    ┌──────────▼───────────┐
                    │  Merge All PDFs      │
                    │  Cover + Documents   │
                    │  (PyPDF2)            │
                    └──────────┬───────────┘
                               │
                    ┌──────────▼───────────┐
                    │  Download Bundle     │
                    └──────────────────────┘
```

### Architecture

The application uses an **agentic AI architecture** built with LangChain:

- **Orchestrator Agent** — A `ZERO_SHOT_REACT_DESCRIPTION` agent that reasons about document content and decides how to extract metadata
- **TitleExtractor Tool** — A registered LangChain tool that the agent uses to parse document information
- **Gemini LLM** — Google's Gemini model serves as the reasoning backbone
- **Two-Phase PDF Generation** — First pass creates a temporary cover, second pass generates the final cover with accurate exhibit data

---

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Frontend** | Streamlit | Interactive web UI for upload & download |
| **AI Engine** | Google Gemini | Document understanding & metadata extraction |
| **Agent Framework** | LangChain | Agentic reasoning with tool-based orchestration |
| **PDF Extraction** | pdfplumber | Text extraction from uploaded PDFs |
| **PDF Generation** | ReportLab | Professional cover page creation |
| **PDF Merging** | PyPDF2 | Combining all documents into one bundle |
| **Environment** | python-dotenv | Secure API key management |

---

## Project Structure

```
document-analyzer/
├── app.py                 # Main application — UI + AI agent + PDF pipeline
├── requirements.txt       # Python dependencies
├── .env                   # API keys (create this yourself)
├── .gitignore            # Ignores venv/ and sensitive files
├── LICENSE               # MIT License
└── README.md             # You are here
```

---

## Use Cases

- **Immigration Law Firms** — Bundle client petition documents with exhibit cover pages
- **Corporate Legal Teams** — Organize case exhibits for court filings
- **Paralegals & Legal Assistants** — Automate repetitive document bundling tasks
- **Solo Practitioners** — Save hours on document preparation
- **Any Professional** — Who needs to merge and index multiple PDFs with metadata extraction

---

## Roadmap

- [ ] Batch processing for large document sets
- [ ] Custom exhibit label templates
- [ ] OCR support for scanned documents
- [ ] Multi-language document support
- [ ] Cloud deployment (Streamlit Cloud / AWS)
- [ ] Document summarization per exhibit
- [ ] Export to Word/Excel exhibit lists

---

## Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

---

## Connect With Me

Built by **Muhammad Bahjat** — AI & Automation Developer

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/muhammadbahjat/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/SyedBahjat)

If this project helped you, consider giving it a star! It helps others discover it too.

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**If you find ExhibitForge useful, please give it a :star: on GitHub!**

*Built with AI. Designed for legal professionals.*

</div>
