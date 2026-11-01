# Simple RAG Document Retrieval

This project is a small, notebook-based demonstration of retrieval-augmented generation (RAG) building blocks. It shows how to load documents, split text into chunks, create embeddings, store them in vector indexes, and retrieve relevant chunks for a natural-language query.

The example uses a PDF about the Transformer paper and searches for its authors. It demonstrates semantic document retrieval; it does not generate a conversational answer with a language model.

## What the notebook does

[`simplerag.ipynb`](./simplerag.ipynb) walks through these steps:

1. Loads a local text file, a web page, and a local PDF.
2. Splits the PDF into chunks of up to 1,000 characters, with 200 characters of overlap.
3. Uses OpenAI embeddings to represent the first 20 PDF chunks as vectors.
4. Stores and searches those vectors with both Chroma and FAISS.
5. Displays the retrieved text for a sample query.

The text and web sources are loaded for demonstration, but the current chunking and indexing cells use only the PDF. The vector stores are built in memory when the notebook runs.

## Project files

- `simplerag.ipynb` — the end-to-end retrieval walkthrough.
- `attention.pdf` — the PDF used by the notebook.
- `speech.txt` — a text-loader example.
- `requirements.txt` — Python package dependencies.
- `.env` — local environment variables, including the OpenAI API key; keep this file private.

## Run locally

### 1. Prerequisites

- Python installed.
- An OpenAI API key. The embedding cells send requests to OpenAI and may incur API charges.
- Internet access to download Python packages and load the example web page.

Run the following commands from the project directory.

### 2. Create and activate a virtual environment

**Windows PowerShell**

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell prevents activation, you can invoke the environment's Python directly as shown in the install and launch commands below.

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

With the virtual environment activated:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If you did not activate the environment in Windows PowerShell, use:

```powershell
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

### 4. Configure the OpenAI API key

Create or update `.env` in the project directory:

```dotenv
OPENAI_API_KEY=your_openai_api_key
```

Replace the example value with your key. Do not commit or share the real key.

### 5. Launch the notebook

With the environment activated:

```bash
jupyter notebook simplerag.ipynb
```

On Windows without activation:

```powershell
.\.venv\Scripts\jupyter.exe notebook simplerag.ipynb
```

In Jupyter, select the virtual environment's Python kernel, then run the notebook cells from top to bottom. Run it with the project directory as the working directory so it can find `speech.txt` and `attention.pdf`. The web-loader cell also fetches its configured page, and the embedding and vector-store cells require the API key.

## Customize

- Change the `query` values in the notebook to search for other information.
- To retrieve from the text or web source as well, pass those loaded documents (or a combined document list) into the splitter and vector-store construction cells instead of only `pdf_documents`.
- The current example displays retrieved document text. Generating a natural-language answer from retrieved context would require adding a language-model response step.
