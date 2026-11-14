# Intelligent Calculator Agent (LangChain & Groq)

## Project Overview
This repository contains the Google Colab implementation (`intelligent_calculator.ipynb`) of an Intelligent Calculator agent built with **LangChain** and **Groq (`openai/gpt-oss-20b`)**. The notebook demonstrates baseline LLM responses, role-prompted replies, custom tool binding, missing-parameter validation, and execution tracing.

---

## Tool Choices & Architecture
- **Model**: `ChatGroq(model="openai/gpt-oss-20b", temperature=0)` configured for deterministic tool selection and mathematical responses.
- **Custom Tools (`@tool`)**:
  - `add(a: int, b: int) -> int`: Combines two whole-number quantities.
  - `tree_distance(height_m: float, angle_deg: float) -> float | str`: Computes horizontal tree distance on level ground using `height_m / tan(radians(angle_deg))` rounded to 2 decimal places, with input guards ensuring positive finite height and an elevation angle strictly between `0` and `90` degrees.
- **Agent Execution (`create_agent`)**: Bound to `[add, tree_distance]` with system instructions enforcing single tool calls for complete inputs, clarifying questions when inputs are missing, and explicit units in final answers.

---

## Verification & Check Status Labels
- **Saved Notebook Outputs**: **Verified**. All code cells (Cells 1–16) contain saved execution outputs directly inside `intelligent_calculator.ipynb`.
- **LangSmith Tracing Check**: **Attempted (Configuration Warning Observed)**. The notebook executes `tracing_context` with custom run names (`intro_apples`, `intro_tree`, `intro_missing_angle`). In the saved run, interactive setup received an Agent ID containing spaces (`'intro build calculator'`) and `'us'` instead of a full `https://` endpoint URL, producing `EnvAddressError` / `TracerException` warnings in stderr while the underlying agent runs completed cleanly.
- **MCP Integration Check**: **Not Demonstrated in This Notebook**. This notebook uses standard LangChain `@tool` decorators (`add` and `tree_distance`) rather than an external MCP server/client transport; MCP server/tunnel setup was handled separately in the local environment.

---

## Summary of Recorded Notebook Runs
1. **Baseline & Role-Prompted LLM Calls**:
   - Plain prompt (`5 + 10` apples) $\rightarrow$ `"There are 15 apples in total."`
   - Patient math tutor system prompt $\rightarrow$ `"There are 15 apples."`
2. **Direct Tool Unit Tests**:
   - `add({"a": 5, "b": 10})` $\rightarrow$ `15`
   - `tree_distance({"height_m": 10, "angle_deg": 30})` $\rightarrow$ `17.32`
   - `tree_distance({"height_m": 10, "angle_deg": 0})` $\rightarrow$ `"Invalid angle. Supply an angle strictly between 0 and 90 degrees."`
3. **Agent Runs (`show_run`)**:
   - **Apples (`5 + 10`)**: 1 tool request (`add {'a': 5, 'b': 10}`) $\rightarrow$ `"There are **15 apples** in total."`
   - **Tree Distance (`10 m`, `30°`)**: 1 tool request (`tree_distance {'angle_deg': 30, 'height_m': 10}`) $\rightarrow$ `"The horizontal distance from you to the tree is **17.32 m**."`
   - **Missing Angle (`10 m`, no angle)**: 0 tool requests $\rightarrow$ Prompted the user to provide the angle of elevation in degrees.
   - **Fresh Test (`7 + 8` apples)**: 1 tool request (`add {'a': 7, 'b': 8}`) $\rightarrow$ `"They have a total of **15 apples**."`
