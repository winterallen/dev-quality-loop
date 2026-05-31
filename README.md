# Dev Quality Loop

Dev Quality Loop is a Codex skill for disciplined software development work. It guides Codex through a practical loop for implementing, debugging, refactoring, reviewing, and shipping code changes with scoped context gathering, low-risk edits, proportional validation, and concise handoffs.

## What It Helps With

- Frame a coding request before editing.
- Inspect repository state and relevant conventions.
- Choose the smallest credible implementation path.
- Preserve user work while making targeted changes.
- Select useful tests, diagnostics, builds, or manual checks.
- Review diffs for accidental churn and missing coverage.
- Summarize results clearly after the work is done.

## Skill Structure

```text
dev-quality-loop/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── review-checklist.md
```

- `SKILL.md` contains the main workflow and trigger description.
- `agents/openai.yaml` provides UI metadata for Codex skill listings.
- `references/review-checklist.md` is loaded when a change needs a deeper final review.

## Installation

Clone this repository and copy the skill folder into your Codex skills directory:

```bash
git clone git@github.com:winterallen/dev-quality-loop.git
mkdir -p ~/.codex/skills
cp -r dev-quality-loop/dev-quality-loop ~/.codex/skills/
```

If `CODEX_HOME` is set, install it under `$CODEX_HOME/skills` instead:

```bash
mkdir -p "$CODEX_HOME/skills"
cp -r dev-quality-loop/dev-quality-loop "$CODEX_HOME/skills/"
```

## Example Prompts

```text
Use dev-quality-loop to fix this failing test and validate the change.
```

```text
Use dev-quality-loop to refactor this module without changing public behavior.
```

```text
Use dev-quality-loop to review the diff before I open a PR.
```

## Validation

Validate the skill folder with the Codex skill creator validator:

```bash
python ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py dev-quality-loop
```

On this repository, the skill currently validates successfully.
