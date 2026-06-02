# design-skills

Reusable Codex skills for turning business and technical source materials into build-ready backend and API design outputs.

## Included Skills

- `design-from-materials`: turn mixed project materials into a normalized pre-development design package
- `api-contract-designer`: turn requirements and examples into explicit API contracts
- `domain-solution-designer`: shape domain models and backend solution drafts before coding

## Repository Structure

- `design-from-materials/`
- `api-contract-designer/`
- `domain-solution-designer/`
- `references/`: shared output templates and source-reading heuristics

## Install Locally

Copy or symlink the skill folders into your Codex skills directory, or keep the repository intact and reference the skill folders from here.

Typical local skills directory on this machine:

`C:\Users\Zhou\.codex\skills\`

## Validate

The repository is designed to be checked with the `skill-creator` validator:

`C:\Users\Zhou\.codex\skills\.system\skill-creator\scripts\quick_validate.py`

## Push to GitHub

`gh` is not installed in this environment, so the repository can be prepared and committed locally here, then pushed manually:

```bash
git remote add origin <github-repo-url>
git push -u origin main
```
