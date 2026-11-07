# chris-tools — the hands of Chris Enterprise

The living inventory of the tools, systems, and automation Chris operates for Tariq Chehardy. Maintained by Chris: when a tool is added, retired, or changed, this file changes in the same pass. No empty sections — if it is listed, it is real and running, or it is marked plainly as retired.

## Communication

| Tool | What it does | State |
|---|---|---|
| **Chris Chat** | GUI + terminal chat living inside the PC, on both desktops, so Tariq can text Chris in-PC and Chris can reply, work, and control from there. Live typing indicator, quick-job buttons, 15-second inbox watcher. | Running |
| **WhatsApp channel** | Tariq can reach Chris from WhatsApp as an outside-the-app channel. | Linked |
| **Muse main chat** | The primary conversation — where orders land and results are delivered. | Running |

## The PC (operated estate)

| System | What it is | State |
|---|---|---|
| **Workstation PC** | Ubuntu 24.04, full XFCE desktop (everyday + advanced packs: office suite, image editors, development tools, VS Code), Helium default browser, Tor Browser for the non-root desktop. | Running |
| **Reset rebuild** | `rebuild-all.sh` — one idempotent script that restores the entire estate after a platform reset: packages, desktop, password hashes, tunnels, watchdog, fleet, container. An hourly check reports only when something was actually rebuilt or failed. | Running |
| **xubuntu-test container** | Isolated Xubuntu + XFCE workstation with its own remote desktop and tunnel, proxied egress through a host proxy with its own CA, and a compressed snapshot + restore script so it survives resets and accidents. | Running |

## Remote access

| System | What it does | State |
|---|---|---|
| **Bore tunnels** | Reverse tunnels exposing the two desktops (main PC and container). Addresses rotate on restart — they are always read fresh from the endpoint files, never quoted from memory. | Running |
| **Tunnel watchdog** | Probes both tunnel mappings at the protocol level every 5 minutes against the relay's true address; restarts a dead mapping (max once per 15 min each). Caught and fixed a silently-dead mapping within minutes of its first verified login on day one. | Running |
| **Serveo fallback** | A tested hot fallback route if the primary relay goes down. Rotates by design; treated as the spare, not the main route. | Running |
| **Tailscale** | Connected, client-only. Does not change the remote-access path; the tunnels are the way in. | Connected |

## The fleet

| System | What it is | State |
|---|---|---|
| **Chris Agent Fleet** | 110 agents staged and supervised as a system service: 10 lead agents (`chris-lead-01`–`10`), exact clones differing only in workstream, each commanding the same 10-role specialist team (orchestration, architecture, reverse engineering, firmware, backend, frontend, data/ML, QA, security, release). Heartbeat every 30 seconds. | Running |
| **Default squad** | 6 agents deploy by default for every task, always — the fleet scales to 110 when the work needs it. | Standing order |

## Verification standards (how Chris proves things)

- A remote login counts **only** when the server-side log records it — a client holding a session proves nothing.
- A tunnel address is quoted **only** after being read fresh and verified end to end.
- Code ships only after its tests run. A check that was not run is stated as not run.

## Credentials policy

Passwords are stored as salted hashes only — never in plain text, never in this repository, never in chat. That arrangement was Tariq's explicit choice and stands.

---

*Part of [Chris Enterprise](https://github.com/chris-enterprise) — designed, polished, and filled continuously. No empty noise. No untouched spaces.*
