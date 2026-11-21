# Changelog

## 1.3.95 - 2026-11-21

### Added

- Add an independent automatic Rule heartbeat so Manager and Widget can detect a stopped automation worker even when the Windows service remains running.
- Add red Widget states and deduplicated Windows notifications for a stopped collector, stale or unavailable Rule status, missing credentials, paused automation, consecutive failures, and no enabled automatic Rules.
- Configure Windows service recovery to restart the Threat Collector after unexpected failures.

### Changed

- Send the separately enabled Rule-failure email for each failed automation attempt, while still pausing automation after three consecutive failures.
- Keep the collector service alive when its Rule worker exits unexpectedly so the stale heartbeat is visible and a critical service/Rule alert can be attempted.
- Place application-log retention and **Save config** on one aligned row and increase the Home performance action row so Refresh is not clipped.

### Fixed

- Distinguish a healthy Windows service from an unresponsive automatic Rule worker in the Widget.
- Prevent unchanged Rule-engine alerts from producing a notification every ten-second Widget refresh.

### Security

- Retain the privacy contract: diagnostic reporting remains only in **Manage > Config**, transport credentials remain hidden, and consent, sanitization, and temporary-file cleanup remain enforced.

### Documentation

- Document automatic Rule heartbeat monitoring, Widget failure states, service recovery, Rule-failure email behavior, and the continued experimental status of **Network > Rules**.

### Known limitations

- **Network > Rules** remains experimental across SFOS versions; verify detected rule types and values before applying changes.
- Widget automation health depends on the shared public heartbeat written by the Threat Collector and reports it as stale after 45 seconds without an update.

## 1.3.94 - 2026-11-20

### Added

- Add a connected-only **Home > Information** page with firewall identity and persisted CPU, memory, disk, and per-interface performance information.
- Parse Sophos System Health Usage Syslog in the Threat Collector, store the latest snapshot in ProgramData, and refresh the Manager view every minute while preserving collection after Manager closes.
- Add automated coverage for merging CPU, memory, disk, and interface health messages and ignoring unrelated Syslog records.

### Changed

- Separate Home connection controls from connected information so the identity and performance view has dedicated space and a clear availability state.
- Include accepted System Health messages in collector status without misclassifying them as rejected non-threat packets.

### Fixed

- Keep threat-event counters unchanged when a valid performance-only Syslog record is received.
- Report missing and stale performance data explicitly instead of displaying misleading zero values.
- Clean stale privacy-report temporary files and remove the current temporary file even when an atomic settings or pending-report replacement is interrupted.

### Security

- Retain the 1.3.93 privacy contract: diagnostic reporting remains only in **Manage > Config**, transport credentials remain hidden, and consent/sanitization requirements remain enforced.

### Documentation

- Document System Health forwarding, Home performance monitoring, release installation, and the continued experimental status of **Network > Rules** in README, browser Help, compiled Help, and release notes.

### Known limitations

- **Network > Rules** remains experimental across SFOS versions; verify detected rule types and values before applying changes.
- Performance information depends on Sophos System Health Usage Syslog forwarding to this computer on UDP 514 and is marked stale after five minutes without an update.

## 1.3.93 - 2026-11-12

- Audit all branches, worktrees, reflogs, unreachable commits, local artifacts, tags, and releases before preparing the official release source.
- Keep privacy-protected diagnostic reporting exclusively in Manage > Config and remove Endpoint, Client ID, Secret, About, and Logging shortcuts from the UI.
- Add a release feature contract that prevents diagnostic transport settings or non-Config shortcuts from returning in future builds.
- Refresh version metadata, README, browser-readable Help, compiled Help inputs, and release documentation while retaining the experimental Network > Rules notice and stable Latest Release link.

## 1.3.92 - 2026-11-12

- Carry forward every change already integrated into the official `master` source and publish a synchronized 1.3.92 application, Widget, Threat Collector, Help, and Setup.
- Refresh README, browser-readable Help, compiled CHM Help, and release metadata while retaining the experimental notice for Network > Rules and the stable Latest Release download link.
- Re-run the full build, automated test suite, packaged startup checks, NuGet vulnerability audit, and local Setup/service verification before publication.

## 1.3.91 - 2026-11-11

- Refreshed the official release from the fully synchronized master source, including README, browser-readable Help, compiled Help, Setup metadata, and updater assets.
- Added end-to-end release verification that installs the generated Setup locally and confirms the installed Manager version and Threat Collector service state.

## 1.3.90 - 2026-11-10

- Added persistent Previous day and Next day controls to Threats > Trends, using complete-day ranges, disabling Next day on today, preventing future navigation, and enforcing their presence during release builds.
- Added a guarded Reinstall action to About so users can download, SHA-256 verify, and run the latest installer even when the installed version is already current.
- Locked the Home connection-settings group while connected so displayed values cannot diverge from the active session.

## 1.3.89 - 2026-11-10

- Restored persistent Previous day / Next day controls before the Threats From filter across All and severity tabs, prevented navigation beyond today, and added unit tests plus a release-build feature contract.
- Improved Sophos Log viewer CSV import to preserve each event's severity and request catch-up evaluation across every enabled automatic Rule without requiring a target Rule selection.
- Added regression coverage confirming imported Moderate, Major, and Critical events are routed to the matching automatic Rules.

## 1.3.88 - 2026-11-10

- Added duplicate-safe import of Sophos Log viewer IPS/IDP and ATP CSV exports, with validation, result counts, and optional immediate Rule preview.
- Simplified the Threat Rules grid: click Enabled to save the state, edit Order directly, drag rows to reorder, and double-click a row to edit it. Removed the redundant Edit, Move up/down, and Enable/Disable buttons.
- Added Previous/Next pagination for the All, Critical, Major, and Moderate threat tabs while preserving full-result sorting and export.
- Hardened Setup logging and Windows service validation so pending-deletion and missing Collector configurations no longer appear as successful installs.

