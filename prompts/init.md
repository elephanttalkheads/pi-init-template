---
description: 生成或更新 AGENTS.md（opencode /init 移植）
argument-hint: "[focus 说明]"
---

Create or update `AGENTS.md` for this repository, following the behavior of opencode's `/init`.

First, locate the repository root with `git rev-parse --show-toplevel` (or `pwd` if not a git repository). The target file is `AGENTS.md` at that root — do not write it anywhere else.

The goal is a compact instruction file that helps future sessions avoid mistakes and ramp up quickly. Every line should answer: "Would an agent likely miss this without help?" If not, leave it out.

User-provided focus or constraints (honor these):
$ARGUMENTS

## How to investigate

Read the highest-value sources first:
- `README*`, root manifests, workspace config, lockfiles
- build, test, lint, formatter, typecheck, and codegen config
- CI workflows and pre-commit / task runner config
- existing instruction files (`AGENTS.md`, `CLAUDE.md`, `.cursor/rules/`, `.cursorrules`, `.github/copilot-instructions.md`)
- project-local agent config such as `.pi/`, `opencode.json`, `.codex/`

Note: pi automatically loads `AGENTS.md` / `CLAUDE.md` from every ancestor directory up to the filesystem root, plus the global `~/.pi/agent/` dir. If this repo relies on nested or module-level instruction files, keep that hierarchy in mind and mention it in the output.

If architecture is still unclear after reading config and docs, inspect a small number of representative code files to find the real entrypoints, package boundaries, and execution flow. Prefer reading the files that explain how the system is wired together over random leaf files.

Prefer executable sources of truth over prose. If docs conflict with config or scripts, trust the executable source and only keep what you can verify.

## What to extract

Look for the highest-signal facts for an agent working in this repo:
- exact developer commands, especially non-obvious ones
- how to run a single test, a single package, or a focused verification step
- required command order when it matters, such as `lint -> typecheck -> test`
- monorepo or multi-package boundaries, ownership of major directories, and the real app/library entrypoints
- framework or toolchain quirks: generated code, migrations, codegen, build artifacts, special env loading, dev servers, infra deploy flow
- repo-specific style or workflow conventions that differ from defaults
- testing quirks: fixtures, integration test prerequisites, snapshot workflows, required services, flaky or expensive suites
- important constraints from existing instruction files worth preserving

Good `AGENTS.md` content is usually hard-earned context that took reading multiple files to infer.

## Questions

This environment has no interactive question tool. If the repository cannot answer something important, do NOT block on it: proceed with the best reasonable assumption and list the open questions at the end of your result, so the user can answer them in a follow-up message.

## Writing rules

Include only high-signal, repo-specific guidance such as:
- exact commands and shortcuts the agent would otherwise guess wrong
- architecture notes that are not obvious from filenames
- conventions that differ from language or framework defaults
- setup requirements, environment quirks, and operational gotchas
- references to existing instruction sources that matter

Exclude:
- generic software advice
- long tutorials or exhaustive file trees
- obvious language conventions
- speculative claims or anything you could not verify
- content better stored in another file referenced via agent config

When in doubt, omit.

Prefer short sections and bullets. If the repo is simple, keep the file simple. If the repo is large, summarize the few structural facts that actually change how an agent should work.

If `AGENTS.md` already exists at the repository root, improve it in place rather than rewriting blindly. Preserve verified useful guidance, delete fluff or stale claims, and reconcile it with the current codebase. If the user explicitly asked to rewrite it from scratch (e.g. "完全重写" / "rewrite"), do so instead.
