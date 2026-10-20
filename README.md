# Olympians

A notebook-based Persian question-answering project for Greek mythology. It combines a curated reference dataset, few-shot prompting, and Cohere chat models to generate short, grounded answers in Persian.

## Features

- Grounds answers in a curated JSON reference about Olympian gods.
- Uses few-shot examples to reinforce the expected answer format.
- Limits responses to four or five Persian words.
- Produces a CSV submission and a portable ZIP bundle for evaluation.

## Technology stack

- Python 3
- Jupyter Notebook
- Cohere via `langchain-cohere`
- LangChain Core
- pandas

## Architecture

```text
gods.json + few-shot examples
             │
             ▼
      system message and prompt
             │
             ▼
       Cohere chat model
             │
             ▼
data/questions.csv ──► submission.csv ──► result.zip
```

The notebook loads `gods.json` as its model context, builds a LangChain prompt, invokes Cohere for each question in `data/questions.csv`, and writes the resulting answers to `submission.csv`.

## Project structure

```text
.
├── Olympians.ipynb       # Main notebook and workflow
├── gods.json             # Persian reference data used by the notebook
├── questions.csv         # Root-level question dataset copy
├── data/
│   ├── gods.json         # Reference-data copy
│   └── questions.csv     # Evaluation questions used by the notebook
├── examples.csv          # Generated few-shot example export
├── submission.csv        # Generated answer export
├── model_configs.json    # Generated model configuration export
└── result.zip            # Generated evaluation bundle
```

## Prerequisites

- Python 3.10 or later
- A Cohere account and API key
- Internet access for Cohere API requests

## Installation

Create and activate a virtual environment, then install the notebook dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install jupyterlab pandas langchain-core langchain-cohere
```

On macOS or Linux, activate the environment with `source .venv/bin/activate`.

## Configuration

The notebook requests the Cohere key interactively and places it in `CO_API_KEY` only for the active process. Do not add an API key to the notebook, CSV/JSON datasets, or version control.

## Run the notebook

```powershell
jupyter lab Olympians.ipynb
```

Run the cells in order. When prompted, enter a valid Cohere API key. The question loop pauses after every ten requests to reduce the chance of hitting API rate limits.

## Usage

The completed workflow creates a DataFrame named `submission` with one `answer` column. Its final cell exports:

```text
submission.csv
examples.csv
model_configs.json
result.zip
```

`result.zip` contains the notebook and the three CSV/JSON evaluation artifacts.

## Development guidelines

- Preserve the Persian data and response requirement: they are intentional product behavior.
- Keep evaluation questions separate from few-shot examples.
- Do not commit API keys, tokens, local environments, or notebook checkpoints.
- Keep answers within the notebook's four-to-five-word limit.

## Testing

There is no automated test suite in this repository. Validate changes by opening the notebook, running the workflow with a valid Cohere API key, and confirming that `submission.csv` has one answer per row in `data/questions.csv`.

## Troubleshooting

| Symptom | Suggested action |
| --- | --- |
| Authentication error | Confirm that the Cohere API key entered at the prompt is valid. |
| Import error | Activate the virtual environment and install the dependencies listed above. |
| Rate-limit error | Wait before retrying; the notebook already pauses after every ten requests. |
| Incorrect submission shape | Re-run the question loop and verify that `submission` has a single `answer` column. |

## Security

See [SECURITY.md](SECURITY.md) for reporting guidance. Treat the Cohere API key as a secret and rotate it immediately if it is exposed.

## Contributing

Contributions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a change.

## License

No license file is currently included. All rights are reserved unless the repository owner adds an explicit license.