## 1.3.87 - 2026-11-10

- Move Threat Collector service creation/configuration into verified installer code that checks every Windows Service Control exit code instead of continuing silently.
- Validate the copied collector executable before service creation, enable Setup logging, and provide actionable guidance for Windows error 1072 (service marked for deletion).
- Refresh README, browser-readable Help and compiled Help with the application icon, retain the experimental notice for Network > Rules, and keep the stable Latest Release download link.

## 1.3.86 - 2026-11-08

- Refresh README and browser-readable Help with the real Sophos Security Assistant icon and restrained visual markers for download and navigation.
- Refresh compiled Help, retain the experimental notice for Network > Rules, and keep the stable Latest Release download link.

## 1.3.85 - 2026-11-04

- Make **Restart service** wait for Windows to confirm the Threat Collector is fully stopped before starting it again, then verify that it reaches the running state.
- Refresh README, browser-readable Help and compiled Help, retain the experimental notice for Network > Rules, and keep the stable Latest Release download link.

## 1.3.84 - 2026-11-04

- Detect changes to the Sophos host, API port, username, or password when Windows-service Rule automation is already configured, and display a persistent action-required warning.
- Keep the warning visible until **Manage > Config > Set up automatic Rules > Test and enable** succeeds with the current Sophos credentials.
- Refresh README, browser-readable Help and compiled Help, retain the experimental notice for Network > Rules, and add a stable Latest Release download link.

## 1.3.81 - 2026-10-30

- Finalize the consent-based, privacy-protected diagnostic workflow for direct delivery to the development team through `api.eslamifar.com`.
- Preserve the application product name in every report so the Receiver can safely accept and group diagnostics from multiple applications.
- Keep manual preview and confirmation, independent automatic-report opt-ins, client/server sensitive-data rejection, and transparent delivery status as release requirements.
- Refresh README, browser-readable Help and compiled Help while retaining the experimental notice for Network > Rules.

## 1.3.80 - 2026-10-30

- Replace the temporary GitHub issue workflow with direct, HMAC-authenticated HTTPS delivery to `api.eslamifar.com`, including exact-payload preview, explicit confirmation for manual sends, retry/backoff, and visible delivery status.
- Add independent opt-in automatic-report triggers for application errors, a selected daily local time, application startup, and application exit.
- Strengthen privacy enforcement on both client and Receiver: exclude exception messages and raw logs; sanitize or reject usernames, credentials, IPv4/IPv6 addresses, MAC addresses, email addresses, URLs, host/user/network paths, and raw client IDs; document the unavoidable transport-level visibility of source IP to IIS/reverse proxies.
- Include the application product name in every report and keep Receiver grouping isolated by application name and fingerprint for safe multi-application diagnostics.
- Refresh README, browser-readable Help and compiled Help while retaining the experimental notice for Network > Rules.

## 1.3.79 - 2026-10-29

- Add an explicit-consent problem-report workflow from Logging and About that previews exactly what will be shared before opening the development team's GitHub issue page.
- Let the user independently include or exclude basic system information and up to 80 recent application log entries; nothing is transmitted automatically.
- Sanitize passwords, passphrases, secrets, tokens, authorization values, cookies, API keys and URL credentials before the report is displayed or copied.
- Copy the complete sanitized report to the clipboard and prefill a bounded GitHub issue so the user retains final control over submission.
- Refresh README, browser-readable Help and compiled Help while retaining the experimental notice for Network > Rules.

## 1.3.78 - 2026-10-28

- Highlight a Threats > Rules row in green only when the enabled automatic Rule is genuinely managed by a running, configured, unpaused and recently reporting Windows service.
- Reload the shared Rule store once after every successful add, edit or delete so the grid immediately reflects the service-visible persisted state.
- Refresh README, browser-readable Help and compiled Help while retaining the experimental notice for Network > Rules.

## 1.3.77 - 2026-10-26

- Preserve the authoritative SFOS 17.5 WebAdmin WAN-audit result when Business Application inventory is unavailable instead of falling through to populated-but-unnamed XML templates and showing a misleading modal warning.
- Require a trusted Authenticode Code Signing certificate for release Setup builds, sign and timestamp first-party binaries plus the final installer, and verify every signature before a build can be published. Unsigned output now requires an explicit local-test override.
- Load the separate SFOS 17.5 `main=3` firewall metadata response so Network > Rules uses the real WebAdmin group names, complete membership lists and group-zone labels instead of synthetic `Group N` nodes with one representative rule.
- Stop treating the SFOS 17.5 User/Network inventory as Business Application evidence during the WAN enforcement audit; the known inventory limitation is logged without showing a false missing-WAN-rule warning.
- Reconcile collapsed SFOS WebAdmin rule records with late `firewallGroupList` metadata so Network > Rules shows the real group names and every member rule.
- Update the product slogan in README, browser/compiled Help, and the in-app About dialog.
- Update Microsoft and MailKit dependencies to patched releases and pin the safe cryptography package version so NuGet reports no known vulnerable packages.

## 1.3.76 - 2026-10-24

- Rename the product, solution, projects, executables, service, data folders, Help, Setup, and repositories to Sophos Security Assistant.
- Move update discovery to the dedicated SophosSecurityAssistant-Releases repository while retaining safe upgrade compatibility with existing installations.
- Complete the SFOS 17.5 WebAdmin firewall-rule inventory by loading named groups and their member rules, and keep ROOT limited to ungrouped rules.
- Add the product slogan to README and Help while retaining the experimental notice for Network > Rules.

## 1.3.75 - 2026-10-23

- Audit WAN enforcement against the dedicated WAN rule inventory on SFOS 17.5 instead of the User/Network rule page.
- Add a ROOT-and-groups navigation tree to Network > Rules and show only the selected group's member rules.
- Replace raw JSON in the read-only rule-details view with labelled rule fields.
- Improve legacy rule group-name, source/destination-zone, and Reject-action resolution.
- Mark Network > Rules as experimental while cross-version write operations continue to be validated.

