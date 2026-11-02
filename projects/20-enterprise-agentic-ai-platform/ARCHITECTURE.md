# Architecture Document: Enterprise Agentic AI Platform

## System Overview
The Enterprise Agentic AI Platform organizes agent logic into modular, decoupled layers:

1. **Prompts Layer (`src/prompts/`)**: Defines system personas, few-shot examples, and ReAct instructions.
2. **Tools Layer (`src/tools/`)**: Contains deterministic functions with Pydantic schema validation.
3. **Memory Layer (`src/memory/`)**: Manages conversation history, context trimming, and persistent state.
4. **Agent Layer (`src/agents/`)**: Coordinates the perception-reasoning-action loop.
