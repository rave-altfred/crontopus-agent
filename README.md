# Crontopus Agent

Prebuilt binaries for the [Crontopus](https://app.crontopus.com) agent — the
on-host component that discovers scheduled jobs (cron / Windows Task
Scheduler), reports executions, and applies managed jobs.

This repository hosts releases only; the Crontopus source lives in a private
repository and releases are published here automatically.

## Install — Linux (amd64 / arm64)

```sh
curl -fsSL https://github.com/rave-altfred/crontopus-agent/releases/latest/download/install.sh | sudo bash
```

Then enroll the host with an enrollment token from the Targets page and keep
the agent running (systemd or similar):

```sh
sudo crontopus agent --api-url https://api.crontopus.com --enrollment-token enrtok_...
```

## Install — Windows (amd64)

Download the latest `crontopus-agent_<version>_windows_amd64.zip` from
[Releases](https://github.com/rave-altfred/crontopus-agent/releases), unzip,
then from an elevated PowerShell:

```powershell
.\crontopus.exe install --api-url https://api.crontopus.com --enrollment-token enrtok_...
```

This installs and starts the agent as a Windows service.
