# Matter Server (patched)

See the README for what this fork changes. Configuration matches the official
Matter Server add-on minus the removed npm-override options:

- **log_level**: Matter Server log level.
- **enable_test_net_dcl**: test-net DCL usage (development only).
- **ble_proxy** / **bluetooth_adapter_id**: BLE commissioning options.
- **matter_server_args**: extra CLI arguments (e.g. `--subscription-watchdog false`
  to disable the watchdog).
- **matter_server_env_vars**: extra environment variables (KEY=VALUE).

The Home Assistant Matter integration connects via WebSocket on port 5580.
