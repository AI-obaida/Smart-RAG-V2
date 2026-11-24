# Smart-RAG-V2 — Smart RAG PDF QA & Information Extraction Platform

## Overview

Smart-RAG-V2 is an academic Information Retrieval project built around the Smart RAG PDF QA platform. It provides a Flask-based web application that allows users to upload PDF documents, process and index their contents, and ask natural-language questions. The system uses Retrieval-Augmented Generation (RAG) to produce source-grounded answers with document and page references.

The application supports English and Arabic questions. Answers are generated using a locally hosted language model through Ollama.

This repository will serve as the foundation for the team's collaborative development, implementation, and evaluation throughout the Information Retrieval course (0135222) at Al-Zaytoonah University of Jordan.

## Problem Statement

Students, researchers, and professionals often need to find specific information within long PDF documents. Manually searching these documents can be time-consuming, especially when information is distributed across multiple pages.

General-purpose AI systems may also provide answers without verifiable sources, making it difficult for users to confirm their accuracy.

Smart RAG PDF QA addresses this problem by helping users retrieve information from their own documents and verify answers using document and page references.

## Proposed Solution

Smart RAG PDF QA is a web-based platform that allows users to upload PDF documents and ask natural-language questions in English or Arabic.

The system extracts text from PDFs, preserves page numbers, divides the text into chunks, and generates multilingual vector embeddings. These embeddings are stored in PostgreSQL using pgvector.

When a user submits a question, the application retrieves relevant document passages and sends the retrieved context to a locally hosted language model through Ollama.

The system also applies relevance and citation validation checks to reduce unsupported answers.

Retrieval-Augmented Generation (RAG) was selected because it combines semantic search with natural-language generation while allowing answers to reference the original documents.


## Unified Application Architecture

Smart-RAG-V2 is designed as a unified document retrieval and question-answering platform supporting both PDF and TXT knowledge sources through a single web interface.

The platform will maintain separate processing pipelines for each document type while providing a consistent user experience.

### PDF Retrieval Pipeline
- PDF upload and text extraction.
- Page-aware document chunking.
- Multilingual embedding generation.
- Semantic retrieval using PostgreSQL and pgvector.
- Source-grounded answer generation using RAG.

### TXT Information Retrieval Pipeline
- A structured knowledge base containing 30 TXT documents.
- Text preprocessing and indexing.
- Inverted Index implementation.
- TF-IDF-based document ranking.
- Top-5 relevant document retrieval.

### Unified User Experience

Users will interact with one application to search and retrieve information from supported PDF and TXT sources.

The application will provide relevant retrieved content and source references. The existing PDF-based RAG functionality will be preserved while the TXT-based Information Retrieval capabilities are integrated.

The architecture is intended to keep document processing and retrieval components modular, maintainable, and independently testable.

**Implementation status:** The PDF-based platform is the existing foundation. The TXT Information Retrieval pipeline and its integration are planned team development tasks.

## Project Structure

```text
Smart-RAG-V2/
|
|-- app/
|   |-- endpoints/
|   |-- frontend/
|   |-- services/
|   |   |-- pdf/
|   |   |-- txt/
|   |   |-- retrieval/
|   |   `-- ai/
|   |-- config.py
|   |-- models.py
|   `-- __init__.py
|
|-- knowledge_base/
|   `-- txt/
|       `-- (30 TXT knowledge-base documents - planned)
|
|-- tests/
|   |-- pdf/
|   |-- retrieval/
|   `-- evaluation/
|
|-- Documentation/
|-- Evaluation/
|-- Presentation/
|-- .env.example
|-- .gitignore
|-- requirements.txt
|-- schema.sql
|-- run.py
`-- README.md
```

The directory structure above represents the planned organization of the project. Some directories will be created as the corresponding development tasks are implemented. Existing project files and functionality will be preserved during this process.

The project separates API endpoints, application services, document processing, retrieval, AI logic, and database functionality to improve maintainability and independent testing.

## Clone the Repository

Clone the project from GitHub:

```powershell
git clone https://github.com/AI-obaida/Smart-RAG-V2.git
Set-Location Smart-RAG-V2
```

After cloning, follow the prerequisites and Windows setup instructions below.

## Course Information

| Item | Details |
|---|---|
| Course | Information Retrieval |
| Course Number | 0135222 |
| University | Al-Zaytoonah University of Jordan |
| Project | Smart-RAG-V2 |
| Academic Year | 2026–2027 |