## 1.3.74 - 2026-10-22

- Preserve the SFOS WebAdmin firewall-rule position order instead of sorting legacy rules by name.
- Display firewall rule groups together with their rule counts, and prevent group rows from exposing rule-only mutation actions.
- Align Network > Rules columns with Sophos WebAdmin: ID, Name, Group, Source, Destination, What, Action, Features, and Status.
- Resolve nested SFOS 17.5 lookup data more reliably so zones, hosts, services, and Business Application details are shown by their labels.

## 1.3.73 - 2026-10-19

- Add Network > Rules with Sophos firewall-rule inventory, XML details and editing, deletion, enable/disable controls, manual refresh, and automatic refresh after successful changes.
- Distinguish an empty/template FirewallRule XML response from a real missing or disabled WAN rule. The configuration audit reports that inventory is unavailable instead of presenting this condition as a WAN configuration failure.
- Distinguish fully empty FirewallRule templates from populated legacy records whose names were omitted by Sophos, preventing unsafe identification or updates of anonymous rules.
- When the SFOS 17.5 XML API returns only an empty FirewallRule template, load named User/Network and Business Application rules through the validated WebAdmin Controller inventory and detail requests. Later firmware families continue using their supported XML or REST capabilities.

## 1.3.72 - 2026-10-17

- Parse both conventional FirewallRule containers and legacy/alternate flattened rule records, detect Business Application rules from stable feature fields, and retain safe XML element paths for cross-version diagnostics.

## 1.3.71 - 2026-10-17

- Explain WAN enforcement audit failures with returned-rule counts, enabled/WAN/Business/blocked-client classification totals, per-rule rejection reasons, and the XML field names returned by Sophos in the application log.

## 1.3.70 - 2026-10-16

- Add an automatic WAN business-application Configuration Audit for the four required blocked-client groups.
- Add continuous post-block verification from Firewall Syslog events, persistent `ENFORCEMENT FAILURE` activity, collector metrics, and critical-alert email notification.
- Add a unified per-IP Timeline combining attacks, automatic membership changes, expirations, and enforcement failures.
- Coalesce short Syslog bursts and process the highest severity per source first, reducing duplicate Sophos API cycles and Critical blocking latency.
- Document the required `Blocked client networks` hardening for every WAN-to-LAN Business Application rule that publishes a service.
- Compile current Help during release builds and emit a versioned standalone CHM beside Setup for separate GitHub Release download.
- Check GitHub for updates every 10 minutes after startup, use conditional ETag requests when the latest Release is unchanged, and reduce the metadata-request timeout to 10 seconds.
- Back off failed background checks to 20, 40, and at most 60 minutes, then restore the 10-minute interval after a successful check.
- Show the automatic update prompt only once for each discovered version while retaining manual checks from About.

## 1.3.69 - 2026-10-14

- Add Live mode to the All, Critical, Major, and Moderate Threats tabs so their To timestamp advances to the current time on every 5-second auto refresh; manually changing To preserves a fixed historical range.
- Add exact From/To and category filters to application Logging with optional Live mode and multi-file newest-first results.
- Add configurable 14-365 day application-log retention under Manage > Config and immediately clean files older than the selected period.
- Record application startup, shutdown, total runtime, successful Sophos connections, disconnections, and exact connection duration in the diagnostic log.

## 1.3.68 - 2026-10-14

- Refresh Network interfaces and static routes together with gateway health every minute while connected.
- Give Threats Logs an explicit 60-second auto refresh while visible, with Live mode advancing To to the current time across midnight and a fixed-range option for historical review.
- Auto-refresh Expirations every 60 seconds while its tab is visible, reloading shared Rule state and recalculating remaining, expiring, and overdue membership values.
- Keep the Trends To timestamp live across midnight and advance it to the current time on each 30-second auto refresh while Live is enabled; retain a switchable fixed range for historical reports and vertically align the complete filter row.
- Widen and right-align the Home connection-setting labels so `REST API key (SFOS 22)` remains on one line.

## 1.3.67 - 2026-10-08

- Promote automatically managed IPs to the highest matching severity group, suppress lower-severity duplicates, and extend expiration when a stronger same-group Rule provides a longer duration without ever shortening an existing block.
- Record severity on timed memberships, show it in Expirations, migrate legacy records from their Rule or group name, and log promotion, suppression, extension, and cleanup failures explicitly.
- Protect the Home Password and SFOS 22 REST API key with Windows DPAPI for the current Windows user, omit both plain-text values from saved JSON, and automatically migrate legacy plain-text settings.
- Give all eight Home connection settings consistent vertical spacing, including the SFOS 22 REST API key row.
- Document that the REST API key is optional and used only for the SFOS 22 official REST capability probe.

## 1.3.66 - 2026-10-06

- Replaced the Threats Last days selector with exact From/To date-time filtering, initialized from the oldest stored event through the end of today.
- Added exact From/To date-time filtering to Windows-service Rule activity logs while retaining the newest 100 matches.
- Expanded Trends so selecting a day lists every attacking source IP with severity, counts, timestamps, signature, country, and current Sophos groups.
- Renamed Memberships / Expiring to Expirations and synchronized the application Help and GitHub documentation.

## 1.3.65 - 2026-10-06

- Automatically removed obsolete version folders from the in-app update cache while retaining the installed version, the update target or newest previous version, and active downloads.
- Added clickable daily details to the Threat Trends chart with exact Critical, Major, Moderate, Other, and total counts.
- Made application data grids consume their available width using proportional column fill sizing.
- Updated and recompiled the English CHM Help and synchronized both GitHub READMEs for version 1.3.65.

## 1.3.64 - 2026-10-06

