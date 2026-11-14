# FAQ

## Is Action Composer an official baramundi product?
No. It is a community project by baramundi colleagues. baramundi does not support it.

## What does it cost? What is the licence?
Free. Apache-2.0.

## What does it do?
It builds baramundi deployment scripts (`.bds`) visually. It packages them as Software and Job `.bdx` containers for baramundi Management Suite (bMS). The desktop app can also publish to bMS, find installers with winget, copy them to the DIP, record GUI actions, explain jobs and read vulnerabilities.

## Does it need internet?
Not for the core work. Building and exporting scripts, Publish and the recorder work offline. Internet is needed only for winget downloads and the AI Assistant. See [REQUIREMENTS.md](REQUIREMENTS.md).

## Does it change anything in bMS without my approval?
No. Publish needs your approval first, and your Windows user name is recorded. By default it stops in the Management Center's Import/Export screen, and an administrator clicks Import. A checkbox can import and open the job for you. It is off by default. Nothing is assigned to devices. The desktop app does not write to bMS through bConnect.

## Which bMS versions work?
Tested on bMS 2026R1 (26.1) and 2026R2 (26.2). Older versions: not yet tested.

## What bMS rights does it need?
A read-only bConnect API key for reads. For Publish, the bMC user must be allowed to import. See [REQUIREMENTS.md](REQUIREMENTS.md).

## Where are my credentials stored? Are they sent anywhere else?
In plain files in `%APPDATA%\Action Composer`, protected by your Windows profile. They are not encrypted. The bConnect key and the AI key go only to the address you configured. They are write-only: the app never shows them again. They are never sent over plain `http`, except to your own PC.

## Do I need an AI key?
No. The AI Assistant is optional. You bring your own Anthropic API key. Without it, everything else works. An administrator can turn AI off completely.

## What is sent to the AI service?
The request the app builds for the question you ask, with the items shown in the Assistant. The model does not write the output files. Nothing is sent until you use an AI feature.

## How are winget downloads verified?
The app reads the winget package list itself and never runs the winget program. The list must be signed by Microsoft and match its own hashes. Each manifest, and then the installer, is checked against a SHA-256 named by the step before. A file that does not match is thrown away. Only HTTPS is used. A download host you have not approved asks you once. The installer's digital signature is shown to you before you use the file.

## Why is the installer unsigned? Why does SmartScreen warn?
The project has no code-signing certificate yet. Windows warns about unsigned installers on first run. Choose More info, then Run anyway, if your policy allows it. Some organisations block unsigned installers.

## Why does the recorder show a UAC prompt?
The recorder must run with higher rights than the installer it records. There is one UAC prompt per recording. Press F10 to stop.

## Where are settings and logs?
Settings: `%APPDATA%\Action Composer`. Publish approvals and audit log: `%LOCALAPPDATA%\Action Composer\bridge`. Recorded sessions: the `captures` folder in the install folder.

## How do I uninstall?
Windows Settings, Apps, Action Composer. This removes the program and the `captures` folder. Delete `%APPDATA%\Action Composer` and `%LOCALAPPDATA%\Action Composer` if you also want your settings and sign-ins gone.

## Can I use a proxy or an internal certificate authority?
Put the CA in the Windows Trusted Root store. winget downloads use the Windows proxy settings. For bConnect and the AI Assistant, allow those hosts directly.

## How do I report an issue?
Open an issue in the project's GitHub repository. Do not paste API keys or server names.
