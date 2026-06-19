---
name: client-product-communication
description: Guide product-client communication from rough request to confirmed deliverables. Use when Codex needs to clarify product requirements, design UI confirmation artifacts, capture database/API plans, write the plan into Feishu/Lark or similar docs, and prepare or publish the resulting skill/artifacts to GitHub.
---

# Client Product Communication

## Overview

Use this skill to run a practical product communication loop: ground the request, ask only decisions that affect the outcome, produce confirmable artifacts, preserve decisions in a document, and package reusable process knowledge when asked.

For detailed checklists and reusable templates, read `references/playbook.md`.

## Workflow

1. **Ground the request**
   - Inspect the workspace, existing docs, config, repository state, and available CLIs before asking questions.
   - Identify whether the user wants planning, design confirmation, implementation, documentation, publishing, or all of these.
   - Keep a decision log as requirements evolve.

2. **Clarify only consequential choices**
   - Ask about choices that materially change the spec: target platform, data ownership, auth, cloud setup, UI tone, document destination, repository destination.
   - Prefer concrete defaults and record them as assumptions when the user accepts or does not object.

3. **Produce confirmation artifacts**
   - For product work, output a concise plan with pages, data, interactions, states, error/empty/loading behavior, tests, and assumptions.
   - For UI work, include both screen-level mockups and control interaction states when the user asks for confirmation.
   - Correct artifacts immediately when the user points out a mismatch; state the corrected rule explicitly.

4. **Write decisions to the system of record**
   - If the user asks to write to Feishu/Lark, inspect the local CLI help and auth state first.
   - Create or update the target document using the current authenticated identity.
   - Insert images/media only after confirming the CLI has upload permissions; otherwise request authorization or report the exact missing scope.

5. **Package reusable process as a skill**
   - Name skills with lowercase hyphen-case.
   - Keep `SKILL.md` short and action-oriented.
   - Put longer checklists, templates, or examples in `references/`.
   - Validate the skill before committing.

6. **Publish cleanly**
   - Check Git status and avoid staging unrelated user files.
   - Commit only the skill files unless the user asks otherwise.
   - Push only when a GitHub remote or authenticated GitHub tool is available; if not, leave a ready-to-push commit and report the blocker.

## Quality Bar

- Requirements must preserve user corrections exactly.
- Confirmation docs must include links or embedded assets when available.
- GitHub publishing must not include local secrets, auth QR codes, generated scratch files, or unrelated workspace changes.
- Final responses should include the document URL, commit hash, branch, remote/PR URL, and any blocked upload steps.
