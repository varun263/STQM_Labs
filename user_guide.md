# Postman + Newman CI/CD — User Guide

This short guide shows how to run API tests with **Postman** collections locally using **Newman** and automatically in **GitHub Actions**. It fits the needs of two documentation labs:

- **Lab 1** (review-based testing + version control) — you will submit this very file for peer review.
- **Lab 2** (automated documentation quality checks) — this file will be linted for spelling and style with GitHub Actions.

> Repository this guide targets: any simple Node/Express demo API that serves on `http://localhost:3000`. Adjust commands if your repo differs.

## Prerequisites

- Node.js 18+ and npm
- A Postman collection (e.g., `collections/demo.postman_collection.json`)
- (Optional) A Postman environment file (e.g., `environments/local.postman_environment.json`)
- Git + a GitHub repository

## Local Setup

```bash
# Install dependencies
npm ci

# Start the API (runs at http://localhost:3000)
node server.js
```

Verify the API is alive:

```bash
curl http://localhost:3000/health
```

## Run Postman Tests Locally with Newman

Install Newman (once):

```bash
npm i -g newman
```

Run the collection:

```bash
newman run collections/demo.postman_collection.json   -e environments/local.postman_environment.json   -r cli,html --reporter-html-export reports/newman.html
```

Open the HTML report from `reports/newman.html` in your browser.

## CI/CD with GitHub Actions (Newman) — Quick Reference

A typical job looks like:

```yaml
# .github/workflows/api-tests.yml (example)
name: API Tests (Postman + Newman)

on:
  push:
  pull_request:

jobs:
  newman:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm ci
      - name: Start API
        run: |
          node server.js &
          npx wait-on http://localhost:3000
      - name: Run Newman with HTML report
        run: |
          npx newman run collections/demo.postman_collection.json             -e environments/local.postman_environment.json             -r cli,html --reporter-html-export reports/newman.html
      - name: Upload HTML report
        uses: actions/upload-artifact@v4
        with:
          name: newman-report
          path: reports/
```

## Reviewer Checklist
- [ ] Steps run locally
- [ ] Terminology is consistent
- [ ] Spelling/Markdown checks pass


## Documentation Quality Checks (Lab 2)

This repository includes a workflow that lints Markdown and runs a spell-check:

- **markdownlint** checks common Markdown issues.
- **codespell** catches frequent spelling mistakes.

The workflow lives at `.github/workflows/docs-quality.yml`. Configuration files:

- `.markdownlint.yaml` — disables a few noisy rules (line length, etc.).
- `.codespellrc` — skip folders and ignore domain words like “Postman”.

## Troubleshooting

- **API won’t start in CI:** Ensure `server.js` starts quickly and listens on `0.0.0.0:3000`. Add `npx wait-on http://localhost:3000` before running Newman.
- **Newman can’t find the collection:** Check the relative paths inside your repo.
- **Lint failures (Lab 2):** Open the failed GitHub Actions job, read the logs, fix the lines in `user_guide.md`, push again until the job is green.

## Glossary

- **Postman collection:** A JSON file describing API requests and tests.
- **Newman:** A CLI runner for Postman collections.
- **CI/CD:** Continuous Integration / Continuous Delivery pipelines.
- **Linting:** Automated checks for style and common errors.
## Lab 2 – CI Checks (Fixed)

### Common mistakes (for the bot to catch)
- This sentence definitely contains no typos now.
- In this environment we test the linter.

**Next steps**
- Fix these issues without changing anything else in the file.
