# Collaboration Test Plan (Lab 3)

> **Purpose:** A short, practical test plan to practice *collaboration* workflows (branches, PRs, reviews, issues) on GitHub while documenting how you will test a simple API + docs repo. Replace placeholders in **ALL CAPS** with your details.

## 1. Document Control
- **Project/Repo:** STQM_Labs (example)
- **Version:** 0.1
- **Owner:** **YOUR_NAME**
- **Reviewers:** **FRIEND1**, **FRIEND2**
- **Dates:** Start **YYYY-MM-DD**, Target sign‑off **YYYY-MM-DD**

## 2. Scope
- **In scope:** Markdown documentation (`user_guide.md`), Postman collection smoke tests (if available), GitHub Actions docs-quality workflow.
- **Out of scope:** Full API functional testing, performance tests.

## 3. Objectives
- Ensure the docs are clear, correct, and pass automated checks.
- Exercise collaboration: branch strategy, PR reviews, issue tracking, approvals, and merge.
- Track defects and their resolution.

## 4. Roles & Responsibilities (RACI)
| Activity | Author | Reviewer A | Reviewer B | Maintainer |
|---|---|---|---|---|
| Draft test plan | R | C | C | A |
| Draft/update docs | R | C | C | A |
| Run CI checks | R | C | C | A |
| Raise defects | R | R | R | A |
| Approve PR | C | A | A | A |
> R = Responsible, A = Accountable, C = Consulted, I = Informed

## 5. Items to be Tested
- `user_guide.md` — formatting, spelling, clarity, completeness
- `.github/workflows/docs-quality.yml` — lints must pass
- Optional: Postman collection paths referenced in `user_guide.md`

## 6. Test Approach
- **Static checks:** markdownlint + codespell via CI; fix until green.
- **Peer review:** two reviewers comment and request changes; author fixes; reviewers approve.
- **Traceability:** map each requirement to at least one test/checklist item.

## 7. Entry / Exit Criteria
**Entry:**
- Branch created from latest `main`.
- Files compile/format locally (no obvious syntax errors).

**Exit:**
- CI green.
- At least **1** approval (or per branch protection).
- All review comments resolved.
- Test evidence attached/linked in the PR.

## 8. Test Environment
- GitHub repo with Actions enabled.
- Local machine with Git; optional Node.js for demo API.
- Editors: VS Code/Notepad.

## 9. Test Data
- N/A for docs. If API available, sample data described in collection/environment files.

## 10. Risks & Mitigations
- **Risk:** CI flaky. **Mitigation:** re-run job; keep workflow minimal.
- **Risk:** Reviewers unavailable. **Mitigation:** add backup reviewer; extend deadline.

## 11. Defect Management
- Create GitHub Issues using the **Bug report** template.
- Severity: **S1 Critical**, **S2 Major**, **S3 Minor**, **S4 Cosmetic**.
- Link issues to PRs; close via commit/PR message: `Closes #<issue_number>`.

## 12. Test Schedule (example)
- Day 1: Draft docs + open PR.
- Day 2: Reviews + fixes.
- Day 3: Final approval + merge + tag `v0.1`.

## 13. Deliverables
- This test plan (`TEST_PLAN_LAB3.md`).
- Review checklist (`REVIEW_CHECKLIST.md`) filled in PR.
- PR link with comments, approvals, CI logs.
- (Optional) Release notes.

## 14. Requirements → Checks (Traceability)
| ID | Requirement | Check |
|---|---|---|
| R-01 | Docs render cleanly | markdownlint passes |
| R-02 | Spelling correct | codespell passes |
| R-03 | Setup steps are executable | reviewer executes steps |
| R-04 | Collaboration practiced | PR review + approval recorded |
| R-05 | Issues are tracked | linked Issues closed by PR |

## 15. Sample Test Cases
1. **TC-01:** Lint passes on `user_guide.md` → Expect CI green.
2. **TC-02:** Misspelt word triggers codespell → Expect CI red; fix → green.
3. **TC-03:** Reviewer suggests change → Author commits fix → Reviewer approves.
4. **TC-04:** PR merged with “Squash and merge” → `main` updated.

## 16. Sign‑off
- Author: __________________ Date: __________
- Reviewer A: ______________ Date: __________
- Reviewer B: ______________ Date: __________
- Maintainer: ______________ Date: __________
