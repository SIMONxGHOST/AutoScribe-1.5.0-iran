<div align="center">

# AutoScribe v1.5.0

**Find the Windscribe servers and protocols that actually work on your network.**

**English** · [فارسی](README.fa.md) · [Русский](README.ru.md)

</div>

---

AutoScribe is a desktop app that drives the official **Windscribe CLI** for you. It works through every
server, protocol and port you pick, connects to each one, measures ping, packet loss, and optional HTTP/HTTPS web
connectivity through the tunnel, and ranks the combinations that work best. It also includes a built-in
**Windscribe Log Diagnostics** analyzer (`config/log.bin`, `config.ovpn`, `wireguard_service.log`) to diagnose
WireGuard/AmneziaWG handshake timeouts and DPI blocks.

## What's New in v1.5.0

- **Node-level targeting & One server per city option** – Connects to the specific server nickname (`location`) instead of repeating identical city-only commands, plus an optional **One server per city** switch to deduplicate multi-node cities.
- **Free servers only filter** – Skip Pro-only locations (`is_premium` / `premium_only`) and mark `[FREE]` nodes in the location picker.
- **Keep Windscribe firewall option** – Optional switch to preserve Windscribe's firewall/Kill Switch instead of running `windscribe-cli firewall off` between tests.
- **HTTP/Web tunnel verification** – Optional HTTP/HTTPS check through the tunnel (`http://cp.cloudflare.com/generate_204` by default) alongside ICMP `ping`, with a dedicated **Web** latency column in Results, Best routes, SQLite DB, and CSV exports.
- **Built-in Windscribe Diagnostics tab** – Parses Windscribe's binary WireGuard ringbuffer (`config/log.bin`), `config.ovpn` anti-DPI parameters, and `wireguard_service.log` to summarize handshake timeouts and contacted endpoints.
- **Enhanced PingRunner** – Supports IPv4/IPv6 and localized `ping` outputs even when `TTL=` is omitted.

## Features

- **Automatic testing** – server × protocol × port, with WireGuard, IKEv2, UDP, TCP, Stealth and WStunnel.
- **Ping, packet loss & HTTP web check** through the tunnel.
- **Best routes** – a live leaderboard of the fastest working routes. Double-click a route to connect to it.
- **Searchable location picker** – type to find any country, city or server, filter by region, spot `[FREE]` servers, and select whole countries or single servers.
- **Up-to-date server list** – one click on **Update list** downloads the current server list from windscribe.com.
- **Protocol priority** – reorder protocols and choose exactly which ports to test.
- **Resume** – skip combinations that are already tested and pick up where you left off.
- **Stop on first success** – stop the run and stay connected as soon as one route works.
- **Profiles** – save and load complete sets of settings.
- **Live dashboard** – the server being tested, each step (disconnect → connect → settle → ping/web), progress, time left, success rate and best ping.
- **What works here** – success rate per protocol, with a tip when a protocol keeps failing.
- **Diagnostics tab** – inspect `config/log.bin` binary ringbuffer logs and OpenVPN anti-censorship directives.
- **CSV export** of all results (including HTTP latency) to the `reports/` folder.
- **Three languages** – English, Farsi (fully right-to-left) and Russian.

## Requirements

- **Windows 10/11** (Linux and macOS work too if `windscribe-cli` is on your `PATH`)
- **Python 3.9+** with Tkinter (included in the standard Windows installer) and `customtkinter`
- **Windscribe desktop app**, signed in (`C:\Program Files\Windscribe\windscribe-cli.exe`).

## Installation

```bash
pip install -r requirements.txt
python main.py
```

## Building a standalone .exe

```bash
pip install pyinstaller
pyinstaller --noconsole --onefile --name AutoScribe --collect-data customtkinter main.py
```

Put `locations.json` in the same folder as `dist\AutoScribe.exe` (or run `build_exe.bat` on Windows).

## License

Released under the **MIT License with a removal-on-request condition**. See [LICENSE](LICENSE).
