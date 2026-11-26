# Sophos Security Assistant 1.3.97

![Sophos Security Assistant](SecurityAssistantIcon.png)

> Sleep more peacefully with Sophos Security Assistant.

## Highlights

- Adds an independent Windows Repair Watchdog that checks the Threat Collector and heartbeat every minute and restarts stopped or stale collection.
- Adds protected offline recovery from the last successfully installed Setup, guarded by SHA-256, Authenticode signer matching, and repair rate limits.
- Sends important repair results to the Windows Application event log, Widget, and enabled service-alert email.
- Preserves Automatic Rules recovery, heartbeat monitoring, Widget and sustained performance alerts, 10/30/60-second service recovery, privacy-protected diagnostics, and the corrected uninstall workflow.
- Fixes missing heartbeat data being treated as healthy and ensures transiently locked Watchdog/cache files are removed during uninstall.

`Network > Rules` remains **Experimental**. Verify the detected rule type and values before applying changes.

Privacy-protected diagnostic reporting remains only in `Manage > Config`. Endpoint, Client ID, and Secret are not exposed in the UI.

## Verification

- Release build: 0 errors, 0 warnings
- Automated tests: 139 passed, 0 failed
- Packaged and installed Manager/Widget smoke tests: passed
- Upgrade from 1.3.96, fresh install, complete uninstall, and final reinstall: passed
- Threat Collector and Repair Watchdog: Running, Automatic; recovery actions 10/30/60 seconds
- NuGet vulnerability audit: no vulnerable packages reported

## Code-signing notice

**Status: NotSigned.** No trusted Code Signing certificate with a private key was available for this release. Windows may display Unknown publisher or Microsoft Defender SmartScreen. Monitoring and service restart remain operational, but unattended offline reinstallation is intentionally refused for an unsigned Setup because signer verification cannot be satisfied.

## SHA-256

```text
395450C57CCE17F2EB6A24C4C30B78D55295A50D0A3CF32768416F92E3F795C3  SophosSecurityAssistant-Setup-1.3.97-win-x64.exe
40A5EBFB28C3513BE0050D1ADFD7B0EF17022645CC2F26D05CAD9C5F5997A737  SophosSecurityAssistant-Help-v1.3.97.chm
```

Source commit: `1319c2ad36d77824ab3d1e5ab9299a3797200306`
