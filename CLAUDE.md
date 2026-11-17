# sommer-26

## Preview artifact (required after every change)

This repo has exactly ONE preview artifact on claude.ai. Its link is in
`.claude/preview-artifact.json` (`artifact_url`). The owner uses it to see what
has been built without deploying, so it must always match the repo.

Rules:
- Never create a second artifact for this repo. Always publish to the
  `artifact_url` above (Artifact tool, `url` set). In a new session, `read`
  the artifact once first, as the Artifact tool requires.
- The preview's source is `.claude/preview/index.html` (plus any files in
  `.claude/preview/`). It is a clickable, self-contained copy of the app's
  screens with realistic sample data (no login, no backend calls), and a
  change log.
- After ANY change to the repo (feature, fix, copy, data model), in the same task:
  1. Update the affected screens in `.claude/preview/index.html` so they
     show the new behaviour.
  2. Add a change-log entry at the top of the change log in that file:
     date, one line on what changed, and which screen shows it.
  3. Publish it to `artifact_url`.
  4. Run `bash .claude/hooks/preview-sync.sh`, then commit and push
     `.claude/` together with the change.
- A Stop hook (`.claude/hooks/preview-check.sh`) blocks the end of a turn
  when the repo changed but the preview was not synced.
