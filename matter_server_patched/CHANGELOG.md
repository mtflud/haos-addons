# Changelog

## 1.2.2-wd.4

- Replace a node subscription immediately when the server's final data-report
  ACK cannot be delivered (peer-unresponsive), instead of waiting for the
  subscription timeout (~11 min on 10-min-interval battery devices). Cuts the
  stale-state window for missed contact-sensor reports to ~25-30s; queued
  events (e.g. a missed door close) arrive with the replacement subscription.
  Fork dist patch on `@matter/protocol`, guarded by behavioral tests and a
  patch canary ([release](https://github.com/mtflud/matterjs-server/releases/tag/v1.2.2-wd.4)).
- Ships matter.js 0.17.5-alpha.0-20260711 (upstream keepalive-liveness fix
  included; fork keepalive dist patch retired).

## 1.2.2-wd.3

- Blocker fix: empty subscription keepalives now refresh the watchdog's liveness signal (patched `@matter/node` `NetworkClient`, upstream [matter.js#4057](https://github.com/matter-js/matter.js/issues/4057)); healthy-but-quiet devices no longer false-trip at threshold. Guarded by a canary unit test and an end-to-end idle-node integration test ([release](https://github.com/mtflud/matterjs-server/releases/tag/v1.2.2-wd.3)).
- Watchdog: implausible (>24h) reported subscription intervals fall back to the 15-minute unknown-interval threshold instead of silently disabling protection ([matter.js#4058](https://github.com/matter-js/matter.js/issues/4058)).
- Time sync: `TimeNotAccepted` refusals now earn the full 24h cooldown instead of 5-minute retries.
- Production multi-stage image (dev toolchain removed, 900s healthcheck start period restored), digest-pinned base image, release workflow refuses overwriting existing tags.
- Docs: migration/rollback runbook, `stage: experimental`, watchdog disambiguation, stale translations removed.

## 1.2.2-wd.2

- Five upstream-targeted robustness fixes: guarded frame-build/observer conversion throws (frozen-state hazard), guarded attribute-cache updates, stale observer-group cleanup on re-register, time-sync cooldown only on success (5-min retry backoff on failure), unhandled-rejection hardening in the WS response path.

## 1.2.2-wd.1

- Initial fork release: matterjs-server 1.2.2 + subscription-liveness watchdog.
