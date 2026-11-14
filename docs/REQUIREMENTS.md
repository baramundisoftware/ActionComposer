# Requirements

What Action Composer needs, so you can allow only what you use.

## Everyone

- Windows 10 or 11, 64-bit.
- Administrator rights once, to install.
- Nothing else for building scripts, Software and Jobs and exporting them as `.bds` / `.bdx`. That works offline, without bMS.

## By feature

| Feature | What it needs |
|---|---|
| Build and export scripts, Software, Jobs | Nothing extra |
| Read from bMS (jobs, software, devices, vulnerabilities) | A read-only bConnect API key, and HTTPS to your bMS server |
| Publish to bMS | The Management Center (bMC) installed and signed in on the same PC, and a bMC user allowed to import bDX containers |
| Copy installers to the DIP | Read and write on the DIP share |
| Find installers with winget | HTTPS to `cdn.winget.microsoft.com` and to the installer's download host |
| AI Assistant (optional) | Your own Anthropic API key, and HTTPS to `api.anthropic.com` |
| GUI recorder | One Windows UAC prompt per recording |

## Hosts to allow

All connections are outbound. Web traffic is HTTPS only.

| Host | For |
|---|---|
| Your bMS server (bConnect) | Reading from bMS |
| Your DIP share (SMB) | Copying installers |
| `cdn.winget.microsoft.com` | winget |
| The vendor's download host, for example `github.com` and `release-assets.githubusercontent.com` | winget downloads. The app asks you once before it uses a new host. |
| `api.anthropic.com` | AI Assistant |

If your network uses its own certificate authority, it must be in the Windows Trusted Root store. Allow the bMS server and `api.anthropic.com` directly rather than through a proxy.

## bMS

- Tested with bMS 2026 R1 and 2026 R2.
- **bConnect API key:** read access to Endpoints, Jobs, Software, Variables, Update management and Compliance. Nothing more: the app never writes to bMS through bConnect.
- **Publish:** you approve every publish in the app. It stops in bMC's Import/Export screen, and an administrator imports it. Nothing is assigned to devices.

## Where it keeps things

| What | Where |
|---|---|
| Settings, sign-ins, AI key | `%APPDATA%\Action Composer` (protected by your Windows profile, not encrypted) |
| Publish approvals and log | `%LOCALAPPDATA%\Action Composer\bridge` |
| Installer copies | `<your DIP>\Apl\<Product>\<Version>\` (never overwritten) |

## Switching features off

- **AI:** set `STUDIO_AI=off` in the environment. The app then never contacts an AI service.
- **winget:** block `cdn.winget.microsoft.com`.
