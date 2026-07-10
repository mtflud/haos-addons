# Changelog

## 1.2.2-wd.2

- Five upstream-targeted robustness fixes: guarded frame-build/observer conversion throws (frozen-state hazard), guarded attribute-cache updates, stale observer-group cleanup on re-register, time-sync cooldown only on success (5-min retry backoff on failure), unhandled-rejection hardening in the WS response path.

## 1.2.2-wd.1

- Initial fork release: matterjs-server 1.2.2 + subscription-liveness watchdog.