- Added Expirations with current timed Rule memberships, remaining time, overdue entries, filters, and recent expiration outcomes.
- Added daily Critical, Major, Moderate, and other threat-event trend charts over a selectable 1-365 day period.
- Added complete per-IP attack and Rule-automation history on double-click from threat and membership tables.
- Added an explicit Target group prompt so selected threat IPs cannot be added until a real Sophos group is chosen.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.64.

## 1.3.63 - 2026-10-04

- Increased the Hosts import-source tab height and Browse/Download button height so both commands remain fully visible across Windows 10/11 DPI layouts.
- Made Setup explicitly close Manager and Widget processes before replacing files, including tray-hidden or asynchronously disconnecting instances that Windows Restart Manager leaves running.

## 1.3.62 - 2026-10-04

- Added firmware-family compatibility profiles and a capability matrix through SFOS 22, with automatic API-version selection and safe read-only probing for unknown firmware.
- Separated the official XML API, official SFOS 22 REST API, and versioned internal Web Admin adapters; the `mode=55` group rename protocol is now restricted to its validated SFOS 17.5 profile.
- Added SFOS 22 bearer-token REST support, full firmware-version discovery, and sanitized JSONL capture of internal Web Admin request metadata for diagnostics.
- Protected Sophos system hosts such as interface and built-in `#` objects from editing or deletion in both the UI and API layer.
- Applied deterministic Threat-row colors: severity colors in All and attack-count colors inside individual severity tabs.
- Combined the configured site name with the report title and date in daily summary, backup, and attack email headings.
- Auto-refresh gateway connectivity every minute, synchronize each refresh with the Widget, and optionally email when an existing gateway changes between connected and disconnected states.

## 1.3.61 - 2026-09-29

- Fixed direct IP host-group rename on SFOS 17.5 by initializing the Web Admin session, forwarding its CSRF token, accepting the asynchronous `202` success response, and retrying XML inventory verification until the transaction completes.
- Added an opt-in live rename round-trip test for validating the complete workflow against a configured firewall.

## 1.3.60 - 2026-09-28

- Fixed Web Admin Controller authentication in obfuscated builds so direct IP host-group rename works without `System.Text.Json` constructor-metadata errors.

## 1.3.59 - 2026-09-28

- Fixed IP host-group rename on legacy SFOS 17.5 by using the same object-aware Web Admin Controller operation as the firewall UI (`mode=55`), followed by XML inventory verification.

## 1.3.58 - 2026-09-28

- Use Sophos Firewall's native IP host-group update operation for direct rename, preserving members and policy references without creating or deleting a group.

## 1.3.57 - 2026-09-28

- Added MAC host-name entry and editing alongside MAC addresses, including double-click editing from the MAC inventory.
- Added safe MAC host rename with duplicate validation and automatic rollback when the old referenced object cannot be removed.
- Preserved UI Rule edits and group renames when the Threat Collector saves concurrent automation results.
- Prevented transient Rules-grid row-index errors while the grid is being rebound.

## 1.3.56 - 2026-09-28

- Added the API version, compatibility profile, and firewall time zone to the device footer in every email.
- Added a configurable daily-summary delivery hour from 00:00 through 23:00 under Manage > Email.
- Added safe IP host-group rename with Rule and timed-membership migration, plus group-list double-click editing.

## 1.3.55 - 2026-09-27

- Added an optional site heading under Manage > Email and include it as an HTML heading in every Manager and Threat Collector email, with the Sophos URL, reported model, and configured device address in the footer.

## 1.3.54 - 2026-09-27

- Fixed opening Manager from the startup Widget when no Manager window is running.
- Treat Windows service-control error 1056 as a successful Start when the collector is already running.

## 1.3.53 - 2026-09-27

- Split email notifications into independent Critical attack, daily summary, Rule failure, service/backup failure, and capacity-warning options.
- Preserve the previous combined operational-alert choice when upgrading from version 1.3.52.

## 1.3.52 - 2026-09-27

- Added correct implicit SSL/TLS SMTP support alongside STARTTLS and plain SMTP, plus email testing and optional delivery of verified FTP backup copies.
- Reconciled stored in-window threats automatically when the collector starts or automatic Rule definitions change.
- Added Excel-compatible export for Threat grids while preserving scroll position during automatic refresh.
- Added Host-name editing with safe membership-preserving rename behavior.
- Added IP-grid double-click editing and a confirmed red Delete action in the Edit IP host dialog.
- Vertically centered and aligned all controls in the shared Threat filter row.

This file summarizes distributed releases. SHA-256 values and downloadable installers are also available on the GitHub Releases page.

## 1.3.51 - 2026-09-26

- Recreate missing Critical.csv, Major.csv, and Moderate.csv automatic-block archives on service startup and every ten-second automation configuration refresh, including after users move or delete the files.
- Detect an already-running elevated Manager before requesting UAC, so launching the shortcut while Manager is minimized restores the existing window instead of starting another process or showing another elevation prompt.

## 1.3.50 - 2026-09-24

- Restore the Widget's Last backup card to date/time and backup type only; remote FTP file counts are no longer displayed or polled.
- Retry downloading a newly created FTP backup for up to two minutes when Sophos or the FTP server still has the file locked, and use a unique temporary local file for every copy attempt.
- Require Administrator approval before Manager starts; if Windows elevation cannot be obtained or the UAC request is cancelled, Manager exits without opening. Widget mode remains independent.
- Require an FTP password before an immediate FTP backup when Manager has no protected copy, so an accepted Sophos request is not knowingly sent without the credentials needed for the configured local archive copy.
- Add BlockedUntil to the Critical, Major, and Moderate CSV archives, using the exact expiry timestamp or Permanent and migrating older files with Unknown for historical rows.
- Keep Manage available for the entire connected session; temporary backup operations and backup-setting refreshes no longer disable the workspace.
- Move the Threats severity navigation above its filters and show Last days, Refresh, Target group, and Add only inside All and severity workspaces, not Rules or Logs.
- Sort every Threats inventory by Last seen descending by default and allow sorting in either direction from every column header.
- Reformat Home connection settings as seven full-height rows and keep Auto disconnect at a compact text-sized width.
- Protect the FTP password for the current Windows user after it is entered, allowing later FTP backup requests and status checks to create local archive copies without re-entering it each session.
- Backfill missing severity CSV rows from tracked active automatic Rule memberships without duplicating existing archive entries.
- Restore the CHM Contents navigation as the default left pane and correct its Rules, Logs, Config, and Email menu locations without redesigning the Help structure.

