# Net-Pulse vision

## Product statement

Net-Pulse is a personal Android app that makes a home's network understandable:
it discovers devices across configured network zones, maintains a useful device
registry, shows meaningful change, and provides intentional diagnostics without
requiring a cloud account.

## Who it is for

The initial user is the technically capable owner/administrator of one home
network. The app must also be understandable for a future owner whose home has
only one router and one subnet.

## Problems it solves

- Knowing what devices are on the home network and where they belong.
- Recognizing new, known, missing, and currently unobservable devices without
  deleting history.
- Investigating a device with an explicit TCP port scan.
- Understanding what parts of a segmented home network were actually observed.
- Exporting the owner's network information for personal analysis.

## Product principles

- **Truthful coverage.** A device is never reported absent merely because its
  zone could not be scanned.
- **Local by default.** Device names, owners, addresses, history, and exports
  remain on the owner's phone unless the owner explicitly exports them.
- **User-owned context.** The owner can name devices and define zones, gateways,
  and routing notes in language that matches the home.
- **Intentional diagnostics.** Deeper and port scans are initiated by the owner,
  scoped to registered home networks, and never attempt exploitation.
- **Works from simple to segmented.** One-router homes stay simple; advanced
  homes can model multiple routed zones without losing their policy boundaries.

## Future direction, not MVP scope

Continuous monitoring from home-side observers, notifications, household
presence inference, router management, bandwidth management, cloud sync, and
automatic remediation may be evaluated after the MVP proves useful.
