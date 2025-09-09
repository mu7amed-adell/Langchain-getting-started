# LangChain Quickstart

This project demonstrates various LangChain capabilities including:
- Basic chat with LLMs using Ollama
- Prompt templates
- Retrieval-Augmented Generation (RAG) with Ollama embeddings

## Prerequisites

1. Install [Ollama](https://ollama.com/) and download a model (e.g. `llama3.2`):
   ```bash
   ollama pull llama3.2
   ```
2. Python 3.10 or higher

## Installation

1. Clone this repository
2. Create and activate a virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Running the Notebooks

### 1. Basic Chat Model (`1_chat_model_basics.ipynb`)
Demonstrates basic interaction with Ollama LLMs:
1. Start Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
2. Open and run `1_chat_model_basics.ipynb`

### 2. RAG with Ollama (`2_chat_model_with_RAG.ipynb`)
Implements a full RAG pipeline:
1. Processes documents from `data/` directory
2. Creates vector store using Ollama embeddings (`nomic-embed-text`) [Embeddings](https://ollama.com/search?c=embedding)
3. Performs similarity search and generates responses

## Key Features

- **Local LLMs**: Uses Ollama for running models locally
- **Embeddings**: Uses Ollama's `nomic-embed-text` for document embeddings
- **Vector Store**: Uses ChromaDB for storing and retrieving embeddings

## How RAG Works - Higher level abstraction

Retrieval-Augmented Generation (RAG) combines large language models with external knowledge retrieval through these key steps:

1. **Loading Documents**
   - Source documents are loaded from files or databases
   - Various formats supported (PDF, text, etc.)
   - Documents are parsed into raw text content

2. **Creating Document Chunks**
   - Documents are split into smaller, meaningful chunks
   - Chunk size optimized for model context windows
   - Strategic overlap preserves context between chunks

3. **Initializing the Embedding Model**
   - Select an appropriate embedding model
   - Configure model parameters (dimensions, etc.)
   - Load model weights into memory

4. **Embedding Document Data**
   - Convert each text chunk to numerical embeddings
   - Embeddings capture semantic meaning of text
   - Store embeddings in a vector database

5. **Retrieving Relevant Chunks**
   - Embed user queries with same model
   - Perform similarity search against vector store
   - Retrieve top-k most relevant document chunks
   - Pass retrieved context to LLM for generation

Key Advantages:
- Overcomes LLM knowledge limitations
- Provides verifiable sources
- Enables domain-specific applications

## Data Preparation

Place your documents in the `data/` directory. Supported formats:
- PDF (`.pdf`)
- Text (`.txt`)

The RAG notebook will automatically process these files.

## Troubleshooting

- If you get connection errors, ensure Ollama is running:
  ```bash
  ollama serve
  ```
- For embedding issues, verify the model is downloaded:
  ```bash
  ollama pull nomic-embed-text
  ```

## Customization

You can modify these environment variables:
```bash
export OLLAMA_MODEL=llama3  # Change default model
export EMBEDDING_MODEL=nomic-embed-text  # Change embedding model
```

## Future Topics

We will create another LangChain deep dive covering advanced techniques for:

### Text Splitting Methods:
- **Character-based Splitting**: Simple splitting by fixed character count
- **Token-based Splitting**: Splitting by token count (respects token boundaries)
- **Semantic Splitting**: Splitting at natural semantic boundaries
- **Overlap Strategies**: Context-preserving overlap between chunks

### Retrieval Techniques:
- **Basic Similarity Search**: Standard vector similarity retrieval
- **Maximum Marginal Relevance (MMR)**: Balances relevance and diversity
- **LLM-aided Retrieval**: Uses LLMs to refine retrieval queries
- **Compression Techniques**: Summarizes retrieved content to fit context

### Context Window Solutions:
- **Map-Reduce**: Processes long documents in parallel chunks
- **Refining**: Iteratively improves answers through multiple passes
- **Map-Rerank**: Scores and reranks multiple candidate answers

These techniques will help optimize RAG performance for different document types and use cases.
