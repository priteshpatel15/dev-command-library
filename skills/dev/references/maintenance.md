# Installation and maintenance

The source repository owns this library. A single global skill link exposes its `skills/dev` package to Codex. Product artifacts remain in their projects or configured OpenSpec stores.

## Dependencies and discovery

Required capabilities are Codex skills, the OpenSpec CLI and corresponding installed workflows, and the installed Ponytail skill. Project testing dependencies are discovered by `$dev setup` rather than globally prescribed.

Resolve skills from the current available-skill catalog and read their actual files. Do not hardcode a versioned Ponytail plugin-cache path. An installed file and discovery by a new Codex session are separate checks.

`$dev setup` can diagnose missing capabilities and initialize OpenSpec in the selected project. It must not pretend that a locally absent skill ran. Native OpenSpec initialization owns its generated skills and metadata; preserve existing stores and custom schemas.

## First installation

The initial approved locations are:

```text
source repository: /Users/po/codeandconfigs/dev-command-library
skill package:     /Users/po/codeandconfigs/dev-command-library/skills/dev
global link:       /Users/po/.agents/skills/dev
```

Before installing, validate the source package and behavioral scenarios. Inspect the destination, including dangling links, and preserve an unexpected existing `dev` installation. A matching link already completes the filesystem installation step.

Run these shell commands only after the source has been created and validated:

```sh
dev_source=/Users/po/codeandconfigs/dev-command-library/skills/dev
dev_link="$HOME/.agents/skills/dev"
test -f "$dev_source/SKILL.md"
ls -ld "$dev_link"
readlink "$dev_link"
```

For a first installation, the last two commands will report that no destination exists. If both a real entry and a dangling link are absent, create the link without a force option:

```sh
mkdir -p "$HOME/.agents/skills"
if test -f "$dev_source/SKILL.md" && test ! -e "$dev_link" && test ! -L "$dev_link"; then
  ln -s "$dev_source" "$dev_link"
else
  printf '%s\n' 'Missing source or existing destination: inspect before installing.'
fi
test -f "$dev_link/SKILL.md"
readlink "$dev_link"
```

The explicit absence checks also catch dangling links and existing directories; an unguarded `ln -s` can create a link inside an existing directory. Do not use a force option, delete an existing installation, or create another same-name skill under a second global skill directory.

Changing global files can require filesystem approval in the active Codex environment. Use the environment's normal approval mechanism for the exact authorized installation if needed; a failed attempt is not evidence of installation.

Start a fresh Codex session in an unrelated temporary project. Confirm `dev` appears in its skill catalog, invoke `$dev status`, and inspect that it loads the linked package and chooses the temporary project. Then exercise `$dev setup` in that isolated project. Only a successful observed check establishes global discovery and cross-project behavior.

