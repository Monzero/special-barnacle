# Special Barnacle

This project uses LLMs to generate data transformation rules between a source and target schema.

## Features

- Reads source and target schemas from CSV files.
- Converts schemas to JSON format.
- Uses OpenAI GPT models to generate transformation rules for each target field.
- Saves transformation rules as a JSON file in the `03_output` folder.

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
    - Place your source schema CSV at `./01_input/01_ctr_schema.csv`
    - Place your target schema CSV at `./01_input/02_target_schema.csv`

4. **Run the notebook**
    - Open `01_schema_provider.ipynb` in VS Code or Jupyter.
    - Execute all cells.

5. **Output**
    - The transformation rules will be saved as `./03_output/transformation_rules.json`.

## Customization

- Update the prompt in the notebook to change the transformation logic or output format.
- You can provide different target schemas to generate new rules.

## Requirements

- Python 3.8+
- Packages: `pandas`, `openai`, `python-dotenv`

---
