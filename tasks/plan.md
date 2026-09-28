# Implementation Plan: Vibe Code OS dashboard

## Overview
A vibe-coding dashboard that works on any device (phone, tablet, desktop) as a responsive web app / PWA. Graphify is set up first so every agent session works from a knowledge graph of the codebase instead of re-reading raw files.

## Architecture decisions (proposed, confirm before Phase 1)
- Next.js + React + TypeScript, deployed on Vercel.
- Supabase for auth, database and realtime.
- Mobile-first responsive layout, installable as a PWA.
- Graphify ([Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify), PyPI `graphifyy`) as the codebase knowledge graph from day one.

## Phase 0: Graphify foundation
- [ ] Task 0.1: Install Graphify
  - Run: `uv tool install graphifyy` (or `pipx install graphifyy`)
  - Acceptance: `graphify --version` prints a version.
- [ ] Task 0.2: Register Graphify with Claude Code for this repo
  - Run in the repo root: `graphify install --project --platform claude`
  - Writes project-scoped files (`.claude/skills/`, `CLAUDE.md` section, a `PreToolUse` hook). Review the diff before committing.
  - Acceptance: `/graphify` is available in a Claude Code session in this repo.
- [ ] Task 0.3: Build the first graph and commit the shared outputs
  - Run: `/graphify` (or `graphify` CLI) at the repo root.
  - Commit only `graphify-out/graph.json` and `graphify-out/GRAPH_REPORT.md` (`.gitignore` already keeps cache and machine-local files out).
- [ ] Task 0.4: Keep the graph fresh
  - Rebuild the graph as part of each task's verification step (Phase 1 onward), and before opening a PR.

### Checkpoint: Foundation
- [ ] A new session can answer "where is X?" with `graphify query` before reading files.

## Phase 1: App skeleton (after spec approval)
- [ ] Task 1.1: Scaffold Next.js app, lint, typecheck, test runner.
- [ ] Task 1.2: Responsive shell (nav, layout) verified at 375px, 768px, 1280px.
- [ ] Task 1.3: Supabase auth (sign in / out) end to end.
- [ ] Task 1.4: PWA manifest and install prompt.

### Checkpoint: Skeleton
- [ ] Builds clean, signs in on phone and desktop, graph rebuilt.

## Open questions
- What does the dashboard show first (projects, sessions, PRs, deploys)?
- Single user (you) or shared with others?
