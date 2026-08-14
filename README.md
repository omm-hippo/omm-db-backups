# omm-db-backups

Daily full snapshots of the [omm](https://github.com/omm-hippo/omm) project's Firebase Realtime Database (`/telemetry` node, currently the only node in the DB).

- `.github/workflows/backup.yml` runs once a day (03:30 UTC) and pulls the entire `/telemetry.json` tree via a plain GET (the node is publicly readable), overwriting `backups/telemetry.json` and committing it.
- Each fetch is a full export, not a diff of the previous one — so every commit on this file is a complete, independent point-in-time snapshot. Git history is the archive: `git log --oneline -- backups/telemetry.json` lists every day a snapshot changed; `git show <commit>:backups/telemetry.json` recovers that day's full state.
- Retention: unbounded — commits are never pruned.
- Trigger manually: `gh workflow run backup.yml --repo omm-hippo/omm-db-backups`