## Team Members and Responsibilities

| Team Member | University ID | Role and Responsibilities |
|---|---|---|
| Obaida Allan | 202112799 | Team Leader, system integration, quality assurance, and final submission |
| Tareq Daraghmeh | 202211864 | Collecting, cleaning, and documenting the 30 TXT knowledge-base documents |
| Jameel Abu Salimeh | 202111224 | Implementing and testing the Inverted Index and TF-IDF ranking, including Top-5 retrieval |
| Yazan Al-Saayfeh | 202313914 | Preparing evaluation questions, measuring Precision@5, and comparing chatbot responses with and without retrieved context |

## Team Workflow and Contribution Guidelines

The team will follow a sequential development workflow to ensure that each component is completed, reviewed, and integrated before the next stage begins.

### Development Sequence

1. **Tareq – Knowledge Base Preparation**
   - Collect and clean 30 TXT documents.
   - Document the content and organize the files.
   - Submit the knowledge base through a Pull Request.

2. **Jameel – Information Retrieval Engine**
   - Implement text preprocessing and the Inverted Index.
   - Implement TF-IDF ranking.
   - Retrieve the Top-5 relevant documents.
   - Test the retrieval engine and submit a Pull Request.

3. **Yazan – Evaluation**
   - Prepare 10 evaluation questions.
   - Measure Precision@5.
   - Compare chatbot responses with and without retrieved context.
   - Document evaluation results.

4. **Obaida – Integration and Quality Assurance**
   - Review and integrate team contributions.
   - Verify compatibility with the existing PDF-based application.
   - Perform system-level testing.
   - Prepare the final project submission.

### GitHub Contribution Rules

- The `main` branch represents the official stable project version.
- Team members must create separate feature branches for their tasks, starting from the latest approved `main` branch.
- Each development stage should begin only after the previous stage has been reviewed and merged into `main`.
- Do not push directly to `main`.
- Submit changes through Pull Requests.
- Review and test changes before merging.
- Keep commits focused and use descriptive commit messages.
- Do not commit `.env` files, credentials, or local environment folders.

### Suggested Branch Names

- `feature/knowledge-base`
- `feature/inverted-index-tfidf`
- `feature/evaluation`
- `feature/system-integration`

The next development stage should begin after the previous stage has been reviewed and integrated.

## Main Features

- PDF upload and validation
- Text extraction with page-number preservation using PyMuPDF
- Document chunking and indexing
- PostgreSQL storage with pgvector
- Multilingual semantic search using sentence-transformers
- Retrieval-augmented question answering
- Local LLM inference using Ollama
- Arabic question translation for improved retrieval
- Structured answers with source and page citations
- Citation entailment and question relevance checks
- Saved document listing
- Web interface for uploading documents and asking questions
- Automated tests using pytest

## Technology Stack

| Component | Technology |
| --- | --- |
| Backend | Python 3.11, Flask |
| Database | PostgreSQL with pgvector extension |
| ORM | Flask-SQLAlchemy |
| PDF processing | PyMuPDF |
| Embeddings | sentence-transformers |
| Embedding model | intfloat/multilingual-e5-small |
| Vector search | pgvector cosine similarity |
| Local LLM | Ollama with qwen2.5:3b |
| Frontend | HTML, Bootstrap, JavaScript |
| Tests | pytest |

## Prerequisites

- Python 3.11
- PostgreSQL with the pgvector extension installed
- Ollama installed and running
- Ollama model: qwen2.5:3b
- Internet access for the initial embedding model download

The application has been developed and tested locally on Windows.

## Setup on Windows (PowerShell)

### 1. Create a virtual environment

```powershell
py -3.11 -m venv .venv
```

### 2. Install Python dependencies

```powershell
& ".\.venv\Scripts\python.exe" -m pip install -r requirements.txt
```

### 3. Configure environment variables

Copy the example configuration:

```powershell
Copy-Item ".env.example" ".env"
```

Edit `.env` and set the correct PostgreSQL username and password.

Configuration variables:

| Variable | Description |
| --- | --- |
| SECRET_KEY | Flask application secret key |
| DATABASE_URL | PostgreSQL connection URL |
| UPLOAD_FOLDER | Directory for uploaded PDF files |
| APP_ENV | Application environment: development or production |

