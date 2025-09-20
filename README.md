# Special Barnacle

This project uses LLMs and retrieval-augmented generation (RAG) to generate data transformation rules between a source and target schema.

---

## High-Level Strategy

1. **Schema Ingestion**
   - Read source and target schema files (Excel/CSV) into pandas DataFrames.

2. **Chunking**
   - For the source schema, create a "chunk" for each field using:  
     `TRIMMED COLUMN NAME, Subject Area, Data Type, Business Definition, Table Name, Column Name`
   - For the target schema, create a "chunk" for each field using:  
     `Table Name, Column Name, Data Type, Description, Sample Value`

3. **Filtering**
   - Exclude any source fields marked as "not to be used", "do not use", or "deprecated".

4. **Embedding**
   - Generate OpenAI embeddings for each chunk in both source and target schemas.

5. **Retrieval (RAG)**
   - For each target field, retrieve the top-N most relevant source fields using a combination of:
     - Semantic similarity (cosine similarity of embeddings)
     - BM25 keyword-based search

6. **Transformation Rule Generation**
   - For each target field, send the target chunk and its top-N relevant source chunks to the LLM.
   - The LLM generates a transformation rule in a structured JSON format.

7. **Output**
   - All transformation rules are saved to `03_output/transformation_rules.json`.

---

## Usage

1. **Install dependencies**
    ```bash
    pip install -r requirements.txt
    ```

2. **Set your OpenAI API key**
    - Add your key to a `.env` file:
      ```
      OPENAI_API_KEY=your-key-here
      ```

3. **Prepare your schemas**
    - Place your source schema Excel at `./01_input/01_source_CTR.xlsx`
    - Place your target schema Excel at `./01_input/02_Target.xlsx`

4. **Run the notebook**
    - Open `01_schema_provider.ipynb` in VS Code or Jupyter.
    - Execute all cells.

5. **Output**
    - The transformation rules will be saved as `./03_output/transformation_rules.json`.

---

## Requirements

- Python 3.8+
- Packages: `pandas`, `openai`, `python-dotenv`, `rank_bm25`, `numpy`, `scipy`

---
