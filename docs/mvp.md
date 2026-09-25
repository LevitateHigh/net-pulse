# MVP

## Goal

Prove that a personal Android app can give an owner a trustworthy, useful view
of a configurable home network while keeping data on the phone.

## Included

### Home and zones

- Create, edit, enable/disable, and archive owner-named network zones.
- Record address ranges, gateways, purpose, and routing notes for every zone.
- Run Fast Scan across enabled zones and show a per-zone coverage outcome.

### Device Registry

- Persist devices across scans.
- Show and edit name, owner, type, model, zone, status, observed addresses,
  manufacturer, hostname, and last-seen information.
- Mark new discoveries in the results and registry.
- Filter by zone, owner, type, and status.
- Preserve history and permit owner-directed record merging and archiving.

### Diagnostics

- Fast Scan as the default action.
- Explicit Deep Scan using a configurable, non-exhaustive profile.
- Explicit targeted TCP port scans for one device or an owner-selected range and
  port selection.
- Show clear port state, service information, scope, timing, and scan origin.

### Export

- Manual complete CSV export of devices, zones, scan history, port results, and
  device events, including available deep-scan details.

### Privacy and safety

- Single personal user; no sign-in.
- Phone-local data only.
- Monitoring data excluded from automatic device backup.
- Scans only target owner-configured home zones.
- No router changes, bandwidth controls, blocking, exploitation, or automatic
  remediation.

## Explicitly deferred

- Always-on monitoring, background alerts, and push notifications.
- Household presence inference.
- Router/API integrations, device blocking, parental controls, and bandwidth
  management.
- Guaranteed discovery across routed or NAT-isolated zones.
- UDP scanning, vulnerability assessment, and external/public-IP scanning.
- Cloud sync, remote access, multi-user sharing, and automatic backups.

## MVP acceptance criteria

1. A one-router user can configure or confirm a zone, run Fast Scan, and keep a
   useful local device registry.
2. A multi-zone user can represent each zone, run a whole-home scan attempt, and
   see exact coverage instead of false absence claims.
3. A new device is visibly marked New; an earlier record is never silently
   deleted because it was missed.
4. An owner can investigate a selected registered target with a TCP port scan.
5. An owner can export all retained data and deep-scan results as CSV.
