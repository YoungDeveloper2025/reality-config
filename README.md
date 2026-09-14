# Reality Config

Install Xray-core and create a VLESS TCP REALITY configuration with `flow=xtls-rprx-vision`. The script displays a connection link and QR code.

Requires Linux with systemd, a public IPv4 address, root/sudo access, and curl. Allow the selected TCP port through your server and provider firewalls.

## Defaults

| Setting | Value |
| --- | --- |
| Xray-core | Latest stable release (no prereleases) |
| SNI | `play-apps-features.googleusercontent.com` |
| Port | `8443` |
| uTLS fingerprint | `firefox` (fixed; no selection menu) |

REALITY `dest` follows the selected SNI on port `443`. The destination must be reachable and support compatible TLS 1.3.

## IPv4 Routing

The connection link uses the server's IPv4 address. The `apple`, `meta`, `google`, `openai`, `spotify`, `netflix`, `reddit`, and `speedtest` geosite groups use the `IPv4` outbound with `ForceIPv4`. Other destinations use the normal `direct` outbound.

DNS uses `1.1.1.1` and `8.8.8.8` for IPv4 queries. HTTP/TLS/QUIC sniffing extracts visible domain names for routing and resolution. Traffic whose domain cannot be identified cannot match a geosite rule. Geodata is refreshed through the official installer before configuration validation.

## Manual Installation

Asks for the Xray version, SNI, and port. Press Enter to accept each default.

```bash
curl -fL --retry 3 -o reality.sh https://raw.githubusercontent.com/YoungDeveloper2025/reality-config/main/reality.sh && sudo bash reality.sh
```

## Automatic Installation

Asks only for the Xray version; other settings use their defaults.

```bash
curl -fL --retry 3 -o reality.sh https://raw.githubusercontent.com/YoungDeveloper2025/reality-config/main/reality.sh && sudo bash reality.sh --auto
```

## Version Selection

```text
Press Enter to use the latest stable Xray-core release (no prereleases). If you prefer a specific version, we recommend 26.6.27.
Enter the desired Xray-core version [latest version]:
```

Press Enter, or enter `latest` / `last`, to install the latest stable release, replacing any previously installed prerelease. Enter a version such as `26.6.27` or `v26.6.27` to install that specific release.

The configuration is validated explicitly as JSON and saved to `/usr/local/etc/xray/config.json`. Rerunning replaces it and generates new keys; the previous configuration is saved as `config.json.bak`.

`minClientVer` and `maxClientVer` are empty; `maxTimeDiff` is `0`.
