# SGR-BENCH Evaluation Protocol

This document summarizes the controlled evaluation setup used in the main SGR-BENCH evaluation.

## 1. Controlled CLI Evaluation Scope

The configuration described here applies to the eight CLI-based systems used in the main evaluation:

- Kimi K2.5
- GLM-5.1
- Qwen3.6-Plus
- DeepSeek V4 Pro
- Seed-2.0 Pro
- Claude Opus 4.7
- Gemini 3.1 Pro
- GPT-5.5

All eight systems are evaluated under a common search-fetch-PDF retrieval setup. Observed performance differences therefore reflect system behavior under a matched retrieval-tool regime rather than differences in the available external tools.

## 2. Prompt Template and Controlled Protocol

All agents receive the same task prompt. Each prompt consists of:

- the current date
- the benchmark task instruction
- the required structured output schema

Prompts do not provide a start URL. They instruct agents to solve the task through the designated search, fetch, and PDF tools while prohibiting alternative retrieval paths.

## 3. Exposed Tools and Runtime Restrictions

Across all eight CLI systems, the runtime exposes only three external retrieval tool classes:

- Serper search
- fetch-based webpage reading
- PDF reading

For the Claude Code systems, each run uses a project-level MCP configuration under a strict MCP configuration so that only the designated search, fetch, and PDF tools are available during execution. A companion settings file additionally disables the Claude-native WebSearch and WebFetch tools, ensuring that all evaluated systems operate under the same external retrieval-tool budget.

GPT-5.5 is executed through Codex CLI rather than Claude Code CLI, but its implementation is aligned to the same evaluation controls, including prompt constraints, exposed retrieval tools, task isolation, and runtime budget.

## 4. Execution Budget and Task Isolation

Each task is executed in an independent session, with no context shared across tasks.

The execution budget is defined as follows:

- maximum runtime per task: 6000 seconds
- stalled threshold: 3000 seconds without trace progress
- answer extraction polling interval: every 5 seconds during execution
- effort setting for all CLI-based systems: medium

## 5. Commercial System Evaluation

Google Search AI Mode, Gemini Deep Research, and OpenAI Deep Research are evaluated through manual interaction with their respective web interfaces.

For these systems:

- the task prompt is provided as-is
- the final output is collected without modification
- no intermediate trajectory data is available