## 1.3.49 - 2026-09-19

- Archive successful automatic Rule additions in separate Critical, Major, and Moderate CSV files with the block time, source IP, Rule, and target group.
- Add configurable archive folders under Manage > Config, with Browse and Windows Explorer shortcuts, for automatic-block history and local FTP backup copies.
- Copy a newly created FTP backup from the remote FTP folder into the configured local archive when the FTP password is available in the current Manager session.
- Move Windows-service Rule activity from Manage to Threats > Logs, retaining Rule/IP search and time filters.
- Rename Manage > Service to Manage > Config and separate service controls from archive-folder configuration.
- Remove multiple selected IP memberships with one atomic IPHostGroup update instead of updating the group once per IP.
- Add Cancel to selected-IP removal; optional host-object deletion stops safely between API requests.
- Remove Base group name from Home and select the import target from the connected firewall's group list at the top of Hosts > IPs; lock the selector during automatic import while retaining Group capacity on Home.
- Give the import target selector a 40/60 label-to-list layout and correct the Browse and Download button sizing.
- Update English Help, README, and automated tests for the new behavior.

## 1.3.48 - 2026-09-19

- Check for new releases every hour while Manager remains open, without repeatedly prompting for a download.
- Show the installed version in the Manager window title and keep an update-available notice there until a later successful check finds no newer release.
- Refresh Sophos membership and all Threats severity tabs after each successful manual or service-side Rule addition.
- Filter Service activity by 24 hours, 7 days (default), 30 days, or all time; show at most the latest 100 matches and read large histories from the newest entries first.
- Preserve the existing membership duration when a matching IP already belongs to the Rule's target group; only a Rule that actually adds the IP creates an expiry.
- Expand English Help for automatic-Rule setup, safety limits, allowlists, stored-threat catch-up, activity filtering, and membership-duration behavior.

## 1.3.47 - 2026-09-18

- Allow multi-select removal of Hosts > Groups IPs, with a choice to remove only group membership or also delete host objects (subject to other Sophos references).
- Show per-IP progress, cancellation, and completion for Threats > Add selected IPs to group.
- Restore a secure, administrator-approved Manage > Service setup flow for automatic Rules. Test the Sophos XML API connection before storing machine-protected service credentials, without passing the password on the command line.
- Detect new automation settings while the collector runs and optionally evaluate already-stored matching threat events within each Rule's rolling window. Continue queued work after the per-minute change limit instead of dropping it.
- Track group membership separately for overlapping automatic Rules, preventing duplicate additions and premature expiry removal.
- Include automatic no-op checks in Service activity when an IP is already managed or already in the target group, so service execution remains visible even when no Sophos change is needed.

## 1.3.46 - 2026-09-17

- Show an informational Rule preview without an Apply prompt when every matching IP already belongs to the target group; distinguish the Rule's rolling window from the Threats tab's Last days filter.
- Clarify in Manage > Service that the Last report is historical and that the activity grid records service-side Rule actions only, not manual Apply; explain why it is empty without automation credentials.
- Add Order to the Rule editor for creation, editing, and duplication; center Rule dialogs over Manager and use the application icon for Apply progress.
- Move Rules to the last Threats subtab and give users Move up / Move down controls for execution priority; the collector evaluates automatic Rules in the same saved order.
- Move SMTP settings from Manage > Service to a separate Manage > Email subtab. Email Rules and email sending are not implemented yet.
- Prevent concurrent collector status writes from contending for the same temporary filename.
- Update English Help and README for the new workspace layout.

## 1.3.45 - 2026-09-17

- Show service-reported automation readiness and a searchable per-IP activity history in Manage > Service, including additions, expiry dates, removal results, and failures. Keep the Windows service and email settings in two sections of the same Service subtab.
- Save SMTP host, port, encryption, authentication, sender, reply-to, default recipients, and timeout for future email features; protect the password with Windows DPAPI for the current user. This does not send email yet.
- Show a live per-IP progress window during manual Rule Apply, allow cancellation between IP operations, and replace Cancel with OK when finished.
- Refresh the Rules grid while open so Last run changes made by the Windows service become visible without leaving the tab.
- Updated the English CHM Help, source and release READMEs, and build documentation for version 1.3.45.

## 1.3.44 - 2026-09-17

- Opening Threats from the Widget selects a one-day window and triggers the same Refresh action as the Threats button.
- Simplify Manage > Service by removing the three automation information/control rows and placing the four collector-service buttons below its status.
- Clarify that automatic Rules keep running after Manager closes only when the collector service is running and its separate automation credentials were previously configured and remain unpaused. The hidden setup controls mean a fresh installation cannot currently enable service-side automation by checking the Rule option alone.
- Updated the English CHM Help, source and release READMEs, and build documentation for version 1.3.44.

## 1.3.43 - 2026-09-17

- Read the connected firewall's configured time zone through the XML API on each connection and use its calendar date for Threats and Widget day filters, with a fallback when the API does not report a usable zone.
- Show attack-event counts in every Threats tab, matching the Widget and Sophos Reports; keep the table grouped by source IP and show both event and unique-IP totals in the footer.
- Updated the English CHM Help, source and release READMEs, and build documentation for version 1.3.43.

## 1.3.42 - 2026-09-17

