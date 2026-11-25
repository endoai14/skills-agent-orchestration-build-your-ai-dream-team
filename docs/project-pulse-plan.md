# Project Pulse dashboard implementation plan

## Goal

Build Mona's lightweight static Project Pulse dashboard so contributors can quickly see active projects, owners, status, recent activity, priority or risk, and a short contributor-friendly summary. Follow `.github/project-pulse-brief.md`: use vanilla HTML, CSS, and JSON, with a polished card-based interface.

## Responsibilities and file assignments

- **Designer — `app/styles.css`:** Define the responsive layout, visual hierarchy, accessible contrast, readable spacing, and polished project-card styling. Include `.dashboard` and `.project-card` hooks, clear status badges and priority treatment, rounded corners, and shadows. Coordinate the selectors and visual states with Coder before integration.
- **Coder — `app/project-data.json`:** Create valid JSON with a top-level `projects` array. Each project includes `name`, `owner`, `status`, `recentActivity`, and `priority`, plus a concise `summary` to meet the brief's contributor-friendly overview.
- **Coder — `app/index.html`:** Create the semantic page with the exact title `Project Pulse`, reference `styles.css` and `project-data.json`, and render the projects as visible `.project-card` elements that show name, owner, status, recent activity, priority, and summary. Include accessible labels and clear loading, empty, and data-load error states.
- **Coder — `.vscode/launch.json`:** Create strict JSON without comments and a deterministic launch configuration named `Run Project Pulse Dashboard`. Set `cwd` to `${workspaceFolder}/app`, serve that directory with `python3 -m http.server 5500`, and use `serverReadyAction` to open `http://localhost:%s/index.html` so the dashboard opens instead of a directory listing.

## Phases, dependencies, and parallel work

1. **Parallel foundation:** Designer defines `app/styles.css`; Coder defines `app/project-data.json` and `.vscode/launch.json`. These can proceed in parallel once the shared visual hooks and data fields above are agreed. Keep the scope explicit so Designer does not edit implementation or launch files.
2. **Sequential page integration:** Coder builds `app/index.html` after the CSS hooks and JSON schema are agreed, consuming the data and applying the agreed dashboard and project-card styles. The HTML depends on both the stylesheet contract and the JSON schema.
3. **Sequential end-to-end validation:** After all four assigned files exist, Coder and Orchestrator verify the integrated dashboard, data rendering, and launch experience. Launch validation depends on `index.html` being present.

## Validation expectations

- Parse `app/project-data.json` and `.vscode/launch.json` with `python3 -m json.tool`.
- Check that `app/index.html` has the exact `Project Pulse` title, references both assets, renders `.project-card` elements, and presents all required project fields including summary.
- Check that `app/styles.css` contains `.dashboard`, `.project-card`, responsive behavior, readable contrast, status/priority cues that are not color-only, `border-radius`, and `box-shadow`.
- Start `Run Project Pulse Dashboard` in VS Code and confirm it serves from `app/` and opens `index.html` with project cards rather than a directory listing. Also exercise loading, empty-data, and data-load error states as applicable.
- Run `bash scripts/validate-exercise.sh` for the repository's exercise checks.

## Dependencies and risks

The HTML rendering depends on the JSON field contract and CSS hooks; settle those in the parallel foundation phase before integration. The launch configuration must serve over HTTP for JSON loading and must target `index.html`. Keep the app dependency-free and deterministic; report any browser/runtime limitation rather than masking data-load failures.
