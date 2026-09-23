## Day 1 — journalctl (2026-09-22)

**Commands used:**
- `journalctl --since "..." --until "..."` — time-window filtering
- `journalctl --since today` / `--since yesterday` — relative day filtering
- `journalctl -f` — live follow
- `systemctl list-units --type=service --state=running` — confirm units before filtering
- `journalctl -u docker.service` — unit-scoped filtering

**Test:** pushed to GitHub → CI/CD triggered → container redeployed, watched live via `journalctl -f`; separately queried `docker.service` directly.

**Real finding:** `journalctl -u docker.service` surfaced a genuine `dockerd` healthcheck failure (`Unavailable: connection ...`, Sep 10) — buried in the full journal, immediate once scoped to the one unit.

