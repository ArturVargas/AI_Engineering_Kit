# AI Engineering Kit v1.1 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add the minimum persistent standards and templates needed to apply Superpowers practices to AI Engineering Kit projects.

**Architecture:** The kit owns durable project context, plans, and evidence. Superpowers owns agent behavior during design, implementation, debugging, review, and verification. Documentation files connect the two without scripts, dependencies, or duplicated skills.

**Tech Stack:** Markdown, YAML, Git.

**Spec:** `docs/superpowers/specs/2026-08-18-superpowers-integration-design.md`

## Global Constraints

- Do not copy Superpowers skills into this repository.
- Do not add dependencies, scripts, CI, or automation.
- Keep the process proportional: small changes must not require architectural artifacts.
- Require evidence before release-ready claims.

---

### Task 1: Add execution and release standards

**Files:**
- Create: `standards/execution.md`
- Create: `standards/release-readiness.md`

**Interfaces:**
- Consumes: the initiative types declared by `template/.ai/workflow.yaml`.
- Produces: selection rules for project runs and a release evidence checklist.

- [x] **Step 1: Draft `standards/execution.md`**

Define `spike`, `bounded`, and `architectural`; state required artifacts and escalation rules. Scope TDD and independent review by risk.

- [x] **Step 2: Draft `standards/release-readiness.md`**

List evidence required for acceptance criteria, automated checks, migrations, rollback, secrets/permissions, and observability where applicable.

- [x] **Step 3: Verify the standards**

Run: `rg -n 'spike|bounded|architectural|rollback|observability' standards/execution.md standards/release-readiness.md`

Expected: Every required classification and release safeguard is present.

### Task 2: Add persistent implementation and incident templates

**Files:**
- Create: `templates/specification.md`
- Create: `templates/implementation-plan.md`
- Create: `templates/incident-root-cause.md`

**Interfaces:**
- Consumes: project references, ADRs, architecture and evidence.
- Produces: approved requirements, executable task plans, or a root-cause record.

- [x] **Step 1: Create the specification template**

Include problem, scope, exclusions, user flow, acceptance criteria, edge/error behavior, non-functional requirements, observability, and open decisions.

- [x] **Step 2: Create the implementation-plan template**

Require exact files, interfaces, test/verification command, migration or rollback impact, and task-level completion evidence.

- [x] **Step 3: Create the incident root-cause template**

Require reproduction, evidence, recent changes, a single hypothesis, root cause, corrective action, regression proof, and an architecture escalation after three failed hypotheses.

- [x] **Step 4: Verify template coverage**

Run: `rg -n 'Criterios de aceptación|Interfaces|Rollback|Causa raíz|Hipótesis' templates/specification.md templates/implementation-plan.md templates/incident-root-cause.md`

Expected: All requested planning and diagnostic fields are present.

### Task 3: Upgrade workflow, verification, and README

**Files:**
- Modify: `template/.ai/workflow.yaml`
- Modify: `templates/verification.md`
- Modify: `README.md`

**Interfaces:**
- Consumes: the new standards and templates.
- Produces: a discoverable workflow and an evidence-based verification handoff.

- [x] **Step 1: Insert `implementation-plan` into the workflow**

Place it immediately after `architecture` and before `implementation`. Document the three initiative types and their entry points.

- [x] **Step 2: Expand verification evidence**

Add fields for fresh command output, build/lint/type-check, release/migration/rollback, security, observability, and a clear decision status.

- [x] **Step 3: Update README**

Explain the kit/Superpowers division of responsibility, the new execution flow, and risk-proportional use. Link the new standards and templates by name.

- [x] **Step 4: Verify release documentation**

Run: `rg -n 'implementation-plan|Superpowers|evidencia|rollback' README.md template/.ai/workflow.yaml templates/verification.md`

Expected: Workflow placement, ownership boundary, and evidence requirements are discoverable.

### Task 4: Validate the v1.1 artifact set

**Files:**
- Modify: `docs/superpowers/plans/2026-08-18-superpowers-integration.md`

**Interfaces:**
- Consumes: all v1.1 files.
- Produces: verification evidence for the implementation.

- [x] **Step 1: Check expected files exist**

Run: `test -f standards/execution.md && test -f standards/release-readiness.md && test -f templates/specification.md && test -f templates/implementation-plan.md && test -f templates/incident-root-cause.md`

Expected: exit code 0.

- [x] **Step 2: Check documentation formatting**

Run: `git diff --check`

Expected: exit code 0 with no whitespace errors.

- [x] **Step 3: Review against the spec**

Confirm every acceptance criterion in `docs/superpowers/specs/2026-08-18-superpowers-integration-design.md` maps to an implemented file or README section, then mark the task checkboxes complete.
