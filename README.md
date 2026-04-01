# Assignment 3: LLM-Powered Applications & Distributed Computing
 
This assignment combines distributed data processing using Spark with a Retrieval-Augmented Generation (RAG) pipeline, culminating in an integrated analytics application that routes and responds to natural language queries.
 
---
 
## Assignment Overview
 
The notebook is structured into three parts:
 
**Part 1 – Distributed Data Processing with Spark**
Processes the NYC Yellow Taxi dataset (January 2024) using PySpark. Tasks include environment setup and data loading, data cleaning and feature engineering, Spark SQL analytics (busiest hours, trip speeds, revenue by location, cumulative trip counts, and distance-based fare comparisons), and performance optimization via caching and partition pruning.
 
**Part 2 – RAG Pipeline over Transportation Documents**
Builds a Retrieval-Augmented Generation pipeline over a corpus of transportation policy PDFs. Covers document ingestion and quality inspection, chunking and embedding using HuggingFace's `all-MiniLM-L6-v2` model, vector storage with ChromaDB, and a full RAG question-answering pipeline backed by an OpenAI-compatible LLM.
 
**Part 3 – Integrated Analytics Application**
Combines Parts 1 and 2 into a unified system with an LLM-powered query router that classifies user questions as `DATA`, `DOCUMENT`, or `HYBRID`, a data query handler that generates and executes Spark SQL from natural language, and a natural language answer synthesizer for query results.
 
---
 
## Project Structure
 
```
assignment3/
├── assignment3.ipynb       # Main notebook
├── data/
│   ├── raw/                # Downloaded Parquet data (auto-created)
│   └── output/             # Partitioned Parquet output (auto-created)
├── docs/                   # PDF documents for the RAG pipeline
├── chroma_db/              # ChromaDB vector store (auto-created)
└── .env                    # Environment variables (see setup below)
```
 
---
 
## Requirements
 
- Python 3.9+
- Java 8 or 11 (required for PySpark)
- pip packages:
 
```
pyspark
pandas
requests
openai
python-dotenv
langchain
langchain-community
langchain-text-splitters
chromadb
sentence-transformers
matplotlib
```
 
Install all dependencies with:
 
```bash
pip install -r requirements.txt
```
 
---
 
## Environment Setup
 
Create a `.env` file in the project root with the following variables:
 
```env
LLM_BASE_URL=<your_llm_api_base_url>
LLM_API_KEY=<your_llm_api_key>
```
 
These are used to connect to the OpenAI-compatible LLM endpoints in Parts 2 and 3. Part 3's data query handler also makes calls to `llama3.3-70b-instruct` — ensure your API key has access to that model.
 
---
 
## How to Run
 
### Option 1 – Jupyter Notebook (Recommended)
 
```bash
jupyter notebook assignment3.ipynb
```
 
Run cells sequentially from top to bottom. The notebook will:
- Automatically download the NYC taxi Parquet file into `data/raw/`
- Create a Spark session
- Build and persist the ChromaDB vector store
- Run all analytics and LLM-powered queries
 
> **Note:** Ensure your `docs/` folder contains the transportation policy PDFs before running Part 2.

---
 
## Notes
 
- The first run may take several minutes as it downloads the ~500 MB Parquet file and builds the vector store.
- PySpark requires Java to be installed and available on your `PATH`. Verify with `java -version`.
- The ChromaDB store is persisted to `./chroma_db/` and will be reused on subsequent runs.
- Driver memory is set to 4 GB by default in the Spark session config — increase this if you encounter out-of-memory errors on larger machines.
 
---
 
## Execution Environment
 
| Part | Environment |
|---|---|
| Part 1 – Distributed Data Processing with Spark | Google Colab |
| Part 2 – RAG Pipeline over Transportation Documents | Local execution |
| Part 3 – Integrated Analytics Application | Local execution |
 
---
 
## AI Usage Disclosure
 
The following AI tools were used in the development of this assignment:
 
- **GitHub Copilot** – Used for inline code suggestions to accelerate development and assist with debugging.
- **ChatGPT** – Used to help structure the assignment based on lab documentation and to explore new features for improving code efficiency.
- **Claude** – Used for generating test set questions and producing this README file.