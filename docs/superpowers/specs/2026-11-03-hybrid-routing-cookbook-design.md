# Hybrid Routing Cookbook — Design

**Status:** proposed

**Source of truth:** [`cookbooks/hybrid-routing-pilot.yaml`](../../../cookbooks/hybrid-routing-pilot.yaml)

## Purpose

This addition turns the useful part of Hybrid Reasoning Agents into an
implementable engineering practice: structured operational state, evidence
gates, and explicit escalation. It does **not** claim to reproduce latent
reasoning, hidden-state transfer, or the paper's training method; hosted models
do not expose the required internals.

The Cookbook makes a model-routing experiment reusable without turning the Kit
into an agent runtime. A project can adopt its YAML policy manually first, then
add a deliberately small local adapter only if repetition proves it worthwhile.

## Decisions made

| Topic | Decision |
| --- | --- |
| Canonical format | YAML. The Cookbook is human-reviewable and tool-readable. |
| Home | A dedicated branch of AI Engineering Kit, then reusable by projects. |
| First pilot | CodexRouter. |
| Budget | Two baseline and two candidate flows, two turns each; eight turns total, at most one escalation per flow, no automatic retries. |
| State | Compact, per-run operational state with evidence references only. |
| Runtime | Optional local adapter after cookbook-only adoption; no central service. |
| Validation | Review YAML manually in the first pilot; add schema validation only if multiple projects need it. |

## Boundaries

Use this Cookbook when routing could materially affect cost and a task has
clear acceptance criteria. It is appropriate for a bounded model-routing pilot,
not for ordinary edits or a vague request where classification itself is the
main uncertainty.

Do not use it to persist raw prompts, model reasoning, secrets, source code, or
unbounded transcripts. Do not introduce automatic retries: inconclusive
evidence must stop the run or use its single explicit escalation when a new
phase is authorized and within the existing turn budget. Quota errors, uncertain
turn outcomes, and possible duplicate execution always stop the run. Respect
the user's manual profile choice and CodexRouter's existing origin and provider
checks. Never switch profiles inside an active turn.

## Pilot interpretation

For CodexRouter, the stronger profile handles architectural work and any
escalation. The economical profile is eligible only for the localized UI phase
already bounded by acceptance tests. Evaluation compares complete accepted
flows against the same criteria; lower token use alone is not success.

## Implementation decision gate

Start with a manual, deterministic walkthrough of the YAML policy, without
model calls. The measured pilot can then use the existing evaluation machinery
if it satisfies the protocol; the walkthrough does not require a new runtime.
An optional project adapter may be considered after the pilot demonstrates
savings without accepted quality loss. Extraction of a reusable local library
is justified only after at least one additional project repeats the same
transitions and evidence requirements.
