# Matter Server (patched)

Fork of the official Home Assistant Matter Server add-on that runs
[mtflud/matterjs-server](https://github.com/mtflud/matterjs-server) — upstream
[matterjs-server](https://github.com/matter-js/matterjs-server) v1.2.2 plus a
**subscription-liveness watchdog**: it detects Matter node subscriptions that
die silently (node still "available", no data flowing) and forces a
resubscribe, bounded per-node with backoff, plus an hourly health snapshot in
the logs. Controlled by `--subscription-watchdog` (default on).

Differences from the official add-on:
- Base image is the fork build (`ghcr.io/mtflud/matterjs-server`).
- The `beta` / `matter_server_version` npm-override options are removed — this
  add-on always runs the patched server it ships with.

Intended to be temporary: retired once equivalent protection ships upstream.

## Not a drop-in replacement — read before installing

This add-on has its own identity (`matter_server_patched`) and therefore its
own persistent `/data`. Installing it does **not** transfer the official Matter
Server add-on's fabric credentials, commissioned nodes, storage, or options.
Starting it fresh creates a new, empty Matter controller, and its `discovery`
announcement can repoint Home Assistant's Matter integration at that empty
controller. Both add-ons use host networking on port 5580, so only one may run
at a time.

### Migration from the official add-on

1. Take a full Home Assistant backup, plus a partial backup of the official
   Matter Server add-on.
2. Install this add-on but do **not** start it.
3. Stop the official add-on and set its start-on-boot to off.
4. Copy the official add-on's persistent data into this add-on's data
   directory. With host-level shell access (HAOS developer SSH on port
   22222, or equivalent):
   `cp -a /mnt/data/supervisor/addons/data/core_matter_server/. /mnt/data/supervisor/addons/data/<repo-prefix>_matter_server_patched/`
   Without host access, transfer via a partial backup of the official
   add-on restored into this add-on's slug (advanced; requires editing the
   backup metadata). Either way: copy — never move or delete the original.
5. Start this add-on and wait for startup/migration to finish (watch the log).
6. Verify the Matter integration reconnects and all commissioned nodes are
   connected with live state updates.

### Rollback

1. Stop this add-on and set its start-on-boot to off.
2. Start the official add-on (its data was never touched).
3. Verify nodes reconnect.
