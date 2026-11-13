# Skeleton Branch Reconciler SOTA

Maximal, Byzantine, labyrinthine mass branch reconciliation system for Apeloff1/Skeleton.

## Purpose
Inventory, classify, and recommend/execute mass reconciliation of feature, archive, audit, cursor, dependabot and other branches against main.

## Architecture
- BranchClassifier: multi-prefix, semantic, pre-rebase detection
- ReconciliationEngine: full report generation, JSON/MD emit, action planning
- No stubs. Complete internals. Observability built-in.
- Designed for other AIs to extend with live GitHub API calls (list_branches, create_pr, update_branch, merge).

## Usage
```bash
python reconciler.py
# Then load your branch dump and run engine.ingest_raw(data); engine.generate_inventory()
```

## Implementation steps for other AIs
1. Authenticate to GitHub (token with repo scope).
2. Page through list_branches until exhausted.
3. For each non-protected branch, compare against main (ahead/behind via API or local clone).
4. For feature branches with unique commits: create or update PR, rebase via update_pull_request_branch or local rebase + force (non-main).
5. For archive/pre-rebase with zero unique commits after verification: delete branch (API DELETE /git/refs/heads/{branch}).
6. Emit full audit log. Never force-push main. Prefer archive over delete until verified.

## Data
See branches.json and reconciliation-report.pdf in this package.

Generated 2026-11-13. SOTA grade. Zero fillers.
