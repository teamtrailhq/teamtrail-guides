# Contributing a guide

Thanks for sharing a guide. This page covers how to write one, check it, send it, what review looks at, and how the catalog is built afterwards.

## In short

1. Fork this repo and clone your fork.
2. Add your guide as `guides/<id>.md` and a test example in `examples/<id>/`.
3. Run `npx teamtrail@next guides lint .` until it's clean.
4. Open a pull request, one guide per PR.

A maintainer reviews and merges it; CI then rebuilds `index.json`, and the guide shows up in `teamtrail guides search` and the Lookout's catalog.

## Write it

If you already wrote the guide for your own project (`npx teamtrail@next guides new <id>`), copy `.teamtrail/guides/<id>.md` into `guides/` here. Otherwise copy one of the files in `guides/`.

1. Save it as `guides/<id>.md`. The `id` is short and kebab-case (`a11y`, `api-design`), matches the file name, and isn't one of the built-in guides' ids (`builtin.json`).
2. Fill in the header:
   - `name`, `version` (semver, start at `1.0.0`), `summary` (one sentence) and `author` (you, or your team).
   - `handles.types`: the ticket types it's for (`research`, `prototype`, `junction`, `task`, `execute`, `review`).
   - `checklist`: up to 20 short items (200 characters each) the agent must answer when it finishes. Write things a person could check, not slogans.
   - `requiresChecks` (optional): names of checks the guide's tickets must pass, like `[a11y]`.
   - `proposedChecks` (optional): a check command per name, as a program and its arguments, like `run: [npx, pa11y-ci]`. No shells (`sh -c`), no network tools, no inline code (`node -e`). Each project's trail lead approves it before it ever runs.
   - `license`: MIT unless you have a reason.
3. Write the instructions below the header: what the agent should do, in plain steps. Up to 8 KB. Don't tell the agent to ignore other instructions, answer for the human, approve its own work or edit Teamtrail's files. The lint refuses those, and warns about links.
4. Add a test example in `examples/<id>/`: a ticket (or a diff, or a transcript) to try the guide on, and what a good run looks like.

## Check it locally

```bash
npx teamtrail@next guides lint guides/<id>.md
npx teamtrail@next guides lint .
```

The first checks one file; the second checks the whole catalog, including that every guide has an example. Every finding names its line. Try the guide in a real project with `npx teamtrail@next guides add ./guides/<id>.md` (that copies it into the project and pins it there).

## Send it

Push to your fork and open a pull request against `main`, one guide per PR. CI runs the same lint on every pull request. When you change an existing guide, bump its `version`. Don't edit `index.json`, `index.html` or the table in the README: they're generated after the merge.

## Review and Verified

A maintainer reads the whole guide and its example, and tries it on the example when that helps. They check that:

- it does what the summary says;
- the checklist is useful and checkable;
- any proposed command is safe and needed;
- nothing in it steers an agent around the human.

Maintainers squash-merge with a trailer naming the reviewer:

```
Add a11y guide

Reviewed-by: Jane Maintainer
```

## How index.json is built

After every merge to `main`, CI runs `scripts/build-guide-catalog.mjs` from the Teamtrail repo over this repo's full git history, and commits the result when it changed (`index.json`, `index.html` and the table in this README):

- every guide must pass the lint, or the build stops;
- each commit that changed a guide becomes a history entry, with the version at that commit and the reviewer from its `Reviewed-by:` trailer;
- a guide is **Verified** when its latest change has a reviewer;
- a change merged without one shows as **Not reviewed** until a reviewed change lands;
- each entry carries the file's sha256, and Teamtrail refuses a download that doesn't match it.

Built-in guides (listed in `builtin.json`) are copies of the ones that ship with Teamtrail. Change those in the Teamtrail repo, not here.

## Reports

If a guide misbehaves, open a report with the "Report a guide" issue form (the Lookout's Report link opens it). Maintainers list reported guides in `reported.json` while they look into it; the catalog then marks them as reported.