- Repair existing Automation files' ACLs during Setup, so stale explicit permissions cannot block elevated Manager access to threat rules after an upgrade.
- Store shared Rules separately from protected service credentials so a normal Manager session can enable and edit automatic Rules used by the collector. Migrate existing shared Rules during Setup or service startup; fall back to personal manual Rules only if the shared Rules directory is unavailable.
- Updated the English CHM Help, source and release READMEs, and build documentation for version 1.3.42.

## 1.3.41 - 2026-09-16

- Keep the Sophos connection active when protected Rule storage is inaccessible; disable Rule and automation actions with a clear repair message instead of failing Connect.
- Make window-placement JSON serialization resilient to release obfuscation by using a parameterless placement model.
- Added a Rules-footer button that requests UAC elevation, waits for the current Manager process to exit, then starts a fresh elevated instance instead of reopening the old one.
- Updated the English CHM Help, source and release READMEs, and build documentation for version 1.3.41.

## 1.3.40 - 2026-09-16

- Split the Threat IP inventory into All, Critical, Major, Moderate, and dynamically discovered historical severity tabs, including empty standard tabs.
- Moved Threat Collector Windows service status and controls from Threats to the Manage > Service subtab.
- Added opt-in Windows-service execution for threat rules, with event-driven evaluation, IP/severity deduplication, encrypted machine-scoped credentials, configurable allowlists and per-minute change limits.
- Added automatic membership expiration maintenance, audit JSONL history, three-failure automatic pause, connection testing, and Pause/Resume controls under Manage > Service.
- Migrated the Threat Collector to a self-contained .NET 10 Windows service so it can reuse the guarded Sophos API and rule-evaluation implementations.
- Updated all solution projects to .NET 10 for Visual Studio 2026, refreshed stable NuGet packages and test tooling, and replaced a vulnerable transitive cryptography package.
- Moved shared threat rules to ProgramData with automatic migration from the previous per-user file and cross-process file locking.
- Restricted the shared Automation directory to Administrators and SYSTEM; Manager disables Rules and automation settings when it is not elevated.
- Updated the English CHM Help, source and release READMEs, and build documentation for version 1.3.40.

## 1.3.39 - 2026-09-15

- Fixed Threats and Widget calendar-day filtering when Sophos emits Iran's former `+04:30` offset while Windows uses the current `+03:30` offset.
- Preserve the calendar date carried by Sophos events instead of converting them across offsets, so qualifying Major, Critical, and Moderate events remain visible under the correct day.
- Added automated coverage for same-date and previous-date Sophos events with differing UTC offsets.
- Removed the obsolete release-repository `version.json`; the updater uses the authoritative GitHub Releases API and its latest release asset metadata.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.39.

## 1.3.38 - 2026-09-14

- Made the Threat Collector stop phase mandatory before Setup replaces files during upgrade or repair.
- Setup now waits for the installed service to stop and aborts safely with actionable guidance if the stop command fails; an already stopped service remains valid.
- The upgraded service is reconfigured for Automatic startup and started after the new files and UDP 514 firewall rule are installed.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.38.

## 1.3.37 - 2026-09-14

- Fixed Rules actions using the first grid row when another rule remained visibly selected after the grid was refreshed.
- Restore the selected Rule and its current cell consistently after add, edit, duplicate, enable/disable, delete, preview, or apply refreshes.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.37.

## 1.3.36 - 2026-09-13

- Added legacy SFOS IPS severity support by mapping `rule_priority` values to Critical, Major, and Moderate when explicit detection severity is unavailable.
- Fixed the threat-rule window-unit selector so the saved minute, hour, or day value is selected and applied reliably.
- Added a detailed no-match diagnostic to Rule preview, including severity totals inside the selected rolling window and whether the attack threshold was reached.
- Clarified the administrator and Threat Collector service-restart steps required during an upgrade.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.36.

## 1.3.35 - 2026-09-09

- Added an interface-configuration fallback for firewalls that recognize gateway API entities but return no gateway rows.
- Changed automatic gateway status refresh from every 30 seconds to every hour to reduce XML API traffic.
- Preserve the last known Network and Widget gateway state when an automatic refresh returns no gateways, and record a warning for diagnostics.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.35.

## 1.3.34 - 2026-09-09

- Added a focused Sophos XML API gateway-status query with `GatewayHost` / `Gateway` compatibility fallback.
- Refresh gateway health automatically every 30 seconds while connected, updating both the Network > Gateways table and Widget state without reloading interfaces or routes.
- Prevent overlapping automatic gateway refreshes and pause them while disconnected or while another Network operation is running.
- Log background refresh failures as warnings without interrupting the active Manager session.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.34.

## 1.3.33 - 2026-09-08

- Removed the separate Threat Collector card from the Widget to make the window shorter and more compact.
- Integrated collector health into the Threats card: when the Windows service is stopped, the card now shows `Service is not running` in red instead of presenting a potentially misleading threat count.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.33.

## 1.3.32 - 2026-09-08

- Made every Widget status card open Manager directly at its relevant destination: Home, Network > Gateways, Manage > Backup / Restore, or Threats.
- Added cross-process section-navigation events and matching Manager command-line switches while preserving single-instance restore behavior.
- Isolated Widget smoke-test synchronization objects so release validation cannot interfere with a normally running Widget.
- Added an embedded multi-resolution Widget icon and dedicated uninstall icon generated during release builds.
- Reorganized Start Menu shortcuts under a Sophos Security Assistant folder, assigned the Widget icon to Widget shortcuts, and removed the obsolete Widget desktop-shortcut option and legacy shortcuts during upgrades.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.32.

## 1.3.31 - 2026-09-06

- Split Manage into Backup / Restore, Device Power, and Rules subtabs.
- Added locally persisted threat-rule management with a 10-rule limit, severity and rolling time-window conditions, target groups, and permanent or expiring memberships.
- Added rule preview and manual apply while connected, public IPv4 filtering, reuse of existing Host objects, preservation of existing memberships, and expiration coordination across overlapping rules.
- Added automated tests for threshold, severity, time-window, membership, and private-address evaluation.
- Changed the Widget threat card to show threats from the current local calendar day and color it by the highest severity found.
- Made a second Manager launch restore the existing Manager window instead of displaying an already-running message.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.31.

