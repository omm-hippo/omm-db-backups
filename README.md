# omm-db-backups

Daily full snapshots of the [omm](https://github.com/omm-hippo/omm) project's Firebase Realtime Database (`/telemetry` node, currently the only node in the DB).

- `.github/workflows/backup.yml` runs once a day (03:30 UTC) and pulls the entire `/telemetry.json` tree via a plain GET (the node is publicly readable), writing it to `backups/YYYY-MM-DD.json`.
- Retention: unbounded — every day's snapshot is kept forever as its own commit/file.
- Not a diff — each file is a complete point-in-time export, independent of every other file.
- Trigger manually: `gh workflow run backup.yml --repo omm-hippo/omm-db-backups`