Never commit or distribute a real `.env` file.

### 4. Prepare PostgreSQL

Create a PostgreSQL database named `smartrag` or update `DATABASE_URL` to use your chosen database.

Enable the pgvector extension in the application database:

```sql
CREATE EXTENSION IF NOT EXISTS vector;
```

Initialize the tables in a NEW, EMPTY application database using the included schema.sql file:

```powershell
psql -U postgres -d smartrag -X -v ON_ERROR_STOP=1 -f schema.sql
```

The script creates the documents and document_chunks tables and enables pgvector. Do not execute this initialization script against an existing populated database.

### 5. Prepare Ollama

Ensure Ollama is installed and running.

Download the language model:

```powershell
ollama pull qwen2.5:3b
```

Verify that the model is available:

```powershell
ollama list
```

The application expects Ollama to be available locally at:

```text
http://127.0.0.1:11434
```

### 6. Run the application

```powershell
& ".\.venv\Scripts\python.exe" -m flask --app "app:create_app" run --host 127.0.0.1 --port 5000 --no-reload
```

Open:

```text
http://127.0.0.1:5000/
```

## Usage

1. Open the application in a browser.
2. Upload a supported PDF document.
3. Wait for document processing and indexing to finish.
4. Select an indexed document.
5. Ask a question in English or Arabic.
6. Review the generated answer and its source citations.

Answers are intended to be grounded in retrieved PDF content. The system may return no supported answer when sufficient evidence is unavailable.

## API Endpoints

| Method | Endpoint | Description |
| --- | --- | --- |
| GET | `/` | Main web interface |
| POST | `/api/upload` | Upload and process a PDF |
| GET | `/api/documents` | List saved documents |
| POST | `/api/ask` | Ask a question about an indexed document |

Example JSON request for `/api/ask`:

```json
{
  "document_id": 1,
  "question": "What is the main topic of this document?",
  "top_k": 3
}
```

Replace `document_id` with an ID returned by the application.

## Automated Tests

Run the test suite from the project directory:

```powershell
& ".\.venv\Scripts\python.exe" -m pytest tests -q
```

The verified core test suite can be run with:

```powershell
& ".\.venv\Scripts\python.exe" -m pytest tests -q --tb=line --ignore=tests/test_modality_resolver_feature_safety.py --ignore=tests/test_modality_uncertainty_policy.py
```

Historical test results from a previous submission review reported 219 passing core tests. Seven tests in two experimental modality test modules were failing at that time and were excluded from the core test command.

These figures are historical and have not been re-verified against the current repository state. Run the test commands above to obtain the current results.

## Known Limitations

- Answer quality depends on PDF text extraction and retrieval quality.
- Relevant passages may not always appear among the top retrieved chunks.
- Language models can occasionally paraphrase numerical values inaccurately.
- Documents containing conflicting information may produce ambiguous answers.
- Citation and relevance checks reduce unsupported responses but do not guarantee correctness.
- Scanned PDFs without extractable text may require OCR support.
- The application is intended for local academic demonstration; production deployment requires additional security and operational review.

## Security and Submission Notes

- Keep `.env` private.
- Use `.env.example` only as a configuration template.
- Do not include uploaded user documents or local database credentials in public repositories.
- Exclude `.venv`, cache files, backups, and experimental artifacts from submission packages.
- The PostgreSQL database and Ollama model must be prepared separately on the target machine.


## Project Status

### Existing Implementation
The current project foundation includes:
- PDF upload and text extraction.
- Page-aware document chunking.
- Multilingual embedding generation.
- Semantic retrieval using PostgreSQL and pgvector.
- RAG-based question answering using Ollama.
- Source citations and validation mechanisms.
- Browser-based user interface.
- Automated tests.

### Planned Development
The following components are planned as part of the Information Retrieval course project:
- Preparing a knowledge base of 30 TXT documents.
- Implementing text preprocessing and an Inverted Index.
- Implementing TF-IDF document ranking.
- Retrieving the Top-5 relevant documents.
- Integrating TXT retrieval into the unified application.
- Evaluating retrieval performance using Precision@5.
- Comparing chatbot responses with and without retrieved context.

### Development Approach

The team will implement these components incrementally, test them independently, and integrate them into the existing Smart-RAG-V2 platform.

The final goal is a unified application supporting both PDF-based semantic retrieval and TXT-based Information Retrieval.
