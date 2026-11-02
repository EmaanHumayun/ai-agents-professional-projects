# Project Specification: DevOps AI Operations Agent (AIOps)

---

### 1. Problem Statement
SRE teams suffer alert fatigue and slow incident response times during production outages.

### 2. Target Users
Site Reliability Engineers, DevOps leads, system administrators.

### 3. Learning Objectives
- Master the underlying concepts of DevOps AI Operations Agent (AIOps).
- Build deterministic tools with strict Pydantic v2 schemas.
- Structure resilient agent cognitive loops with error recovery and retries.
- Evaluate token consumption, inference latency, and groundedness.

### 4. Prerequisites
- Python 3.10+ programming proficiency (OOP, async, type annotations).
- Basic understanding of REST APIs, HTTP status codes, and JSON schemas.
- Familiarity with Git version control and environment variables.

### 5. Concepts Covered
Log anomaly classification, Prometheus alert correlation, runbook automation, least-privilege SSH execution, audit logging.

### 6. Tools and Technology
- **Language / Runtime**: Python, Paramiko, Prometheus Client, Docker SDK, Alertmanager
- **Validation**: Pydantic v2
- **Testing**: Pytest, Mocking
- **Environment**: Python `venv`, `.env`

### 7. Functional Requirements
- **FR-01**: Ingest natural language inputs (Prometheus Alertmanager webhooks and system log streams.).
- **FR-02**: Enforce system prompt boundaries and manage conversational history.
- **FR-03**: Select and execute appropriate tools when required.
- **FR-04**: Track token consumption and compute execution latency.
- **FR-05**: Return grounded outputs (Root cause analysis report, recommended runbook steps, operator approval prompt.).

### 8. Non-Functional Requirements
- **NFR-01 (Reliability)**: Gracefully handle network timeouts and API exceptions with retries.
- **NFR-02 (Security)**: Zero plain-text credentials in logs or source files.
- **NFR-03 (Performance)**: Maintain sub-second latency for local tool execution.
- **NFR-04 (Maintainability)**: Clean separation between prompts, tools, memory, and services.

### 9. Agent Workflow Design
```
[ User Input ] ---> [ Assemble Context & History ]
                               |
                               v
                     [ LLM Cognitive Step ]
                               |
            +------------------+------------------+
            |                                     |
    (Tool Call Required)                    (Goal Fulfilled)
            |                                     |
            v                                     v
[ Validate Pydantic Schema ]              [ Output Return ]
            |
            v
[ Execute Deterministic Tool ]
            |
            v
[ Append Tool Result to Context ]
            |
            +---> (Loop back to LLM for final response)
```

### 10. Trigger Definitions
- Terminal prompt input, API endpoint trigger, or automated test invocation.

### 11. Actions and Integrations
- Tool execution (calculation, search, database query, API dispatch).
- LLM inference request and response parsing.

### 12. Input and Output Data Formats
- **Input**: Prometheus Alertmanager webhooks and system log streams.
- **Output**: Root cause analysis report, recommended runbook steps, operator approval prompt.

### 13. Error Handling
- Invalid tool parameters: Catch validation error and feed failure context back to model to retry.
- API rate limits: Exponential backoff with jitter (1s, 2s, 4s).
- Context overflow: Automatically trim oldest conversational turns while retaining the system prompt.

### 14. Authentication Requirements
- API keys loaded exclusively from environment variables via `.env`.

### 15. Security Requirements
- Treat all external documents and tool outputs as untrusted input.
- Defend against prompt injection using XML-tagged context boundaries.
- Never execute destructive database or file commands without explicit verification.

### 16. Testing Requirements
- **Unit Tests**: Test tool schemas and edge cases in isolation.
- **Integration Tests**: Verify full agent loop with simulated tool returns.
- **Evaluation Tests**: Measure tool selection precision and output groundedness.

### 17. Implementation Milestones
- **Milestone 1**: Project directory scaffolding and configuration templates.
- **Milestone 2**: Core prompts and tool schema definition.
- **Milestone 3**: Agent loop execution and memory integration.
- **Milestone 4**: Automated test suite and evaluation documentation.

### 18. Expected Deliverables
- Working Python source code in `src/`.
- Passing Pytest suite in `tests/`.
- Practical lab documentation in `labs/`.
- Independent assignments in `assignments/`.

### 19. Completion Criteria
- All automated unit and integration tests passing.
- Zero credentials or tokens in git history.
- Clean execution output with documented evaluation report.

### 20. Advanced Extensions
- Add distributed tracing spans using OpenTelemetry.
- Implement streaming response generation.
- Integrate local model fallback via Ollama.
