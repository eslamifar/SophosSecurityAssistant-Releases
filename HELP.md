# Sophos Security Assistant Help

Version **1.3.81** · Sophos Firewall 17.5 or later · Windows x64

> **Sleep more peacefully at night with Sophos Security Assistant.**

This browser-readable guide is provided with every release so users can review the application before installing it. The GitHub Release also includes the complete searchable Microsoft Compiled HTML Help file, `SophosSecurityAssistant-Help-v1.3.81.chm`.

## Contents

- [Requirements and installation](#requirements-and-installation)
- [Home and connection](#home-and-connection)
- [Hosts](#hosts)
- [Network](#network)
- [Threats and automatic Rules](#threats-and-automatic-rules)
- [Required firewall hardening](#required-firewall-hardening)
- [Manage](#manage)
- [Logging](#logging)
- [Desktop Widget](#desktop-widget)
- [Updates](#updates)
- [Troubleshooting](#troubleshooting)

## Requirements and installation

- Windows 10 or Windows 11 x64.
- Administrator approval is required when Manager starts and for installation or service control.
- Sophos Firewall 17.5 or later with XML API enabled and the Manager computer's IP allowed.
- UDP 514 Syslog forwarding is required for Threats. Forward IPS/ATP and Firewall events.
- Setup installs and starts the `SophosSecurityAssistantThreatCollector` Windows service and creates its Windows Firewall rule.
- Upgrades preserve user settings and stop Manager, Widget, and the collector safely before replacing files.

Download the latest Setup and standalone CHM from the [latest GitHub Release](https://github.com/eslamifar/SophosSecurityAssistant-Releases/releases/latest).

## Home and connection

Enter the Sophos host/IP address, HTTPS port, XML API username and password, optional SFOS 22 REST API key, group capacity, auto-disconnect choice, and SSL verification preference.

Password and REST API key values are protected with Windows DPAPI for the current Windows user and are not stored as plain text. Existing legacy plain-text settings are migrated automatically.

Manager tests compatibility after connection and enables supported management areas. The optional REST key is used only for the official SFOS 22 REST capability probe; the primary management workflow uses XML API.

## Hosts

### IPs

- Import IPv4 addresses from a TXT file or online source.
- Select an existing target group before analysis/import.
- Respect the configured group capacity.
- Use Dry Run before changing Sophos.
- Stop safely after the current batch or roll back the last supported batch.
- The selected target-group list is locked while an import is running.

### Groups

Browse IP groups and memberships, search, export, add groups or IP/network objects, edit host name and address, and remove selected members. Multiple removals use the bulk-capable workflow and can be cancelled between requests. Double-click an IP to edit it; deletion requires confirmation.

MAC and FQDN pages provide equivalent supported object-management workflows.

## Network

View and manage supported interfaces, gateways, static routes, and firewall rules. While connected, interfaces, gateway health, and routes refresh every minute from one network snapshot. The Widget uses the same gateway state.

> **Experimental:** The **Network > Rules** workspace is still being validated across SFOS versions. It provides ROOT/group navigation and readable rule details, but you should verify the detected rule type and values before using an available add, edit, delete, enable, or disable operation.

The Rules page follows the firewall position order and displays both rule groups and individual rules with ID, group, source, destination, service, action, feature, status, and group-count details. WebAdmin group metadata is reconciled with collapsed rule records so the left tree uses the real Sophos group names and displays every member. Named XML records can be inspected and changed when the connected API supports those operations; group rows never expose rule-only mutations. On SFOS 17.5, Manager automatically uses the validated WebAdmin Controller inventory and detail requests when the XML API returns only an empty FirewallRule template; those fallback records are read-only unless their change operation has been separately validated.

## Threats and automatic Rules

The collector stores IPS/ATP events continuously even when Manager is closed. Threat tables group events by source IP and support exact From/To filtering, sortable columns, Excel-compatible export, and a Live mode that advances To every five seconds.

Severity tabs are created dynamically. All retains the Severity column; individual severity tabs show Destination IP after Source IP. Double-click an IP to open its combined Timeline of attacks, automatic membership changes, expirations, and enforcement failures.

Rules can match Critical, Major, and Moderate events by attack count and rolling minute/hour/day windows. Automatic Rules:

- run in configured order through the Windows service;
- preserve existing memberships;
- promote an IP to its highest matching severity;
- suppress lower-severity downgrades;
- allow a stronger same-group Rule to extend, but never shorten, expiration;
- retain host objects after expiry;
- record automatic additions in severity CSV archives.

In the Rules grid, green identifies an enabled automatic Rule that is genuinely managed by a running, configured, unpaused and recently reporting Windows service. Selecting Automation alone is not sufficient. After a successful Add, Edit or Delete, Manager reloads the persisted shared Rule list once so the table matches the state visible to the service.

Use **Manage > Config > Set up automatic Rules** to save protected service credentials, configure trusted IP/CIDR exclusions, set the change-rate limit, and optionally catch up stored threats still inside Rule windows.

**Expirations** reloads shared Rule state every 60 seconds. **Trends** supports live or fixed date ranges and lists every attacking IP for a selected day. **Logs** displays Windows-service Rule actions with live or fixed filtering.

## Required firewall hardening

Adding a source IP to a Hacker group does not by itself guarantee that Sophos Business Application rules will reject it.

For every enabled WAN-to-LAN Business Application rule that publishes an internal server or service, add all four groups to **Blocked client networks**:

- `Hacker-Manual`
- `Hacker-Moderate`
- `Hacker-Major`
- `Hacker-Critical`

Keep the top-level WAN-to-LAN drop rule and IPS protection as additional layers. Apply the per-rule setting to every published HTTP, HTTPS, mail, VPN, and other relevant service.

Enable Firewall log forwarding to the collector. Version 1.3.73 parses both conventional FirewallRule containers and alternate/legacy flattened records used across SFOS versions, and falls back to the validated WebAdmin inventory on SFOS 17.5 when XML returns only a template. Business Application detection uses stable feature fields instead of relying only on a version-specific type label. If no matching rule can be identified, the warning reports returned-rule and classification counts; per-rule rejection reasons, field names and safe element paths are written to Logging > Application logs. It also inspects allowed Firewall events after an IP has become an active managed membership. A newly allowed connection is recorded as **ENFORCEMENT FAILURE**, included in the IP Timeline and collector report, and can trigger a critical-alert email.

A short interval exists between the first event and completed group membership. Connections established before membership may continue until they close or expire.

## Manage

### Backup / Restore

Request supported Local, FTP, or Email backups and restore supported configuration files. A successful FTP backup can also be copied to the configured local folder and optionally emailed after verification.

### Config

Control the collector service, open Windows Services, configure automatic Rules, select archive folders, and choose application-log retention from 14 through 365 days.

Automatic blocked-IP archives are maintained as `Critical.csv`, `Major.csv`, and `Moderate.csv`. Missing folders or files are recreated. Rows include source/destination IP, block time, blocked-until value, severity, Rule, and target group when available.

### Email

Configure SMTP with None, STARTTLS, or implicit SSL/TLS encryption. Test delivery before saving. Notification choices include Critical attacks, daily summaries, Rule failures, service/backup failures, capacity warnings, gateway changes, enforcement failures through Critical alerts, and verified FTP backup attachments.

## Logging

Logging reads all retained daily application logs over an exact From/To range. Live mode advances To automatically. Filter by Connection/API, Hosts/Groups, Network, Threats/Rules, Backup/Restore, Updates, Email, or Application. Logs record application runtime and Sophos connection duration.

Use **Privacy-protected diagnostic reporting** in Logging or About to preview the exact pending JSON and manually send it directly to `https://api.eslamifar.com`. A separate explicit opt-in permits automatic uploads after application errors, once daily at a chosen local time, at startup, and at exit; enable each trigger independently and withdraw consent at any time. The scheduled/start/exit triggers only send already-pending Error/Fatal diagnostics and do not generate usage or lifecycle telemetry. One-time sender setup requires the installation's client ID and HMAC secret, which Windows protects with DPAPI.

The payload is deliberately restricted to application/version, component/category, severity, exception type, a sanitized stack trace, timestamps, occurrence count, generic OS/.NET versions, and cryptographic identifiers. It does not include exception messages or raw logs. Client sanitization and server-side validation remove or reject usernames, passwords, secrets, tokens, IPv4/IPv6 addresses, MAC addresses, email addresses, URLs, hostnames, user paths, and raw client IDs.

This protects report content but cannot make a direct HTTPS connection invisible: IIS, a reverse proxy, and the network transport can inherently observe the source IP. The Receiver report database does not persist that source IP. Review the preview before a manual send and apply an appropriate IIS/proxy access-log retention policy.

Use Manage > Config to retain 14, 30, 60, 90, 120, 180, 270, or 365 days.

## Desktop Widget

The independent Widget shows Manager connection state, gateway health, the latest backup, and threat/collector status. Its cards open Manager at the related workspace. Closing Manager does not close the Widget or stop the collector service.

## Updates

Manager checks the dedicated release repository:

- once at startup;
- every 10 minutes while open;
- manually from About.

Unchanged releases use a lightweight conditional ETag request. Failed background checks back off to 20, 40, and at most 60 minutes, then return to 10 minutes after success. The automatic prompt appears once per discovered version; the title retains the update notice.

Downloaded Setup files are SHA-256 verified. Downloads support progress, pause/resume, and cancellation. The update cache preserves the installed/current target and newest applicable previous version while cleaning older folders.

## Troubleshooting

- **No threats:** confirm the collector is Running, UDP 514 is reachable, and IPS/ATP forwarding uses a threshold that includes Moderate events.
- **No enforcement verification:** enable Firewall logs for the SSM Syslog destination.
- **IP remains able to access a published service:** add all Hacker groups to the Business Application rule's Blocked client networks, then review Configuration Audit and Timeline.
- **Automatic Rules do not run:** repeat automatic Rule setup, verify protected service credentials, confirm the service is running, and inspect Threats > Logs.
- **Update check fails:** verify Windows date/time, DNS, HTTPS access to GitHub, proxy/VPN, and TLS inspection.
- **Saved secrets unavailable:** sign in with the Windows account that saved them or enter and save them again.
- **FTP copy fails:** provide the FTP password during the current Manager session and verify the configured local folder.

For searchable offline documentation, download and open `SophosSecurityAssistant-Help-v1.3.81.chm` from the Release assets.

