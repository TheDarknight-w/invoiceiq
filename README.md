# InvoiceIQ — AI Invoice Extractor & Validator

A compact intelligent-document-processing prototype. Upload a PDF or image, extract text, request structured invoice fields from an optional OpenAI-compatible LLM endpoint, run deterministic arithmetic/required-field checks, and download JSON.

## Features
- PDF text extraction with PyMuPDF.
- OCR fallback for scanned PDFs/images using Tesseract.
- LLM-based structured extraction when `LLM_API_KEY` is configured.
- Transparent rule-based fallback for local demos without an LLM key.
- Deterministic missing-field and subtotal-plus-tax validation.
- Browser dashboard and JSON export.

## Local setup
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
# Add your own API key to .env if available
python app.py
```
Open http://127.0.0.1:5002. For OCR of scanned documents, install the Tesseract system binary (`tesseract-ocr`) as well as Python requirements.

## Docker
```bash
cp .env.example .env
# Set LLM_API_KEY in .env or export it in your shell
docker compose up --build
```

## Tests
```bash
python -m unittest discover -s tests -v
```

## Configuration
- `LLM_API_KEY`: optional API key.
- `LLM_BASE_URL`: OpenAI-compatible Chat Completions URL.
- `LLM_MODEL`: model name supported by your chosen provider.

Without an API key, the application uses a simple regex-based fallback. That fallback is intended only for the labelled sample invoice format and is not a substitute for an LLM or robust invoice parser. Validate all extracted values manually before financial use.

## Tech stack
Python, Flask, PyMuPDF, Tesseract OCR, Pillow, requests, LLM API, HTML, CSS, JavaScript, Docker.
