---
layout: page
title: 8xEngineers
description: A lightweight journal and note-taking extension integrated within Visual Studio Code for seamless progress tracking and organization.
img: assets/img/vscode-journal.png
importance: 1
category: work
---

This **8xEngineers** helps developers efficiently track, document, and organize daily progress, tasks, and notes—directly within the Visual Studio Code (VSCode) environment. By reducing context switching and integrating essential productivity tools, the extension is tailored for both individual developers and collaborative teams.

[🔗 View the code on GitHub](https://github.com/8xEngineers/cse210-fa24-group12)

---

### Project Goals

- Deliver an integrated journaling solution for developers within VSCode.
- Enable quick logging of bugs, snippets, and ideas for easy future reference.
- Support both solo and team workflows via an embedded dashboard.
- Minimize workflow interruptions through an all-in-one extension.

---

### User Persona & Use Cases

- **Developers**: Seamless note and task tracking during coding sessions.
- **Teams**: Share project notes and decisions inside VSCode.
- **Collaborators**: Prefer documenting and managing issues without external tools.
- **Power users**: Need fast, intuitive capture and recall of information.

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/user-persona.png" class="img-fluid rounded z-depth-1"%}
</div>

---

### Features

- **File Tagging**: Tag files directly in the navigation bar to quickly organize by category or status.
- **Task & Issues Dashboard**: Sidebar dashboard for daily notes, todo lists, and issue tracking.
- **Integrated Workflow**: Unified place for journaling, minimizing the need to leave the IDE.
- **CI/CD Pipeline**: Automated checks for code quality; rapid iteration.
- **Merged Codebases**: Harnessed the strengths of two mature plugins for improved functionality.

---

### Technical Overview

- Built with **TypeScript** and **Node.js**, using the VSCode extension API.
- Modular, extensible design—future features like markdown notes and advanced dashboards can be added easily.
- CI/CD pipeline with ESlint for code checks.
- Careful dependency management for merging plugin codebases.

---

### CI/CD Pipeline

A robust CI/CD pipeline ensures every code change is checked, tested, and integrated. The pipeline includes:

- **Automated Linting:** Uses ESLint (`.github/workflows/eslint.yaml`) for style and standards.
- **Automated Build & Tests:** All changes trigger test runs (`.github/workflows/test.yml`) to verify features.
- **Code Review Integration:** PRs kick off checks before merge.
- **Continuous Deployment:** Passing changes are auto-merged & deployed for rapid iteration and reliability.

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/ci-cd.png" class="img-fluid rounded z-depth-1 w-75"%}
    <p>The CI/CD flow for the VSCode Journal Extension</p>
</div>

---

### Challenges & Solutions

- **Incomplete Source**: Original codebases were not feature-complete, requiring significant research and refactoring.
- **Dependency Conflicts**: Merging plugins led to versioning issues, solved by systematic dependency management.
- **Testing & Linting**: Started with super-lint and migrated to ESLint for advanced config.
- **Learning Curve**: Ramp-up required for VSCode plugin APIs and architecture.

---

### Demo Video

Watch our feature walkthrough and see the extension in action:

<!-- Replace the URL below with your actual YouTube demo link -->
<div class="col-sm mt-3 mt-md-0 text-center">
  <a href="https://www.youtube.com/watch?v=4PN8Am-AW_Y" target="_blank" rel="noopener">
    {% include figure.liquid path="assets/img/demo-video.png" class="img-fluid rounded z-depth-1 w-60" %}
  </a>
  <p>
    Click the image or 
    <a href="https://www.youtube.com/watch?v=4PN8Am-AW_Y" target="_blank" rel="noopener">watch on YouTube</a>.
  </p>
</div>


---

### Key Takeaways

- **In-IDE journaling** streamlines documentation and task management for busy developers.
- Modular codebases allow rapid feature development, but require careful integration.
- Minimal, user-focused design drives adoption and everyday usability.
- Collaborative retrospectives and paired workups kept the project aligned and agile.

---

