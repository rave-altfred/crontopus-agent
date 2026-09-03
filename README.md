# Crontopus Agent

The on-host component of [Crontopus](https://app.crontopus.com): it discovers
the scheduled jobs that already exist on a machine (cron, Windows Task
Scheduler), reports their executions, and applies managed jobs. One static
binary, outbound HTTPS only — nothing listens on the host.

Releases: https://github.com/rave-altfred/crontopus-agent/releases — that
repository hosts binaries and installers only; the source is developed in a
private repository. Licensed under the [Apache License 2.0](LICENSE).

## Install

Get an enrollment token from **Targets → Add target** in the app; the panel
prints these commands with the token filled in. Tokens are single-use and
expire after 24 hours.

### Linux (amd64 / arm64)

Standard user, no root needed — discovers the schedules this user can read and
runs as a systemd user service:

```sh
curl -fsSL https://github.com/rave-altfred/crontopus-agent/releases/latest/download/install.sh | bash -s -- --api-url https://api.crontopus.com --enrollment-token enrtok_...
```

Full coverage (every user's schedules, managed deploys to `/etc/cron.d`) — the
same command with `sudo` installs a system service:

```sh
curl -fsSL https://github.com/rave-altfred/crontopus-agent/releases/latest/download/install.sh | sudo bash -s -- --api-url https://api.crontopus.com --enrollment-token enrtok_...
```

Re-running the installer upgrades the agent and restarts the service. The
binary lands in `~/.local/bin` (standard user) or `/usr/local/bin` (root).

### Windows (amd64)

From PowerShell:

```powershell
& ([scriptblock]::Create((irm https://github.com/rave-altfred/crontopus-agent/releases/latest/download/install.ps1))) -ApiUrl https://api.crontopus.com -EnrollmentToken enrtok_...
```

As Administrator this installs and starts the agent as a Windows service
(full coverage, managed jobs). As a standard user it runs a read-only agent in
the foreground for the current session.

## Commands

- `crontopus agent` — run the agent in the foreground.
- `crontopus install` — install or upgrade the background service (enrolls first
  when given a token).
- `crontopus run` — the wrapper managed jobs execute through; its exit code is
  always the wrapped command's, and it never blocks the job on the network.
- `crontopus version`.
