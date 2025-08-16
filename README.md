# syslogtools — Sender & TUI Collector

This package bundles two CLI tools:

- **`syslog-pro`** — professional syslog traffic generator (RFC3164/5424; UDP/TCP/**TLS**; RFC6587 framing; templating; rate controls).
- **`syslog-tui`** — curses-based, colourised syslog collector with scrollback, search, filters, and save (UDP/TCP/**TLS**; RFC3164/5424; auto framing).

> **Note:** Binding to a specific address and/or using privileged ports (<1024 such as 514/6514) typically requires **sudo**.  
> On Linux you can alternatively grant `CAP_NET_BIND_SERVICE` to your Python interpreter.

## Install (editable)
```bash
cd syslogtools_pkg
python3 -m pip install -e .
```

## Console scripts
- `syslog-pro` — `syslog-pro --help`
- `syslog-tui` — `syslog-tui --help`

## Quick usage

Sender (RFC5424 over TCP, octet framing):
```bash
syslog-pro 127.0.0.1 --transport tcp -p 10514 --format 5424 -n 10 -m "hello {seq}"
```

Collector (UDP 5514 only):
```bash
sudo syslog-tui --udp-host 0.0.0.0 --udp-port 5514 --tcp-port 0
```

TLS collector (6514 on IPv6):
```bash
sudo syslog-tui --udp-port 0 --tcp-host :: --tcp-port 6514 --tls --certfile server.crt --keyfile server.key
```

## Linux: bind without sudo (optional)
```bash
sudo setcap 'cap_net_bind_service=+ep' $(readlink -f $(which python3))
# revert: sudo setcap -r $(readlink -f $(which python3))
```

## License
TBD by repository owner (e.g., MIT, BSD-2-Clause, Apache-2.0).
