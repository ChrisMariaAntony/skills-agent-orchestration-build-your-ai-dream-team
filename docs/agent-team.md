# Agent team for Mona's Project Pulse dashboard

- Orchestrator, Planner, Coder, and Designer.
- The model assigned to each agent.
- The responsibility of each agent.
- The .github/agents/ file for each agent.
- How the team will work together to build Project Pulse.

We are using GitHub Copilot CLI in a Codespace to orchestrate the work for Mona's Project Pulse dashboard. The custom team is defined under `.github/agents/` and includes a small specialist set that coordinates planning, design, implementation, and delivery.

- Planner — Model: Claude Opus 5.5 (copilot). Responsibility: researches the repository, checks docs and dependencies, identifies risks and edge cases, and produces a structured implementation plan. Definition: `.github/agents/planner.agent.md`.
- Designer — Model: Gemini 3.7 Flash (copilot). Responsibility: focuses on UX, accessibility, visual hierarchy, responsive layout, and dashboard styling for the Project Pulse interface. Definition: `.github/agents/designer.agent.md`.
- Coder — Model: GPT-5.5 (copilot). Responsibility: implements code changes, fixes logic issues, and builds the runnable dashboard behavior within the assigned file scope. Definition: `.github/agents/coder.agent.md`.
- Orchestrator — Model: Claude Opus 5.5 (copilot). Responsibility: coordinates the Planner, Designer, and Coder agents, splits work into phases, assigns file ownership, and verifies that the integrated result fits the project goals. Definition: `.github/agents/orchestrator.agent.md`.

This team is intentionally lightweight: the Orchestrator manages execution flow, the Planner defines the implementation path, the Designer shapes the dashboard experience, and the Coder handles the code work. Together they let the project move from planning through implementation in a structured, low-conflict workflow.
