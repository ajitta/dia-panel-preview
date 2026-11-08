# dia-panel (preview)

A Claude Code plugin with one workflow, `review-panel`. It reviews one document with four skills from the [`dia`](https://github.com/ajitta/dialectic-skills) plugin at once and then has `dia-adjudicate` judge their reports:

1. Four agents run in parallel, each with one skill: `dia-negative`, `dia-reductio`, `dia-warrant` and `dia-counterplan`. Each returns its whole report in the skill's own layout.
2. Two agents run `dia-adjudicate` on the whole reports, each with the reports in a different order (the second order reverses the first).
3. A last agent lists the items on which the two judgments differ. Check those against the sources yourself; the workflow does not.

This is a preview. It is kept apart from the `dia` marketplace until it is known whether every surface that syncs that marketplace accepts a plugin with a workflow.

## Requirements

- Claude Code with workflows (tested on 2.1.314).
- `dia` 2.11.0 or later from the `dialectic-skills` marketplace.

## Install (Claude Code)

1. Add the `dia` marketplace and install `dia`, if you have not:
   ```
   claude plugin marketplace add ajitta/dialectic-skills
   claude plugin install dia@dialectic-skills
   ```
2. Add this marketplace and install the plugin:
   ```
   claude plugin marketplace add ajitta/dia-panel-preview
   claude plugin install dia-panel@dia-panel-preview
   ```
3. Start a new session.

## Use

Ask in a session, naming the document:

```
Run /dia-panel:review-panel on docs/design.md
```

To name the central claim the lenses should examine, add it: `... with the claim "the pilot needs 30 runs"`.

A run starts six to seven agents. In one test it took about 11 minutes and cost about US$4.60 on Opus at effort high. Under `claude -p`, set `CLAUDE_CODE_PRINT_BG_WAIT_CEILING_MS` (for example to `3600000`), or the print run may stop before the workflow ends.

## License

MIT