## 1.3.30 - 2026-09-03

- Changed the Threats `Last days` filter to calendar-day ranges matching Sophos reports: one day begins at local midnight today, and larger values include that many calendar dates.
- Added automated tests for one-day, multi-day, and invalid Threat calendar windows.
- Redesigned Home as a compact dashboard with icon actions for About, Help, Widget, Web Admin, Save Settings, and Connect/Disconnect, plus a dedicated status row and cleaner system information layout.
- Moved update-check and initial-load progress messages into the Home status area instead of reserving a separate progress row.
- Added Manager notification-area support: minimizing hides Manager to the tray while keeping it running and connected, with double-click and Show Manager restore actions and an explicit Exit command.
- Made Widget restore an already-running Manager that is hidden in the tray instead of launching another instance, and distinguish Manager visibility from process existence.
- Added a dedicated high-contrast Widget window and tray icon plus an explicit close control while preserving minimize-to-tray behavior.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.30.

## 1.3.25 - 2026-09-03

- Added the embedded Widget assembly to the release obfuscation set so all first-party application code is protected consistently.
- Made smoke-test mode surface unhandled Windows Forms startup errors directly to the release builder instead of allowing interactive UI handling to hide them.
- Run the packaged Widget with smoke-test mode enabled, strengthening the release gate for both Manager and Widget startup paths.
- Revalidated that Setup and Manager use the same high-contrast icon and updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.25.

## 1.3.24 - 2026-09-03

- Replaced the Setup executable icon with the same high-contrast icon embedded in Sophos Security Assistant.
- Consolidated the desktop Widget into the main executable and launch it independently with `--widget`, eliminating the duplicate self-contained Widget runtime while preserving its separate process lifetime.
- Reworked Manager/Widget Open and Close coordination to use a named mutex and close event instead of process-name and window-message assumptions.
- Added a compact Gateway status card to the Widget, including disconnected-gateway highlighting, new failure notifications, and click-through to Manager.
- Persisted the latest connected gateway snapshot atomically for the Widget and clear its connected state when Manager disconnects.
- Made the release builder smoke-test both Manager and Widget modes and made Setup remove the obsolete standalone `Widget` directory during upgrades.
- Updated the English CHM Help, source README, release-repository README, and build documentation for version 1.3.24.

## 1.3.23 - 2026-09-02

- Distinguished explicit Sophos detection severity from Syslog transport priority, mapped IPS `Warning` priority to Moderate, and normalized compatible legacy IPS records that had previously appeared as Major.
- Added severity-source metadata to stored threats and improved the Threats collector report to show total stored events, unique source IPs, current-service accepted events, and the actual latest stored threat time.
- Changed the Manager and Widget launcher actions into synchronized Open/Close controls that follow the other process state.
- Color-coded Widget backup age as green through 10 days, amber through 30 days, and red when older or unavailable.
- Made Manager-to-Widget heartbeat writes atomic and tolerant of transient file sharing or access errors, and allowed safe concurrent heartbeat reads.
- Renamed the disabled inactivity option from `Off` to the clearer `Never disconnect`.
- Synchronized the release-repository landing page with version 1.3.23 and expanded Help with requirements, installation, updater verification, service lifecycle, and collector data-location details.

## 1.3.21 - 2026-09-01

- Made Manager and Widget backup-state JSON deserialization reliable after release obfuscation by using stable public properties and a parameterless constructor.
- Kept a successful Sophos backup result successful when writing or refreshing the optional local Widget history fails; the local-history error is logged separately.

## 1.3.20 - 2026-09-01

- Moved Refresh to the end of the search row in Groups, MAC, and FQDN; refreshing now clears the search text before reloading Sophos data.
- Added a membership filter to the FQDN inventory and Edit Selected actions for IP, MAC, and FQDN host objects.
- Added single-address and MAC-list creation/editing with normalization, duplicate detection, and input validation.
- Added a standalone Windows desktop widget with independent process lifetime, Manager/Widget launch shortcuts, single-instance protection, tray controls, connection/service status, backup history, and new-threat notifications.
- Added installer options for a Widget desktop shortcut, starting the Widget with Windows, and launching it after Setup.
- Persisted the timestamp and type of each successful in-app backup request for the desktop widget and Manage status area.
- Changed the widget to reload backup state every 10 seconds and show the backup type; FTP backups also show the remote folder file count when session credentials are available.
- Corrected backup tracking so applying backup settings is no longer recorded as a successful backup.

## 1.3.16 - 2026-09-01

- Added live search to MAC and FQDN inventories, matching object names, addresses, descriptions, and group membership where applicable.
- Added preflight checks that reject duplicate MAC host names and MAC addresses before sending a create request to Sophos.

## 1.3.15 - 2026-09-01

- Renamed the IP Management workspace to Hosts and added MAC and FQDN subtabs after Groups.
- Added Sophos MAC-host inventory, creation, and deletion through the XML API.
- Added FQDN `ALL` and `DUPLICATE` views, real Sophos FQDN groups, group creation, and independent/grouped FQDN creation. Full URLs are accepted and normalized to the hostname required by Sophos.
- Added safe removal of an FQDN from a group while preserving the object, and guarded deletion of independent FQDN objects.
- Expanded the English Microsoft Compiled HTML Help for the renamed Hosts workspace and its IPs, Groups, MAC, and FQDN subtabs.
- Improved Threat Collector compatibility with Sophos IDP/Anomaly/Signatures events, legacy date/time/timezone fields, signature messages, and alternate source-country fields.

## 1.3.10 - 2026-08-29

