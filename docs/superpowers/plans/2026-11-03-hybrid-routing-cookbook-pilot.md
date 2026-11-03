# Hybrid Routing Cookbook Pilot Implementation Plan

> **For agentic workers:** Use superpowers:executing-plans to work through this plan task by task. Checkboxes track progress.

**Goal:** Validate a reusable YAML routing method through a bounded CodexRouter pilot and record whether it saves tokens without reducing accepted quality.

**Architecture:** AI Engineering Kit owns the proposed YAML policy and reusable guidance. CodexRouter supplies its existing policy, evaluation fixtures, and usage evidence; the first simulation is a manual table-driven walkthrough, not a new runtime. The measured comparison is a separate gate after preparation.

**Tech Stack:** YAML, Markdown, existing CodexRouter CLI evaluation and Python test tooling.

**Spec:** `docs/superpowers/specs/2026-11-03-hybrid-routing-cookbook-design.md` and `cookbooks/hybrid-routing-pilot.yaml` in AI Engineering Kit; `.ai/specs/2026-10-18-cli-routing-policy-design.md` in CodexRouter.

## Global Constraints

- Four complete flows: two baseline and two candidate, two turns each, eight turns maximum.
- At most one explicit escalation per flow, only before a new turn and within the eight-turn budget; zero automatic retries.
- Baseline: reference profile for both turns. Candidate: reference for architecture, economical only for eligible bounded UI implementation. Revalidate availability before inference; preserve a user-selected profile.
- No new model calls, installation, runtime, or inference until the measured-pilot gate is satisfied and the required execution authorization is in place.
- Record safe operational metadata and evidence references only: no prompts, source code, secrets, PII, chain-of-thought, or raw tool output in working state.
- Unknown provider/origin, quota failure, uncertain outcome, or possible duplicate execution stops the affected run. Never switch profiles during an active turn.
- Success requires at least 5% fewer attributable tokens for the complete accepted flow, with equivalent acceptance quality. Missing trustworthy usage or acceptance evidence is inconclusive, not zero or a pass.

## Review Focus

- Missing acceptance criteria must prevent an economical route and completion (Task 1).
- A manual profile selection takes precedence over the candidate profile (Task 1).
- A quota failure or uncertain turn outcome stops without replay (Task 1).
- A failed check with an exhausted escalation or turn budget stops, without a ninth turn (Task 1).
- Missing usage or failed acceptance must not be reported as a successful saving (Task 2).

## Files and ownership

- AI Engineering Kit: `cookbooks/hybrid-routing-pilot.yaml`, this plan, and the design define the reusable method.
- CodexRouter: inspect `.ai/evals/2026-10-18-cli-routing-comparison.md` and `.ai/specs/2026-10-18-cli-routing-policy-design.md` before reuse; keep project-specific execution evidence under `.ai/evals/` according to its existing conventions.
- Preserve existing untracked files. Obtain workspace write access to CodexRouter before creating or editing anything there. This plan itself lives on the Kit branch.

### Task 1: Rehearse the policy without inference

**Files:** Create `docs/superpowers/plans/2026-11-03-hybrid-routing-walkthrough.md` in AI Engineering Kit.

**Interfaces:** Consumes the YAML policy and CodexRouter's existing routing policy. Produces a table of input conditions, expected decision, next state, and evidence reference for Task 2.

- [ ] Read the two CodexRouter policy/evaluation documents and record their current commit and working-tree status. Resolve any difference with the Cookbook conservatively; do not silently replace the existing policy.
- [ ] Create a table with these cases and expected outcomes: eligible bounded UI → economical; architecture → reference; missing acceptance criteria → stop or reference, never economical; manual model choice → preserve choice; uncertain origin/provider → stop routing; quota error or uncertain outcome → stop without retry; failed verification with one escalation available and a remaining authorized turn → `escalate_pending`; failed verification with no escalation or turn left → stop; accepted verification with all evidence → complete.
- [ ] For each row record a sanitized example working state using the required fields in the YAML. Verify no prohibited data is stored; record evidence references instead of raw output.
- [ ] Walk each transition against the YAML and the existing CodexRouter policy. Record pass/fail and a concrete correction for each discrepancy. Do not continue to the measured pilot while any case fails.
- [ ] Verify the YAML parses and the four-flow/eight-turn limits match this plan. Record the commands and results in the walkthrough.

### Task 2: Prepare and evaluate the comparison

**Files:** Existing CodexRouter `.ai/evals/2026-10-18-cli-routing-comparison.md`; create a dated result in CodexRouter `.ai/evals/` only after workspace access is granted.

**Interfaces:** Consumes Task 1's passing walkthrough, existing comparison fixtures, per-turn native usage and human acceptance evidence. Produces a per-flow result and decision: `pass`, `fail`, or `inconclusive`.

- [ ] Confirm the existing comparison contains the same task, acceptance criteria, two-turn flow, and per-turn usage attribution for both variants. Record any mismatch and stop rather than change the benchmark after results are known.
- [ ] Prepare four rows: baseline 1, baseline 2, candidate 1, candidate 2. Each row records requested and accepted profile, two turn identifiers, total attributable tokens, acceptance outcome, evidence references, escalation count, and stop reason. Do not include raw content.
- [ ] Before inference, verify the account's available profiles, source/provider, existing evaluation commands and usage capture. If any prerequisite or permission is missing, mark the pilot `not run` and report the blocker. Approval of this plan alone does not override the existing CodexRouter spec's separate inference authorization requirement.
- [ ] Once inference is explicitly authorized, execute no more than the four flows/eight turns using the existing protocol. Count any escalation within those limits and stop on uncertain outcome; never replay an uncertain turn.
- [ ] Calculate the mean total tokens per complete accepted baseline flow and per complete accepted candidate flow; savings = `(baseline_mean - candidate_mean) / baseline_mean * 100`. Include all attributable turn and escalation usage. If any planned flow lacks complete usage or acceptance evidence, report `inconclusive` and do not assert savings. If all four flows are complete and accepted, report `pass` only at savings ≥ 5% with equivalent acceptance; otherwise report `fail`.
- [ ] Report each flow and the aggregate, including failures, abstentions, and manual work. Two repetitions per variant provide an initial signal, not statistical proof. Do not expand the budget or tune eligibility retrospectively.

### Task 3: Decide reuse from evidence

**Files:** Append the decision to the Task 2 result; update the Kit Cookbook or README only if the observed evidence calls for a specific correction.

**Interfaces:** Consumes Task 2's recorded outcome. Produces the adoption decision and any explicitly scoped follow-up.

- [ ] If `pass`, document what can be reused manually and propose a project-local adapter only if it removes observed repeated work. A reusable library requires evidence of the same need in at least one additional project.
- [ ] If `fail` or `inconclusive`, document the limiting evidence and stop; do not claim a saving or promote a runtime.
- [ ] Check `git diff --check` in each changed repository and review the complete file list. Report the branch, uncommitted changes, verification results, and any separate authorization needed for the next gate.
