## Day 1 — journalctl (2026-09-22)

**Commands used:**
- `journalctl --since "..." --until "..."` — time-window filtering
- `journalctl --since today` / `--since yesterday` — relative day filtering
- `journalctl -f` — live follow
- `systemctl list-units --type=service --state=running` — confirm units before filtering
- `journalctl -u docker.service` — unit-scoped filtering

**Test:** pushed to GitHub → CI/CD triggered → container redeployed, watched live via `journalctl -f`; separately queried `docker.service` directly.

**Real finding:** `journalctl -u docker.service` surfaced a genuine `dockerd` healthcheck failure (`Unavailable: connection ...`, Sep 10) — buried in the full journal, immediate once scoped to the one unit.

## Day 2 - systemctl (20206-09-24)

**Commands Used:** 
- `systemctl --help` - To learn about the tool
- `systemctl list-units` - To get a list of currently on memomory 
- `systemctl stop Docker` - To stop the docker.service
- `systemctl restart Doccker` - to restart the unnit
- `systemctl is-active ssh` - Check whether units are failed or system is in degraded state
- `systemctl status ssh` - Show runtime details of a unit or job 

**Test:** Checked runtime information of some units/jobs using `systemctl status -unit`; stoped and restarted and checked them again. 