- Added an `Open Web Admin` button on Home beside Verify SSL certificate. It validates the currently entered host/IP and HTTPS port and opens the Sophos Web Admin login in the default browser without requiring the settings to be saved first.
- Set Auto disconnect to 15 minutes by default and vertically aligned its selector with the Home-page label.
- Enabled Moderate threats by default, fixed the clipped Moderate and wrapped Last days labels, documented the five-second local auto-refresh, and added Sophos group-membership detection for exact IP hosts and containing CIDR network objects. Manual Refresh now reloads group inventory from Sophos while periodic refresh avoids unnecessary API traffic.
- Corrected collector diagnostics so non-IPS/ATP messages without a source field are counted as non-threat logs rather than misleading Missing source IP results.
- Added an English Microsoft Compiled HTML Help (`.chm`) file opened from the Home page.
- Added categorized contents, index, full-text search, XML API and Syslog setup, and detailed Home, IP Management, Network, Threats, Manage, Logging, and troubleshooting topics.
- Documented Home group creation and inactivity options, Manage backup behavior, and the 14-file daily application-log retention policy.

## 1.3.0 - 2026-08-29

- Added the Threats workspace with Critical, Major, and optional Moderate filters.
- Added the continuously running `SophosSecurityAssistantThreatCollector` Windows service on UDP 514.
- Added service state, uptime, Start/Restart/Stop controls, and Windows Services access.
- Added Syslog validation for the local target IP, port, IPS/ATP selections, and severity threshold.
- Added collector reporting for received, saved, ignored, and rejected messages with rejection categories and activity timestamps.
- Added grouping of threat events by public source IP and adding selected IPs to an existing Sophos group.
- Added Moderate mappings for common Sophos values including Medium, Information, Informational, Info, Notice, and Notification.
- Added support for common alternate Sophos Syslog field names and Intrusion Prevention component names.
- Added installer creation, upgrade restart, removal, and Windows Firewall handling for the collector service.
- Added sequential initial loading and Home progress reporting for IP Management, Network, Threats, and Manage.
- Added Sophos Syslog configuration warnings without producing a definitive false warning when the XML API cannot verify settings.
- Rebalanced the Threat IP and collector-report tables and removed duplicate status text.
- Added a complete repository README covering configuration, features, data locations, and limitations.

## 1.2.74 - 2026-08-27

- Renamed Objects to IP Management.
- Kept IP Management, Network, and Manage disabled until initial Sophos data loaded successfully.
- Continued loading independent sections when one request failed.
- Added initial loading progress on Home.
- Applied the application icon consistently to the main window and dialogs.
- Added Open FTP location for the configured backup server/path without exposing credentials.
- Placed FTP destination and credential pairs on compact shared rows.

## 1.2.73 - 2026-08-27

- Replaced MaterialSkin with compact standard Windows controls to prevent clipping and unnecessary scrolling.
- Added larger color-coded tabs with a distinct active state.
- Improved Home, IP import, Backup, Interface, Gateway, and Routing layouts.
- Stacked backup actions and grouped related backup/FTP fields.
- Made the Routing grid fill the available width.
- Fixed Pause and Cancel clipping in the update dialog.

## 1.2.72 - 2026-08-27

- Loaded existing Sophos backup configuration into the application.
- Applied Local, Email, and FTP backup modes and scheduling through the XML API.
- Preserved stored Sophos passwords unless replacements were entered.
- Improved Home and Network dialog layouts and reduced unnecessary scrolling.

## 1.2.71 - 2026-08-26

- Made the main window resizable, minimizable, and maximizable with a safe minimum size.
- Restored the last valid position, size, and maximized state.
- Centered update downloads over the main window and added Pause/Resume and Cancel.
- Added a direct GitHub installer link after failed in-app download or verification.

## 1.2.70 - 2026-08-26

- Introduced Google Material styling (later removed in 1.2.73 after layout testing).
- Added interface, gateway, and static-route inventory and supported create/edit/delete operations.
- Added validated interface, zone, netmask, assignment, and IP-family selections.
- Added gateway health highlighting and interface-managed gateway protection.
- Corrected route handling so SFOS routes do not require the Web Admin-only Name field.

## 1.2.67 - 2026-08-26

- Added individual IPv4 network objects in CIDR notation to group management.
- Normalized network addresses and confirmed when host bits were supplied.
- Displayed and sorted network objects using canonical CIDR notation.
- Corrected the Home Password label layout.

## 1.2.66 - 2026-08-25

- Fixed the Home credentials row so Password and Show remain visible.
- Embedded startup update status in Home instead of a separate window.
- Disabled controls during the initial update check and restored their states afterward.

## 1.2.65 - 2026-08-25

- Added visible startup update activity with a bounded network wait.
- Compacted the Home Host/Port and Username/Password layouts.
- Added TLS 1.2/1.3, Windows proxy support, and controlled installer-download retries.
- Replaced the floating update overlay with an in-application progress dialog.

## 1.2.6 - 2026-08-25

- Added configurable automatic disconnect after inactivity.
- Added safe IP host-group creation.
- Added sortable host/IP/group columns and `# ALL`/`# DUPLICATES` views.
- Improved group search, startup centering, update progress, and update-decline warnings.
- Improved XML request construction and logging stability.

## 1.2.5 - 2026-08-22

- Disabled Save Settings during connection attempts and restored it after failure/disconnect.
- Distinguished API/source-not-allowed, authentication, TLS, timeout, and network failures.
- Added guidance for enabling API Configuration and allowing the client IP, with Web Admin access.
- Aligned Base group name and Group capacity on one row.

## Earlier development milestones

- **1.2.7:** introduced the first Material-based network-management build; it was superseded by 1.2.70 to preserve correct numeric update ordering from 1.2.67.
- **1.2.4:** refined updater progress behavior and release metadata.
- **1.2.3:** established the guarded IP import/group workflow, compatibility profiles, update service, checkpoint/rollback support, installer pipeline, obfuscation, and initial automated tests. These milestones were superseded before the public release series shown above.
