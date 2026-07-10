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
