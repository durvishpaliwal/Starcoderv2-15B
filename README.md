🚀 C# Instruction-Tuning Pipeline with StarCoder2-15B

This project adapts the StarCoder2 Self-Alignment pipeline to the C# programming language, using Stack v2 as the code source. The objective is to build a dataset of high-quality instruction-response pairs for fine-tuning instruction-following large language models such as StarCoder2-15B.

📌 Project Overview

🎯 Goal

To generate a C#-specific instruction-tuning dataset by:

Extracting clean and useful functions from Stack v2.
Converting them into natural language commands and instructions.
Using an LLM to generate accurate, aligned responses.
Validating responses to retain only high-quality pairs.
🛠️ Pipeline Components

1. Seed Dataset Curation

Filtered C# code snippets from Stack v2 using language metadata.
Removed duplicates using SHA1 hashing.
Applied structural filtering via Tree-sitter to retain only functions with meaningful return values.
Output: seed.parquet file with 1,942 unique entries, each with an id and seed field.
2. Self-OSS-Instruct Pipeline

Implemented as a multi-step transformation process:

S → C (Seed → Command):
Generated a concise natural language command describing the code’s purpose.
C → I (Command → Instruction):
Rephrased the command into a full user-style instruction (e.g., “Write a function to…”).
I → R (Instruction → Response):
Used StarCoder2-15B (via a vLLM API) to generate accurate C# responses for each instruction.
3. Self-Validation

Automatically checked that each generated response aligns with the given instruction.
Used heuristics such as structural checks, output presence, and syntax validity.
Ensured only consistent and useful instruction-response pairs were retained.
📂 Output Files

seed parquet file: Final cleaned seed dataset (C# code)
I-R pair jsonl file: Instruction-response pairs ready for training
Intermediate files saved between S→C→I→R stages for transparency and reproducibility
🧰 Tech Stack

Python
Tree-sitter (C#)
Hugging Face Datasets
vLLM OpenAI-compatible server
tqdm, hashlib, pandas, pyarrow
🔗 References

StarCoder2-15B on Hugging Face
The Stack v2 Dataset
StarCoder2 Self-Alignment GitHub
✅ Project Status

✅ Seed curation complete
✅ Instruction-response generation complete
Feel free to explore, fork, and build on top of this pipeline for other languages like Java or C++!

Team

Yash Shah - yks@njit.edu

Durvish Paliwal - dp2225@njit.edu

Pruthvi Kadam - pk759@njit.edu
