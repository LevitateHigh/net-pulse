# Architecture

## Chosen direction

Net-Pulse will be a native, local-first Android application. It has two
observation modes behind one common scan model:

1. **Direct phone observation (MVP):** the Android phone performs intentional
   scans from its current network position.
2. **Optional home observation points (future):** owner-approved home-side
   observers may later supply results from zones that a phone cannot reach.

The second mode is intentionally not an MVP implementation commitment. It is a
necessary extension point because an Android phone cannot reliably discover
devices behind every routed/NAT-isolated home zone from every location.

## System shape

```text
Android UI
  └─ presentation / view models
       └─ application use cases
            ├─ Home & Zone management
            ├─ Device Registry
            ├─ Scan orchestration
            ├─ Port diagnostics
            └─ CSV export
                 ├─ domain model and policies
                 ├─ local database and export files
                 └─ observation adapters
                      ├─ Android direct scanner (MVP)
                      └─ Home observer adapter (future)
```

## Android application

- **Language and UI:** Kotlin with Jetpack Compose.
- **Organization:** presentation, application/use-case, domain, and data/
  infrastructure layers. Networking and storage stay behind interfaces so that
  UI and core rules do not depend on one scan mechanism.
- **Storage:** an app-private local database stores the Home, zones, device
  records, observations, scan runs, port results, and audit/event history.
  The implementation must use Android Keystore-backed protection appropriate
  to the selected database approach and exclude monitoring data from automatic
  device backup.
- **Export:** a user-initiated export service creates related CSV files using
  Android's user-visible document/share flow. Export files are never written to
  Git-managed project paths.
- **Permissions:** request only what a feature needs. Local-network access must
  be handled as a runtime permission on Android versions that require it; denial
  produces a clear coverage error rather than a misleading empty scan.

## Scan model

Every scan produces a durable Scan Run with:

- requested mode: Fast, Deep, or targeted port scan;
- requesting zone/scan origin;
- requested targets and profile;
- per-zone coverage result;
- individual device observations and evidence;
- elapsed time and errors.

Fast Scan is conservative discovery. Deep Scan invokes only the owner-selected
profile. Targeted TCP diagnostics use standard connection attempts and record
open, closed, filtered/no response, unreachable, and not-scanned outcomes.

## Multi-zone truth model

The UI never equates a configured zone with an observable zone.

```text
Configured zone → scan attempt → coverage result
                                  ├─ observed: update device status
                                  └─ not observed: mark coverage unknown,
                                                    do not mark devices absent
```

For the MVP, the direct phone scanner may cover only the local zone and any
other routes the current network genuinely permits. A future home observer is
placed only by the owner in an authorized zone and sends results to the phone
over the local network; no cloud is required. Router/NAT traversal is never
assumed.

## Security boundaries

- No credentials are collected or stored in the MVP.
- The target allow-list is derived from owner-configured zones.
- The app has no capability to modify networking equipment or block clients.
- Deep scans and port ranges require explicit owner action and retain a history
  of what was requested.

## Testing implications for the next session

Implementation testing starts with an emulator for UI, storage, filters, CSV,
and deterministic simulated scan results. It then moves to the owner's Android
phone and only the owner's registered home zones for permission, reachability,
and coverage testing.
