# Design Skills Repository Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a Git-tracked repository that contains three reusable Codex skills for turning mixed project materials into backend and API design outputs before coding.

**Architecture:** Create a standalone `design-skills` repository with three independent skill folders and one shared `references/` area at the repo root. Use the system `skill-creator` scripts to scaffold each skill, then replace the templates with focused instructions that complement existing brainstorming and planning skills rather than duplicating them.

**Tech Stack:** Markdown, Codex skill format, Python helper scripts from `skill-creator`, Git

---

### Task 1: Initialize Repository Structure

**Files:**
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\.gitignore`
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\README.md`
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\references\output-templates.md`
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\references\source-material-patterns.md`

- [ ] **Step 1: Create the repo root folders**

Run:

```powershell
New-Item -ItemType Directory -Force 'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\references'
```

Expected: The `references` folder exists under `design-skills`.

- [ ] **Step 2: Add a minimal `.gitignore`**

Write:

```gitignore
.venv/
__pycache__/
*.pyc
```

- [ ] **Step 3: Add a short repository `README.md`**

Write:

```markdown
# design-skills

Reusable Codex skills for turning business and technical source materials into build-ready backend and API design outputs.
```

- [ ] **Step 4: Add shared reference docs**

Write `references/output-templates.md` and `references/source-material-patterns.md` with concise templates and heuristics used by all three skills.

- [ ] **Step 5: Commit**

Run:

```bash
git add .gitignore README.md references
git commit -m "chore: initialize design-skills repository structure"
```

Expected: A commit with the initial structure is created.

### Task 2: Scaffold the Three Skill Folders

**Files:**
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\design-from-materials\SKILL.md`
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\design-from-materials\agents\openai.yaml`
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\api-contract-designer\SKILL.md`
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\api-contract-designer\agents\openai.yaml`
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\domain-solution-designer\SKILL.md`
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\domain-solution-designer\agents\openai.yaml`

- [ ] **Step 1: Run `init_skill.py` for `design-from-materials`**

Run:

```powershell
& 'C:\Users\Zhou\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe' `
  'C:\Users\Zhou\.codex\skills\.system\skill-creator\scripts\init_skill.py' `
  design-from-materials `
  --path 'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills' `
  --resources references `
  --interface display_name='Design From Materials' `
  --interface short_description='Turn source docs into a pre-dev design package.' `
  --interface default_prompt='Use $design-from-materials to turn these materials into a build-ready backend design draft.'
```

Expected: The skill directory and `agents/openai.yaml` are created.

- [ ] **Step 2: Run `init_skill.py` for `api-contract-designer`**

Run:

```powershell
& 'C:\Users\Zhou\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe' `
  'C:\Users\Zhou\.codex\skills\.system\skill-creator\scripts\init_skill.py' `
  api-contract-designer `
  --path 'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills' `
  --resources references `
  --interface display_name='API Contract Designer' `
  --interface short_description='Design endpoint contracts from requirements and examples.' `
  --interface default_prompt='Use $api-contract-designer to draft endpoint contracts from these requirements and examples.'
```

Expected: The skill directory and `agents/openai.yaml` are created.

- [ ] **Step 3: Run `init_skill.py` for `domain-solution-designer`**

Run:

```powershell
& 'C:\Users\Zhou\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe' `
  'C:\Users\Zhou\.codex\skills\.system\skill-creator\scripts\init_skill.py' `
  domain-solution-designer `
  --path 'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills' `
  --resources references `
  --interface display_name='Domain Solution Designer' `
  --interface short_description='Draft domain models and backend solution shapes.' `
  --interface default_prompt='Use $domain-solution-designer to shape the domain model and technical solution for this feature.'
```

Expected: The skill directory and `agents/openai.yaml` are created.

- [ ] **Step 4: Commit**

Run:

```bash
git add design-from-materials api-contract-designer domain-solution-designer
git commit -m "chore: scaffold reusable design skills"
```

Expected: A commit with the generated skill skeletons is created.

### Task 3: Replace Templates with Final Skill Content

**Files:**
- Modify: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\design-from-materials\SKILL.md`
- Modify: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\api-contract-designer\SKILL.md`
- Modify: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\domain-solution-designer\SKILL.md`
- Modify: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\*\agents\openai.yaml`

- [ ] **Step 1: Rewrite `design-from-materials/ SKILL.md`**

Write a concise workflow that:
- inventories source materials,
- extracts facts versus inferences,
- produces a fixed backend design package,
- defers implementation planning to existing skills.

- [ ] **Step 2: Rewrite `api-contract-designer/SKILL.md`**

Write a focused workflow for endpoint boundaries, request and response schemas, validation, shared error models, and unresolved contract questions.

- [ ] **Step 3: Rewrite `domain-solution-designer/SKILL.md`**

Write a focused workflow for entities, state transitions, storage design, runtime responsibilities, and failure/concurrency tradeoffs.

- [ ] **Step 4: Check `agents/openai.yaml` values**

Ensure each `display_name`, `short_description`, and `default_prompt` still match the final `SKILL.md` contents.

- [ ] **Step 5: Commit**

Run:

```bash
git add design-from-materials api-contract-designer domain-solution-designer
git commit -m "feat: author reusable pre-development design skills"
```

Expected: A commit with the finished skill content is created.

### Task 4: Validate and Package the Repository

**Files:**
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\work\validator-requirements.txt`

- [ ] **Step 1: Create an isolated virtual environment for validation**

Run:

```powershell
& 'C:\Users\Zhou\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe' -m venv 'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\.venv'
```

Expected: The `.venv` directory exists.

- [ ] **Step 2: Install `PyYAML` into that venv**

Run:

```powershell
& 'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\.venv\Scripts\python.exe' -m pip install pyyaml
```

Expected: `PyYAML` installs successfully.

- [ ] **Step 3: Run `quick_validate.py` on each skill**

Run:

```powershell
& 'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\.venv\Scripts\python.exe' `
  'C:\Users\Zhou\.codex\skills\.system\skill-creator\scripts\quick_validate.py' `
  'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\design-from-materials'
& 'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\.venv\Scripts\python.exe' `
  'C:\Users\Zhou\.codex\skills\.system\skill-creator\scripts\quick_validate.py' `
  'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\api-contract-designer'
& 'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\.venv\Scripts\python.exe' `
  'C:\Users\Zhou\.codex\skills\.system\skill-creator\scripts\quick_validate.py' `
  'C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\domain-solution-designer'
```

Expected: All three validations pass.

- [ ] **Step 4: Commit**

Run:

```bash
git add .
git commit -m "test: validate skill package structure"
```

Expected: A commit with validation-related updates is created.

### Task 5: Initialize Git History and Prepare GitHub Push

**Files:**
- Create: `C:\Users\Zhou\Documents\Codex\2026-06-02\files-mentioned-by-the-user-xlsx\design-skills\.git`

- [ ] **Step 1: Initialize git if needed**

Run:

```bash
git init
git branch -M main
```

Expected: The repo is initialized on `main`.

- [ ] **Step 2: Make the initial commits if git was not initialized earlier**

Run:

```bash
git add .
git commit -m "feat: add reusable design skills repository"
```

Expected: The repository has at least one local commit.

- [ ] **Step 3: Capture push instructions**

Document that `gh` is not installed in this environment, so the repository can only be prepared locally here. The eventual push path is:

```bash
git remote add origin <github-repo-url>
git push -u origin main
```

- [ ] **Step 4: Offer execution handoff**

State that the repository is ready for either:
1. local installation into `C:\Users\Zhou\.codex\skills\`, or
2. manual push after the user creates a GitHub repository URL.
