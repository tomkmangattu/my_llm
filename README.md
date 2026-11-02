# my_llm

A hands-on learning project for understanding how Large Language Models (LLMs) work, by building a small GPT-style model from scratch.

The training corpus is [the-verdict.txt](the-verdict.txt), the short story *The Verdict* by Edith Wharton. It's a public-domain text, small enough to experiment with on a laptop.

## What's covered so far

| Notebook | Topic |
| --- | --- |
| [sample_encoding.ipynb](sample_encoding.ipynb) | Loading the text, splitting it into tokens with regex, building a vocabulary, and writing simple tokenizers (`SimpleTokenizerV1`, and `SimpleTokenizerV2` with the `<\|endoftext\|>` and `<\|unk\|>` special tokens) |
| [byte_pair_encoding.ipynb](byte_pair_encoding.ipynb) | Byte Pair Encoding (BPE) with the GPT-2 tokenizer from `tiktoken`, building input/target pairs with a sliding window, and starting a PyTorch `Dataset`/`DataLoader` |

## Prerequisites

- [uv](https://docs.astral.sh/uv/), the Python package and project manager
- Python 3.12 (uv can install it for you)

Install uv if you don't have it:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## Setup

### 1. Get the project

To clone this repository:

```bash
git clone <repo-url> my_llm
cd my_llm
```

To start a fresh project from scratch instead (this is how this repo was created):

```bash
uv init --python 3.12 my_llm
cd my_llm
```

### 2. Create and activate a virtual environment

```bash
uv venv
source .venv/bin/activate
```

On Windows, activate it with `.venv\Scripts\activate`.

### 3. Install dependencies

```bash
uv pip install --reinstall -r requirements.txt
```

This installs the packages listed in [requirements.txt](requirements.txt): `torch`, `tiktoken`, `jupyterlab`, `numpy`, `pandas`, `matplotlib`, `tensorflow`, `tqdm`, and `psutil`.

### 4. Register the Jupyter kernel

```bash
uv run python -m ipykernel install --user --name=my-llm-kernel --display-name "Python (my llm)"
```

This makes the virtual environment available as a kernel called **Python (my llm)** in Jupyter, and in VS Code.

### 5. Start Jupyter

```bash
uv run jupyter notebook
```

Open a notebook and select the **Python (my llm)** kernel (Kernel → Change Kernel).

## Quick reference

```bash
uv init --python 3.12 my_llm
uv venv
source .venv/bin/activate
uv pip install --reinstall -r requirements.txt
uv run python -m ipykernel install --user --name=my-llm-kernel --display-name "Python (my llm)"
uv run jupyter notebook
```

## Project structure

```
my_llm/
├── the-verdict.txt            # Training text
├── sample_encoding.ipynb      # Tokenization basics and a simple tokenizer
├── byte_pair_encoding.ipynb   # BPE tokenizer (tiktoken) and the data loader
├── main.py                    # Entry point (placeholder)
├── requirements.txt           # Dependencies installed with uv pip
├── pyproject.toml             # Project metadata
└── uv.lock                    # Locked dependency versions
```

## Notes

- If `the-verdict.txt` is missing, the first cells of `sample_encoding.ipynb` download it with `requests`. If `requests` isn't installed, run `uv pip install requests`.
- To check that the notebook uses the right environment, run `!which python` in a cell. The path should point into `.venv/`.

## References

- Sebastian Raschka, *Build a Large Language Model (From Scratch)*, and the companion repo [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)
