# 🏛️ Instrumental Centralized Engineering Infrastructure (.github)

This repository serves as the single source of truth for organization-wide templates, shared CI/CD workflows, and community health settings.

---

## 🛠️ GitHub Actions (Shared CI/CD)

We use **GitHub Actions Reusable Workflows** to maintain standard security, linting, and testing pipelines without duplicating code across repositories.

### Available Workflows

* **`pr-template-check.yml`**: Enforces the PR description template (`.github/pull_request_template.md`).
  * *Path:* `dfxmachina/.github/.github/workflows/pr-template-check.yml@main`

### How to use it in your Project Repositories

To plug a project repository into our shared CI, create a `.github/workflows/ci.yml` file in your project and reference this repository. Here's an example:

```yaml
name: CI

on:
  # Include edited so a description-only fix re-runs the check, not just the first push.
  pull_request:
    branches: [ main ]
    types: [opened, edited, reopened, synchronize]

jobs:
  run-global-ci:
    uses: dfxmachina/.github/.github/workflows/pr-template-check.yml@main
```

---

## 📝 Global Pull Request Template

The file located at `/.github/pull_request_template.md` acts as the organization-wide default for all incoming PRs.

* 💡 **Automatic Inheritance:** Any repository in our organization that does not have its own local PR template will automatically inherit this one.
* ⚠️ **Local Overrides:** If a specific project requires custom PR parameters (e.g., specialized deployment steps), you can override this global configuration by creating a local `.github/pull_request_template.md` inside that specific repository.

---

## 🔧 Maintenance & Contributions

Because changes to this repository can affect **all active pipelines and pull requests across the entire organization**, please adhere to the following rules:

1. **Protect the Main Branch:** Direct commits to `main` are disabled. All changes must be made via a pull request.
2. **Testing Workflows:** When editing files in `.github/workflows/`, test your changes on a dedicated sandbox branch or sandbox repository before merging.
3. **Pinning Versions:** When updating project repositories to use new workflow features, you can pin to a specific commit or tag (e.g., `@v1`) instead of `@main` to prevent breaking changes.

---
💡 *Questions or need modifications? Contact the **SRE team**.*
