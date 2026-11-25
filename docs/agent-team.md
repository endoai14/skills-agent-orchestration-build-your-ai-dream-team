# Agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate Mona's Project Pulse dashboard team:

- **Orchestrator** - Coordinates the specialist agents, turns the plan into dependency-aware phases, assigns file scopes, and verifies the integrated result. It uses the Claude Opus 5.5 (copilot) model and is defined in [`.github/agents/orchestrator.agent.md`](../.github/agents/orchestrator.agent.md).
- **Planner** - Researches the repository and requirements, identifies dependencies and edge cases, and produces ordered implementation steps with file assignments and validation expectations. It uses the Claude Opus 5.5 (copilot) model and is defined in [`.github/agents/planner.agent.md`](../.github/agents/planner.agent.md).
- **Designer** - Owns UI/UX, accessibility, information hierarchy, interaction flow, responsive behavior, and polished Project Pulse visual styling. It uses the Gemini 3.7 Flash (copilot) model and is defined in [`.github/agents/designer.agent.md`](../.github/agents/designer.agent.md).
- **Coder** - Implements the dashboard and supporting runnable-app configuration with clear, testable code, then validates the result. It uses the GPT-5.5 (copilot) model and is defined in [`.github/agents/coder.agent.md`](../.github/agents/coder.agent.md).
