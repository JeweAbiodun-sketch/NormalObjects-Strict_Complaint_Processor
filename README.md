# Strict Complaint Processor

A LangGraph-based complaint processor for fictional **Downside Up** incidents. The workflow takes a raw complaint, classifies it, validates whether it belongs in scope, and either rejects it politely or generates a structured resolution path.

## Overview

This project is implemented as a Jupyter notebook:

- `normalobjects_langgraph.ipynb`

The notebook builds a stateful LangGraph pipeline with these steps:

1. `intake` - initial category classification
2. `validate` - check whether the complaint is actually Downside Up-related
3. `reject` or `categorize` - branch based on the validation result
4. `resolve` - generate actionable resolution steps
5. `output` - format the final response

The state is tracked through a shared `ComplaintState` object so every run is auditable and reproducible.

## Tech Stack

- Python
- LangGraph
- LangChain
- OpenAI API
- `python-dotenv`
- Jupyter Notebook

## Requirements

The notebook expects:

- Python 3.13+ recommended
- An OpenAI API key
- Internet access for model calls

## Setup

1. Create and activate a virtual environment.
2. Install the notebook dependencies:

```bash
pip install langgraph langchain langchain-openai langchain-core openai ipywidgets python-dotenv
```

3. Create a `.env` file in the project root with:

```env
OPENAI_API_KEY=your_api_key_here
OPENAI_MODEL=gpt-5.2
```

`OPENAI_MODEL` is optional. If omitted, the notebook falls back to `gpt-5.2`.

## How to Run

1. Open `normalobjects_langgraph.ipynb` in Jupyter, VS Code, or another notebook environment.
2. Run the cells from top to bottom.
3. Enter or modify the sample complaints in the test section to see how the graph behaves.

The notebook includes:

- Graph construction
- A `process_complaint()` helper
- A small test suite with valid and invalid complaints
- A results summary with workflow traces

## Workflow Logic

The graph uses a conditional branch after validation:

- Valid complaints continue to `categorize`
- Invalid complaints go to `reject`

For valid complaints, the notebook also assigns severity and generates resolution steps before formatting the final response.

## Example Output

For valid complaints, the final response includes:

- Category
- Severity
- Workflow path
- Complaint text
- Resolution steps

For invalid complaints, the notebook returns a short rejection message explaining that the system only handles Downside Up-related issues.

## Project Notes

- The pipeline is designed as a state machine rather than a freeform agent.
- The `workflow_path` field provides a trace of every node visited.
- The notebook compares LangGraph against a more open-ended LangChain agent approach at the end.

## Files

- `normalobjects_langgraph.ipynb` - main implementation and demo
- `.env` - local environment variables, including the API key

## License

No license has been specified for this project.
