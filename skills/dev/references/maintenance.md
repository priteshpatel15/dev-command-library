# Installation and maintenance

## Purpose

- Maintain the global library's installation, updates, validation, and recovery.
- Keep reusable instructions in the source package and product artifacts in their projects/stores.
- Preserve unrelated work; use existing authorization and the environment's filesystem approval mechanism when required.

## Dependencies and discovery

- Resolve dependencies for the selected operation through [command routing](../SKILL.md#command-routing).
- Read actual installed skills from the current catalog; never substitute remembered instructions or hardcode versioned plugin-cache paths.
- Distinguish a file existing, the global link resolving, and a fresh Codex session discovering the skill.
- Use `$dev setup` for project integration and project-specific testing prerequisites; preserve native OpenSpec stores, schemas, and generated files.
- Report missing required dependencies accurately; diagnostic status remains available without installing them.
- Check current provider documentation when tooling changes affect supported discovery locations.

## First installation

Current locations:

```text
source repository: /Users/po/codeandconfigs/dev-command-library
skill package:     /Users/po/codeandconfigs/dev-command-library/skills/dev
global link:       /Users/po/.agents/skills/dev
```

- Validate the candidate using the applicable checks below before exposing it through the global link.
- Inspect the destination, including dangling links; preserve unexpected files, directories, or links.
- A matching, usable link already satisfies filesystem installation. Do not force-replace it or create a second same-name installation.
- Use this guarded example only for the locations above. It fails on missing source or an unexpected destination:

```sh
(
  dev_source=/Users/po/codeandconfigs/dev-command-library/skills/dev
  dev_link="$HOME/.agents/skills/dev"
  if ! test -f "$dev_source/SKILL.md"; then
    printf '%s\n' 'Missing skill source.' >&2
    exit 1
  fi
  if test -L "$dev_link" && test "$(readlink "$dev_link")" = "$dev_source"; then
    test -f "$dev_link/SKILL.md"
  elif test -e "$dev_link" || test -L "$dev_link"; then
    printf '%s\n' 'Unexpected installation; inspect before changing it.' >&2
    exit 1
  else
    mkdir -p "$(dirname "$dev_link")" && ln -s "$dev_source" "$dev_link"
  fi
)
```

- Verify the resulting link target and readable `SKILL.md`; a failed command is not installation proof.
- In a fresh Codex session in an unrelated temporary project, confirm catalog discovery and run `$dev status`; verify it reads the linked package and selects that project.
- Exercise `$dev setup` in the isolated project and inspect its actual files/results before claiming cross-project setup works.

## Validation

- Inspect the changed instructions and their callers, references, templates, and affected operations.
- Classify by behavioral effect: changed routing, permissions, gates, or stop conditions are behavior changes even when only Markdown changed.
- Always validate skill format with the installed `skill-creator` validator, local links/anchors, template references, and command consistency.
- Apply every relevant row below; the strictest applicable requirement remains binding.

| Change | Additional validation |
| --- | --- |
| Editorial clarification with unchanged behavior | Semantic review against the existing command contracts. |
| Command behavior or completion rules | Relevant isolated scenarios from the repository's `tests/scenarios.md` and independent review. |
| Installation/discovery | Fresh-session discovery and an affected-command smoke test; first installation includes status/setup as above. |
| Shell examples or maintenance procedures | Exercise changed commands in disposable fixtures, including affected refusal/recovery cases. |

- Evaluate actions and artifacts, not matching phrases. Fix demonstrated failures and rerun affected checks.
- Use disposable projects and isolated tool configuration for evaluations; never borrow a product's database, secrets, or live services.
- Record baseline/candidate identities, actual commands/results, evidence paths, review findings, and limitations. Small editorial checks may be recorded in the commit or handoff.
- Retain scenario/discovery reports under source `tests/evidence/`; keep raw output in ignored or temporary locations and declare its path base.
- Label failed, skipped, blocked, and unexecuted checks explicitly. Preserve failed observations when recording later corrections.
- Format/link checks do not prove workflow execution. A negative database guard proves refusal, and a UI fixture proves only that fixture's tested behavior.
- Keep credentials, customer records, and sensitive traces out of committed evidence.

## Updates

- The global link exposes source edits immediately; prepare and validate candidates outside the linked working tree.
- Inspect source HEAD and dirty files, record the baseline, and preserve unrelated changes. Coordinate updates with sessions using the library.
- Use an isolated package copy for a small editorial change or a Git worktree for broader work; keep the global link on the current installation during evaluation.
- Invoke the candidate by its explicit path. Choose unused worktree/branch names and preserve earlier candidates.

Example worktree creation, after inspecting the source:

```sh
git -C /Users/po/codeandconfigs/dev-command-library worktree add -b dev-library-update /private/tmp/dev-library-update
```

- Validate before promotion; commit only intended files and applicable evidence using explicit paths.
- Recheck the linked source's HEAD and dirty state against the recorded baseline immediately before installation. Reconcile changed/divergent state before proceeding; never force-reset or clean it.
- For an editorial package copy, copy only reviewed files after the baseline check, inspect the installed diff, and commit only those files.
- For a committed worktree candidate, review the complete diff and promote with a fast-forward only:

```sh
git -C /Users/po/codeandconfigs/dev-command-library merge --ff-only dev-library-update
```

- Record previous/new commits, verify the global link, and compare installed files with the validated candidate.
- Rerun checks only when promotion changes relevant inputs or reveals a problem; use the validation table for required discovery/behavior tests.
- Existing sessions may retain old instructions; reload changed instructions or start a fresh session. Reloading alone is not a discovery test.
- Remove temporary worktrees/branches only after confirming they contain no uncommitted or unmerged work; use normal Git cleanup without force.

## Rollback

- Identify the faulty commits and a previously validated baseline from history/evidence.
- Revert the faulty changes in an isolated candidate using `git revert`; preserve local work and visible history.
- Validate the affected behavior, then promote using the same update rules.
- For urgent recovery, inform the user and temporarily repoint the single verified global link to a clean, validated worktree of the prior version.
- Record the temporary target, repair the normal source, restore its link, and verify discovery; leave no competing installation.

## Move or remove

- Validate a new source location before moving the installation; a source move can break the existing link.
- Inspect the old destination and unlink only the exact expected symlink. Preserve unexpected entries and project artifacts.
- For a move, create the link to the validated new package, update installation-path documentation, and verify fresh-session discovery.
- The guarded removal example below removes only the original link, including when its expected source is missing:

```sh
(
  dev_source=/Users/po/codeandconfigs/dev-command-library/skills/dev
  dev_link="$HOME/.agents/skills/dev"
  if test -L "$dev_link" && test "$(readlink "$dev_link")" = "$dev_source"; then
    unlink "$dev_link"
  else
    printf '%s\n' 'Unexpected installation; inspect before removing it.' >&2
    exit 1
  fi
)
```

- Keep the source repository, project instructions, designs, specifications, and evidence. Removing project references is a separate selected change.

## Troubleshooting

| Symptom | Inspect and resolve |
| --- | --- |
| `$dev` unavailable | Verify link/source, metadata, duplicate installations, and fresh-session catalog discovery. |
| Old behavior | Identify the loaded source/content; reload it or start a fresh session. |
| Required skill missing | Inspect the catalog and actual files; report the dependency and use the authorized native installation/update path. |
| Wrong project or ambiguous target | Check working directory and selected store; resolve an explicit/unambiguous target. |
| Checked tasks but finish blocked | Inspect current evidence and required findings; use work for fixes or verify for missing/stale evidence. |
| Spec synchronization fails | Keep the change active; resolve the native sync blocker before archive. |
| Copied database unavailable | Report the missing prerequisite; never fall back to production for QA. |
| Source changed during update | Preserve edits, compare identities/diffs, and reconcile before promotion. |

- Consult [commands](commands.md), [OpenSpec integration](openspec-workflow.md), and [engineering](engineering-and-verification.md) for operation-specific rules.
