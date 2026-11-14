# Intelligent Calculator Agent (LangChain & Groq)

## Project Overview
This repository contains the Google Colab implementation (`intelligent_calculator.ipynb`) of an Intelligent Calculator agent built with **LangChain** and **Groq (`openai/gpt-oss-20b`)**[cite: 1]. The notebook includes baseline LLM responses, role-prompted replies, custom tool binding (`add`, `tree_distance`), missing-parameter validation, execution tracing, and a fresh test run (`7 + 8`)[cite: 1].

## Verification & Check Status
- **Saved Notebook Outputs**: **Verified**. All code cell execution outputs are saved directly within the `.ipynb` file so reviewers can verify the runs[cite: 1].
- **Markdown Explanations**: **Included**. Detailed tool choices, missing-parameter behavior, and execution observations are documented inside the notebook's Markdown cells[cite: 1].
- **LangSmith Tracing**: Configured with project-level tracing (`intro-build-calculator`)[cite: 1].
- **Tool Integration**: Custom Python tools (`add` for whole numbers and `tree_distance` for level-ground geometry) are fully implemented and tested[cite: 1].
'@ | Set-Content -Path "readme.md" -Encoding UTF8