The supported global location and symlink behavior are documented in [OpenAI's local skill guide](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills). Verify provider changes when troubleshooting a different Codex version.

## Validation before release

1. Read the changed command's contract and identify affected references, templates, project behavior, and evaluation scenarios.
2. Run the installed `skill-creator` validator against the candidate's `skills/dev` directory. Resolve the validator from the installed skill rather than embedding its path in the runtime library.
3. Check Markdown links, template references, skill metadata, and consistency between documented inputs/outputs and instructions.
4. Run relevant behavioral scenarios from the source repository's `tests/scenarios.md` in isolated projects. Evaluate actual artifacts and actions, not fixed prose or heading matches.
5. Obtain independent review for material workflow or gate changes. Fix demonstrated failures and repeat affected scenarios.
6. Record the candidate identity, observed results, limitations, and safe evidence paths under `tests/evidence/`.

The structural validator checks skill format; it does not prove command correctness. A fixture that deliberately blocks unsafe database use proves that guard case, not successful real-database acceptance. A successful tiny UI fixture does not qualify any product project's UI.

Reports must identify tests not run, failed, skipped, or blocked. Do not record browser QA or agent behavior from inference. Keep credentials, connection secrets, personal data, and raw sensitive traces out of committed reports. Prefer redacted references to existing safe test output.

## Updating without exposing unvalidated instructions

The global link points at a live source directory. Editing that directory immediately changes the instructions visible to new skill loads, even before committing. Create a candidate outside the linked working tree for substantial updates.

Start with clean source history and no active sessions depending on an update. A Git worktree is sufficient; there is no release server or custom installer:

```sh
dev_repo=/Users/po/codeandconfigs/dev-command-library
git -C "$dev_repo" status --short
git -C "$dev_repo" rev-parse HEAD
git -C "$dev_repo" worktree add -b dev-library-update /private/tmp/dev-library-update
```

Choose another unused branch/path when those names already exist; preserve prior work. Edit and validate the candidate there, invoking its `SKILL.md` by explicit path for evaluation. Commit only intended library files and retained evidence in the candidate. Do not change the global link for candidate tests.

After the candidate passes, review its diff and fast-forward the linked source branch:

```sh
git -C "$dev_repo" diff HEAD..dev-library-update --stat
git -C "$dev_repo" merge --ff-only dev-library-update
```

A divergent history or local changes require inspection, not a forced reset. Record the previous and new commit identities. Verify the global link, start a fresh session, and repeat discovery plus an affected-command smoke test. Existing sessions may retain previously loaded instructions; begin a new session after an update.

Remove the candidate worktree/branch only after checking it has no uncommitted or unmerged work, using Git's normal worktree commands without force. For small edits the same principle applies: validate before allowing development sessions to consume the changed instructions.

## Rollback

Identify the last passing release and the specific faulty commits from source history and evaluation reports. Preserve local work. Revert the faulty commit or commits in an isolated candidate, rerun affected validation, and fast-forward the linked source as above. Use ordinary `git revert` so the rollback is visible in history; do not hard-reset or clean a working directory.

For an unusable installation requiring immediate recovery, temporarily point the single global skill link at a verified clean worktree of the last passing commit after inspecting the destination and informing the user. Record that temporary location, repair the normal source through a reviewed revert, and restore the original link. Do not leave a second same-name installation.

## Moving or removing the installation

Moving the source repository breaks the link. After validating the new source location, inspect the old link, remove only that verified link, and create a new link to the new `skills/dev` path. Recheck discovery in a fresh session.

To remove the original installation while keeping its source and every project's artifacts, verify the exact link target before unlinking:

```sh
dev_source=/Users/po/codeandconfigs/dev-command-library/skills/dev
dev_link="$HOME/.agents/skills/dev"
if test -L "$dev_link" && test "$(readlink "$dev_link")" = "$dev_source"; then
  unlink "$dev_link"
else
  printf '%s\n' 'Unexpected installation: inspect it before removal.'
fi
```

This removes the symlink only. It does not delete the source repository, project instructions, designs, OpenSpec specifications, or retained evidence. Review project references separately if you intend to stop using the workflow.

## Troubleshooting

| Symptom | Inspect and resolve |
|---|---|
| `$dev` unavailable | Verify link target and `SKILL.md`, inspect duplicate names, validate metadata, then start a fresh Codex session. |
| Old behavior after update | Check which file/session was loaded; start a fresh session at the verified release. |
| Ponytail or an OpenSpec workflow missing | Resolve the installed catalog and actual files; install/update the missing dependency with appropriate authority. Do not substitute an invented equivalent. |
| Wrong project or ambiguous change | Confirm current working directory and configured OpenSpec store; provide the target explicitly. No last-used global pointer exists. |
| Checked tasks but `finish` blocked | Inspect `verification.md` for stale identity, missing required coverage, failed checks, or unresolved engineering findings. Use `work` for fixes or `verify` for evidence refresh. |
| Required spec sync failed | Leave the change active; resolve the delta/main-spec mismatch before archival. |
| Copied database unavailable | Report the exact missing connection/identity prerequisite. Never use a production database to make QA pass. |
| Global source changed unexpectedly | Inspect Git status and recent history; preserve edits, then compare with the last evaluated identity. |

Operational details remain in the [command reference](commands.md), [OpenSpec integration](openspec-workflow.md), and [engineering reference](engineering-and-verification.md).
