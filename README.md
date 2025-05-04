# HyperGraphRAG: Knowledge Graph RAG System

## Prerequisites

### Environment Setup
1. Install Python 3.11+
2. Create a virtual environment
```bash
python -m venv hypergraphrag
source hypergraphrag/bin/activate  # On Windows use: hypergraphrag\Scripts\activate
```

3. Clone the repository
```bash
git clone https://github.com/your-repo/HyperGraphRAG.git
cd HyperGraphRAG
```

4. Install dependencies
```bash
pip install -r requirements.txt
```

### Configuration
1. Set OpenAI API Key
```python
import os
os.environ["OPENAI_API_KEY"] = "your-openai-api-key"
os.environ["OPENAI_API_BASE"] = "https://api.openai.com/v1"  # Or your custom endpoint
```

## Project Structure

### Key Scripts
- `script_construct.py`: Build knowledge graph
- `script_query.py`: Query the knowledge graph

## Workflow

### 1. Data Preparation
Create `example_contexts.json` with your input data:
```json
[
  {
    "domain": "Medicine",
    "topic": "Hypertension Guidelines",
    "content": "Your medical text content here..."
  }
]
```

### 2. Build Knowledge Graph
```python
 # Create working directory
        working_dir = "expr/medical_hypergraph"
        os.makedirs(working_dir, exist_ok=True)

        # Initialize HyperGraphRAG
        rag = HyperGraphRAG(working_dir=working_dir)

        # Load context data
        with open("example_contexts.json", "r", encoding='utf-8') as f:
            contexts = json.load(f)

        # Convert contexts to text list
        context_texts = [
            f"Domain: {context['domain']}\nTopic: {context['topic']}\nContent: {context['content']}"
            for context in contexts
        ]
```
Change "example_contexts.json"

### 3. Query Knowledge Graph
```python
query_text = 'How strong is the evidence supporting a systolic BP target of 120–129 mmHg in elderly or frail patients, considering potential risks like orthostatic hypotension, the balance between cardiovascular benefits and adverse effects, and the feasibility of implementation in diverse healthcare settings?'
```
Change query_text

## Run
```bash
cd /root/autodl-tmp/clash
./clash -d .
```
Open another powershell
```bash
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
```
Build Knowledge Graph
```bash
cd /root/autodl-tmp/HyperGraphRAG
python script_construct.py
```
Query Knowledge Graph
```bash
cd /root/autodl-tmp/HyperGraphRAG
python script_query.py
```
