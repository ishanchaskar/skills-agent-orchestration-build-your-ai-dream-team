# Project Pulse Dashboard Plan

## Goal

Build a lightweight static Project Pulse dashboard for Mona's contributors. It should make it easy to scan which projects are active, who owns them, their current status, recent activity, priority or risk, and a short contributor-friendly summary. The interface should use a polished, responsive card layout with clear visual hierarchy, readable spacing, and status badges.

The app consists of `app/index.html`, `app/styles.css`, and `app/project-data.json`, with `.vscode/launch.json` providing a VS Code launch configuration for the preview.

## Implementation phases

1. **Coordinate and confirm the plan — Orchestrator and Planner.** The Planner identifies the phases, file ownership, dependencies, and validation below. The Orchestrator assigns scoped work and keeps the implementation aligned with the brief.
2. **Agree the contract and design direction — Orchestrator, Planner, Designer, and Coder.** Agree the six project data fields, CSS and markup hooks, layout direction, accessibility approach, and the HTML contract before implementation begins.
3. **Prepare CSS and independent support inputs — Designer and Coder (parallel).** The Designer implements `app/styles.css` from the agreed hooks and design direction. In parallel, the Coder prepares `app/project-data.json` and `.vscode/launch.json`; these outputs do not depend on the finalized HTML.
4. **Finalize markup — Coder, after the contract and design direction.** The Coder implements `app/index.html` using the agreed project data fields and CSS/markup hooks. The Coder owns loading behavior and renders a visible card for each project.
5. **Integrate and validate — Orchestrator with Coder.** Check that the files work together, run the focused content and JSON checks, then launch the preview and confirm it opens the dashboard.

## File assignments

| File | Owner | Responsibilities |
|---|---|---|
| `app/index.html` | Coder | Create the accessible page markup with the exact title **Project Pulse**; reference `styles.css` and `project-data.json`; own loading behavior and render visible project cards using the `project-card` class and show each project's name, owner, status, recent activity, priority, and contributor-friendly summary. Apply the Designer's information hierarchy and accessibility guidance. |
| `app/styles.css` | Designer | Own the polished card styling, status and priority readability, visual hierarchy, readable spacing, accessibility, responsive behavior, and visual direction. Include `.dashboard` and `.project-card` selectors, `border-radius`, and `box-shadow`. |
| `app/project-data.json` | Coder | Provide valid JSON with a top-level `projects` array. Each project includes `name`, `owner`, `status`, `recentActivity`, `priority`, and a short contributor-friendly `summary`. Use illustrative examples unless Mona supplies real project data. |
| `.vscode/launch.json` | Coder | Create strict JSON (no comments) with a configuration named **Run Project Pulse Dashboard**. Set `cwd` to `${workspaceFolder}/app`, use `python3 -m http.server 5500`, and configure `serverReadyAction` to open `http://localhost:%s/index.html`. |

The Coder owns markup, data, loading behavior, and runnable app support in `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`. The Designer owns `app/styles.css`, including layout, information hierarchy, accessibility, responsive behavior, and visual direction. The Designer and Coder should coordinate on the contract and CSS/markup hooks before implementation to avoid conflicting edits.

## Agent responsibilities

- **Planner:** Research the request and repository patterns; define practical phases, file ownership, dependencies, parallel/sequential decisions, edge cases, validation expectations, and open questions. The Planner plans but does not implement.
- **Designer:** Own `app/styles.css` and guide the dashboard's layout, information hierarchy, accessibility, interaction flow, responsive behavior, and visual clarity. Implement a polished card-based design, status badges, readable spacing, clear priority treatment, and deterministic CSS hooks; report design decisions and validation recommendations.
- **Coder:** Own `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`. Implement accessible markup and data/loading behavior with clear, deterministic behavior. Keep the data and UI aligned, follow the agreed design direction, use strict JSON for the launch configuration, and validate the changes before reporting completion.
- **Orchestrator:** Coordinate the Planner, Designer, and Coder; assign explicit file scopes, sequence work when it has dependencies, run independent work in parallel, integrate and verify the result, and report blockers or remaining risks. The Orchestrator coordinates rather than implementing the app.

## Dependencies and work scheduling

- The data model must be agreed before the HTML renders project fields. Use `projects` as the top-level JSON key and include all six per-project fields: `name`, `owner`, `status`, `recentActivity`, `priority`, and `summary`.
- CSS/markup hooks and the design direction must be agreed before implementation, so Designer and Coder build against the same contract. The Coder also needs that contract and the design direction before finalizing HTML.
- **Parallel:** After the contract is agreed, Designer implements `app/styles.css` while Coder prepares `app/project-data.json` and `.vscode/launch.json`. These tasks have separate file scopes and no implementation dependency on one another.
- **Sequential:** Coder finalizes `app/index.html` after the agreed contract and design direction are available. Integration checks and the launch preview happen only after all four files exist and Designer and Coder outputs are complete.
- **Avoid overlapping edits:** Designer provides design guidance rather than editing the Coder-owned implementation files in parallel. If implementation scope is reassigned, coordinate it explicitly before work begins.

## Validation expectations

1. Parse `app/project-data.json` as JSON. Confirm it has a top-level `projects` array and that each project has `name`, `owner`, `status`, `recentActivity`, `priority`, and `summary`.
2. Check `app/index.html` for the exact title `Project Pulse`, references to `styles.css` and `project-data.json`, visible project cards with the `project-card` class, and rendered project name, owner, status, recent activity, priority, and summary.
3. Check `app/styles.css` for `.dashboard`, `.project-card`, `border-radius`, and `box-shadow`, and confirm the layout remains readable at narrower viewport widths.
4. Parse `.vscode/launch.json` as strict JSON with no comments. Confirm the configuration name is `Run Project Pulse Dashboard`, its `cwd` is `${workspaceFolder}/app`, its command is `python3 -m http.server 5500`, and its `serverReadyAction` opens `http://localhost:%s/index.html`.
5. Run **Run Project Pulse Dashboard** in VS Code. Confirm the browser opens the Project Pulse frontend at the configured URL, rather than a server directory listing, and that project cards display. Stop the preview server after the check.

## Assumptions and open questions

- Project data is not supplied in the brief. Any sample project names, owners, statuses, activity, priorities, and summaries are illustrative only unless Mona provides real data.
- The brief does not define a status vocabulary, priority/risk scale, summary length, or activity date format. Use plain, understandable sample values for the prototype and confirm Mona's preferred conventions before treating the sample data as authoritative.
- The dashboard is a static app served from `app/`; no backend, persistence, editing workflow, or other unsupported behavior is assumed.
