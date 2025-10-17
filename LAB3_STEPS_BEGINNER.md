# Lab 3 — Collaboration (Beginner-Friendly, Click-by-Click)

Follow these exact steps. Even if you know them, do them anyway to avoid mistakes.

## A) Start from a clean main
1. Open **Terminal / Git Bash**.
2. Go to your repository folder (replace the path with your real one):
   ```bash
   cd C:/Users/98120/Downloads/stqm_labs
   ```
3. Get the latest main:
   ```bash
   git switch main
   git pull --ff-only
   ```

## B) Create a Lab 3 branch
```bash
git switch -c docs/lab3
```

## C) Add Lab 3 files
1. Download **lab3_pack.zip** (from this chat) to your computer.
2. Extract it. Inside you will see:
   - `TEST_PLAN_LAB3.md`
   - `LAB3_STEPS_BEGINNER.md`
   - `REVIEW_CHECKLIST.md`
   - `.github/PULL_REQUEST_TEMPLATE.md`
   - `.github/CODEOWNERS`
   - `.github/ISSUE_TEMPLATE/bug_report.md`
   - `.github/ISSUE_TEMPLATE/feature_request.md`
3. Copy **all** of these into your repository folder (keep the same paths).

## D) Stage and commit
```bash
git add TEST_PLAN_LAB3.md LAB3_STEPS_BEGINNER.md REVIEW_CHECKLIST.md .github
git commit -m "Lab3: add collaboration test plan, checklist, and GitHub templates"
```

## E) Push the branch
```bash
git push -u origin docs/lab3
```

## F) Open a Pull Request
1. In your browser, open your repo on GitHub.
2. You should see a yellow banner **“Compare & pull request”** → click it.
   - If you do not see the banner: click **Pull requests** → **New pull request** → set **base: main** and **compare: docs/lab3**.
3. The PR form will automatically load the **PULL_REQUEST_TEMPLATE.md** with checkboxes.
4. **Add reviewers** (they must accept collaborator invites first).
5. Click **Create pull request**.

## G) Create Issues for work items
1. Click **Issues** → **New issue** → choose **Bug report** or **Feature request**.
2. Example:
   - Title: *Fix inconsistent heading levels in user_guide.md*
   - Body: leave template text; add details.
3. Click **Submit new issue**.
4. Link this issue to your PR by typing in the PR description or a commit message:
   - `Closes #<issue_number>` (example: `Closes #2`).

## H) Review & collaborate
1. Reviewers open the PR → **Files changed** tab → leave comments or **Add suggestion**.
2. As author, respond and commit fixes:
   ```bash
   git switch docs/lab3
   # edit files per comments
   git add <changed-files>
   git commit -m "Address review: <short description>"
   git push
   ```
3. Back on GitHub, mark each conversation **Resolved** after fixing.

## I) Approvals and CI
- Ensure the Docs Quality workflow is green.
- Ask reviewers to click **Approve** on the PR.

## J) Merge and clean up
1. On the PR, click **Squash and merge** → Confirm.
2. Click **Delete branch**.
3. Update local main:
   ```bash
   git switch main
   git pull --ff-only
   git fetch --prune
   git branch -d docs/lab3
   ```

## K) Evidence for submission
- Link to the PR showing:
  - Reviewer comments + approvals
  - Linked issues closed (via “Closes #x”)
  - Green CI checks
- Attach `TEST_PLAN_LAB3.md` and a screenshot of the PR’s **Conversation** and **Checks** tabs.

## Optional: Protect main (require review + passing checks)
1. GitHub → **Settings → Branches → Add branch protection rule**.
2. Branch name pattern: `main`.
3. Enable:
   - **Require a pull request before merging**
   - **Require approvals**: 1 (or 2)
   - **Require status checks to pass before merging** → tick your workflow.
4. Save.
