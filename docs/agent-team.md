# Agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate the custom agent team that builds Mona's Project Pulse dashboard.

- **Orchestrator** - Uses **Claude Opus 5.5 (copilot)**. It coordinates the Planner, Coder, and Designer, turns their work into ordered phases, manages file scopes and dependencies, and verifies the integrated result. Its definition is at `.github/agents/orchestrator.agent.md`.
- **Planner** - Uses **Claude Opus 5.5 (copilot)**. It researches the repository and requirements, identifies implementation dependencies and edge cases, and produces a practical plan for the team. Its definition is at `.github/agents/planner.agent.md`.
- **Coder** - Uses **GPT-5.5 (copilot)**. It implements the dashboard logic and supporting configuration, keeps changes testable and deterministic, and validates the assigned code. Its definition is at `.github/agents/coder.agent.md`.
- **Designer** - Uses **Gemini 3.7 Flash (copilot)**. It defines the UI/UX, accessibility, responsive layout, visual hierarchy, styling, and dashboard-specific design direction. Its definition is at `.github/agents/designer.agent.md`.
