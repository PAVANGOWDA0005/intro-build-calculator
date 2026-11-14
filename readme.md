# Intelligent Calculator & MCP / LangSmith Evaluation Project

## Project Overview
This repository contains an intelligent calculator agent built using **LangChain**, **Groq (`openai/gpt-oss-20b`)**, and custom Python tools, demonstrating Model Context Protocol (MCP) integration and LangSmith tracing[cite: 2].

## Verification & Check Status Labels
- **MCP / Tool Integration Check**: **Demonstrated**. Custom tools (`add` for whole-number combining, `tree_distance` for level-ground geometric calculations) are fully integrated, validated, and tested with successful tool calls and missing-parameter handling[cite: 2].
- **LangSmith Tracing Check**: **Demonstrated**. Tracing context and custom run names (`intro_apples`, `intro_tree`, `intro_missing_angle`) are configured to track agent executions[cite: 2].

## Execution Results Summary
- **Apples Test (`5 + 10`)**: Invoked `add` tool $\rightarrow$ Returned `15`[cite: 2].
- **Tree Distance Test (`10m`, `30�`)**: Invoked `tree_distance` tool $\rightarrow$ Returned `17.32` meters[cite: 2].
- **Missing Parameter Handling**: Correctly identified missing elevation angle and asked the user for clarification without invoking the tool[cite: 2].
- **Fresh Query (`7 + 8`)**: Invoked `add(7, 8)` $\rightarrow$ Returned `15`[cite: 2].

## Files Included
- `intelligent_calculator.ipynb`: Jupyter notebook containing all environment setup, tool implementations, agent definitions, test runs, and saved execution outputs[cite: 2].
- `readme.md`: Project documentation, verification status, and check labels[cite: 2].


