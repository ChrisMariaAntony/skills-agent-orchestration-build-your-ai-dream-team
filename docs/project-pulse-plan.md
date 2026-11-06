# Project Pulse Dashboard Implementation Plan

## Summary

Build a small static dashboard that helps contributors scan active projects, owners, status, recent activity, priority or risk, and a short contributor-friendly summary. The repository has no app implementation or front-end framework yet.

The app will load project records from `app/project-data.json`, render accessible project cards in `app/index.html`, and use responsive styling in `app/styles.css`. A `.vscode/launch.json` configuration will run the app from `app/` and open `index.html` so the dashboard appears instead of a directory listing.

## Ordered implementation steps

### 1. Agree on the implementation contract

- **Orchestrator:** Coordinate the file assignments and confirm the data shape, CSS hooks, and launch behavior before implementation.
- **Designer:** Define the visual hierarchy, accessibility requirements, responsive behavior, and CSS hooks, including `.dashboard` and `.project-card`.
- **Coder:** Confirm how the page will load and render the JSON data, how empty/error states will appear, and how the launch configuration will start and open the app.
- **Dependency:** This shared contract precedes implementation so HTML, CSS, data, and launcher assumptions agree.

### 2. Create the stylesheet, data, and launch configuration

After Step 1, the following independent file assignments can proceed in parallel:

- **Designer — `app/styles.css`:** Implement the agreed visual design, accessible contrast and focus treatment, readable spacing, responsive layout, and polished project-card styling. Include `.dashboard`, `.project-card`, rounded corners, and shadows.
- **Coder — `app/project-data.json`:** Create valid JSON with a top-level `projects` array. Every project must include `name`, `owner`, `status`, `recentActivity`, and `priority`. Add a concise `summary` property to support the contributor-friendly summary required by the brief. Use consistent, clear status and priority labels.
- **Coder — `.vscode/launch.json`:** Create strict JSON with a configuration named **Run Project Pulse Dashboard**. Set `cwd` to `${workspaceFolder}/app`, start a static HTTP server from that directory, and open `index.html` when the server is ready. Choose a launch mechanism supported by the Codespace and verify it actually starts the server and opens the page.
- **Dependency:** The data shape, CSS hooks, and launch requirements must be settled in Step 1.

### 3. Implement and integrate the page

- **Coder — `app/index.html`:** Create the page with the title **Project Pulse**. Reference `styles.css` and `project-data.json`; load the data and render a `.project-card` for each project, showing its name, owner, status, recent activity, priority, and contributor-friendly summary. Include clear loading, empty, and data-load error states.
- **Designer:** Review the integrated visual hierarchy, accessibility, and responsive presentation; provide feedback to the Orchestrator without editing Coder-owned files.
- **Dependency:** This step depends on the agreed data shape and stylesheet hooks from Steps 1–2. Coder owns `app/index.html` to avoid conflicting edits.

### 4. Validate and hand off

- **Coder:** Validate both JSON files, run the app, and resolve implementation defects within assigned files.
- **Designer:** Review the rendered dashboard at narrow and wide viewport sizes and report remaining design or accessibility concerns.
- **Orchestrator:** Coordinate fixes with explicit file ownership and report validation results and limitations. Keep the work within the requested static dashboard scope.

## File assignments and responsibilities

| File | Owner | Assignment |
|---|---|---|
| `app/index.html` | Coder | Semantic page structure, references to CSS/data, data loading, loading/empty/error states, and rendered project cards |
| `app/styles.css` | Designer | Visual design, accessibility and focus styling, responsive layout, and card styling |
| `app/project-data.json` | Coder | Sample project records with all required fields and a contributor-friendly `summary` |
| `.vscode/launch.json` | Coder | Strict JSON launch configuration, working directory, server startup, and browser target |

The **Planner** researches and documents the implementation plan only. The **Designer** owns visual design and CSS. The **Coder** owns data, page behavior, and launch configuration. The **Orchestrator** coordinates sequencing, integration, and validation; it does not take overlapping ownership of implementation files.

## Dependencies and parallel work decisions

- **Sequential:** Agree on the data schema, CSS hooks, and launcher behavior before implementation. Integrate the page after the data shape and stylesheet hooks are established. Run end-to-end validation after integration.
- **Parallel:** Once the shared contract is agreed, Designer can implement `app/styles.css` while Coder creates `app/project-data.json` and `.vscode/launch.json`; these have separate ownership.
- **No overlapping edits:** Keep each implementation file assigned to one agent. Designer's integrated review is feedback only; Coder makes any changes to `app/index.html`.
- **Orchestration:** If launch support requires an additional task or tooling file, the Orchestrator should resolve that scope with the team before changes are made.

## Edge cases and risks

- Loading JSON using `file://` may fail in the browser. Validate via the configured HTTP server.
- Empty data, malformed JSON, or a failed fetch should produce a useful empty or error state rather than a blank dashboard.
- Missing or empty values should not create broken or inaccessible cards.
- Status and priority must remain understandable without color alone and maintain adequate contrast.
- Long project names, summaries, or activity text must wrap without causing horizontal overflow.
- The chosen launch mechanism or required VS Code extension may not be available in the Codespace. Verify compatibility rather than assuming a Python debugger extension is installed.
- Port conflicts may prevent the local server from starting; report the failure clearly and stop any preview server after validation.

## Validation expectations

- Confirm all four assigned files exist and both JSON files parse (`app/project-data.json` and `.vscode/launch.json`).
- Verify `project-data.json` has a top-level `projects` array and every record has `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Verify `index.html` references both `styles.css` and `project-data.json`, and renders cards with the required fields and summary.
- Verify the stylesheet includes `.dashboard` and `.project-card`; review contrast, visible keyboard focus, readable spacing, and narrow-screen layout.
- Start **Run Project Pulse Dashboard** in VS Code. Confirm the server runs with `app/` as its working directory and the browser opens `index.html` showing the dashboard rather than a directory listing.
- Check the empty-data and failed-data-request states.
- Run the repository's existing exercise validation where applicable. Treat static checks as complementary to manual launch and UI validation; they do not prove the app runs correctly.

## Open questions

No product-scope questions remain. During implementation, verify which launch mechanism is supported in the Codespace without introducing undeclared tooling.
