# Requirements

## Scope and assumptions

- Net-Pulse is a personal Android app for networks the owner administers.
- It must support a simple single-router home and a home with multiple routed
  zones.
- Zone names and all addressing/routing notes are owner-configurable; example
  names are not product constants.
- The app observes and documents a network. It does not change DHCP, routes,
  firewall rules, router configuration, or device configuration.

## Network model

1. The owner can create a Home containing one or more Network Zones.
2. A zone has a custom name, purpose, one or more address ranges, one or more
   gateways, routing notes, and an enabled/disabled state for whole-home scans.
3. The owner can add, edit, disable, or archive zones without losing historic
   device or scan data.
4. A whole-home scan attempts every enabled zone and reports coverage for every
   zone independently: reachable, partially reachable, unreachable, or unknown.
5. Routing details describe expected paths; they never create or alter network
   routes.

## Device Registry

1. Net-Pulse keeps a persistent Device Registry rather than a disposable scan
   list.
2. A record contains, when known: owner-assigned name, owner, device type,
   model, zone, IP address history, MAC address history, manufacturer, hostname,
   observed services, status, first seen, last seen, and user notes.
3. Device type supports common home categories such as IP camera, TV, tablet,
   phone, IoT switch, router, access point, printer, and custom types.
4. The app may suggest a type/model, but suggestions must identify their source
   and remain editable by the owner.
5. The registry can be filtered together by zone, owner, type, and status.
6. The owner can merge duplicate records, including records created when a
   device changes or randomizes its MAC address.

## Discovery and status

1. Fast Scan is the primary, on-demand whole-home scan.
2. A fast scan discovers reachable devices and updates registry evidence,
   addresses, zone association, and observation status.
3. New discoveries are marked **New** in results and in the registry; the MVP
   does not send automatic notifications.
4. A known device progresses through these meanings:
   - **Known/seen:** observed successfully.
   - **Checking absence:** a previous device was missed and requires
     confirmation.
   - **Not currently observed:** missed after the configured confirmation rule
     during successful coverage of its zone.
   - **Coverage unknown:** its zone could not be successfully observed; this is
     not an offline assertion.
   - **Archived:** owner action only; history is retained.
5. A device becoming unobservable never deletes its record.

## Diagnostics

1. Deep Scan is an explicit, advanced action and is never the default scan.
2. Deep Scan uses a configurable profile to collect richer identification and
   service information from enabled zones and reachable devices.
3. The owner can run an individual TCP port scan against one device or an
   owner-selected host range in registered home zones.
4. The owner can select one port, many ports, or a port range.
5. Port results include target, scan origin/zone, timestamp, duration, exact
   scope, port/protocol, state, inferred or identified service, optional
   response time, and optional voluntarily returned banner/version information.
6. Port states must distinguish at least open, closed, filtered, unreachable,
   and not scanned. The app must not treat a lack of response as closed.
7. TCP is the dependable MVP protocol. UDP scanning and vulnerability assessment
   are deferred.
8. Diagnostics are limited to explicitly registered home zones and never perform
   exploitation or intrusive vulnerability actions.

## Exports and privacy

1. Data remains in private app storage on the owner's phone by default.
2. The MVP has no account, cloud sync, remote upload, or automatic monitoring
   notifications.
3. Monitoring data is excluded from automatic device backup; backup is a future
   explicit feature rather than an implicit data export.
4. The owner can manually export complete data as CSV files. A complete export
   preserves deep-scan details and history rather than flattening them away.
5. A complete export contains related CSV files for devices, zones, scan
   history, port results, and device events.
6. Exports preserve timestamps and the evidence/confidence of inferred versus
   verified details.
7. Live monitoring data, exports, credentials, and device identities must not
   be committed to the source repository.
