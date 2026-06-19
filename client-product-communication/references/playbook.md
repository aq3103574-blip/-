# Product Communication Playbook

## Intake Questions

Ask only after inspecting discoverable context.

- Product goal: what problem is this product solving, and for whom?
- Platform: web, mobile, mini program, backend, document, automation, or mixed.
- Success criteria: what must be true for the user to approve it?
- Scope boundaries: what is explicitly out of scope for v1?
- Data ownership: local-only, account-based, cloud-synced, or tenant-scoped.
- Confirmation format: UI image, written spec, Feishu/Lark doc, GitHub artifact, PR, or all.

## Decision Log Template

Use concise bullets and keep corrections visible.

```markdown
## Confirmed Decisions

- Product name:
- Target platform:
- UI direction:
- Auth/data owner:
- Cloud/backend:
- Document destination:
- Repository destination:
- Corrections:
```

## Product Spec Template

```markdown
# <Product Name> Product Confirmation

## Summary
- Product:
- Audience:
- Platform:
- Core value:

## Pages Or Surfaces
- <Page>: <main content and actions>

## Interactions
- Primary actions:
- Secondary actions:
- Loading states:
- Empty states:
- Error states:
- Disabled states:

## Data Design
- Collections/tables:
- Ownership key:
- Indexes:
- Prediction/calculation rules:

## Tests And Acceptance
- Build/import:
- Main flows:
- Edge cases:
- Device/runtime:

## Assumptions
- <Assumption>
```

## UI Confirmation Checklist

- Show each major screen, not a landing page unless requested.
- Show action placement exactly as confirmed by the user.
- Include control states when requested: default, pressed, selected, disabled, loading, focused, error.
- Include empty, loading, and error states for production work.
- If the user corrects a placement or label, regenerate or update the artifact and restate the corrected rule.

## Feishu/Lark CLI Pattern

1. Inspect commands:
   - `lark-cli docs +create --help`
   - `lark-cli docs +update --help`
   - `lark-cli docs +media-insert --help`
2. Check auth:
   - `lark-cli auth status`
3. Create or update with explicit identity:
   - Prefer `--as user` when the user needs to open and own the document.
   - Use `--doc-format markdown` for structured plans.
4. Insert media:
   - Use relative file paths from the media file directory when the CLI rejects absolute paths.
   - If media insert fails with missing scope, request user auth with exact scopes.
5. Verify:
   - Fetch outline or content after writing.
   - Return the canonical document URL.

Common scopes:

```text
docs:doc
docs:document.media:upload
drive:file:upload
docs:permission.member:create
docs:permission.setting:write_only
```

## GitHub Publishing Checklist

1. Inspect:
   - `git status --short --branch`
   - `git remote -v`
   - available GitHub tools or `gh auth status`
2. Prepare:
   - Exclude generated QR codes, secrets, local auth files, temp files, and unrelated user changes.
   - Add `.gitignore` entries only if they protect generated or sensitive files.
3. Validate:
   - Run the skill validator if publishing a skill.
   - Inspect staged diff before committing.
4. Commit:
   - Use a clear commit message, for example `Add client product communication skill`.
5. Push:
   - Push to the existing remote branch if present.
   - If no remote exists and no GitHub creation tool is available, stop after a local commit and report the exact commands or inputs needed.

## Skill Packaging Checklist

- Required: `SKILL.md` with only `name` and `description` in YAML frontmatter.
- Recommended: `agents/openai.yaml` with display name, short description, and default prompt.
- Optional: `references/` for longer reusable playbooks.
- Avoid README files, install guides, or extra docs that are not directly used by the agent.
- Validate with:

```bash
python3 /path/to/skill-creator/scripts/quick_validate.py <skill-folder>
```
