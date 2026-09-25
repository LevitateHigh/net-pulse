# Architecture and product decisions

## D-001: Local-first personal MVP

**Decision:** Keep all registry and scan data in private Android app storage.
Provide manual CSV export only and exclude monitoring data from automatic device
backup.

**Why:** The first version is a personal exploration tool. This avoids account,
cloud, remote-access, and data-handling complexity.

## D-002: Configurable Home and Network Zones

**Decision:** Model a Home as one or more owner-configured Network Zones with
names, address ranges, gateways, and routing notes.

**Why:** The app must fit both simple homes and segmented/routed homes. Example
zone names and address ranges are not baked into the app.

## D-003: Coverage is a first-class result

**Decision:** Report observation coverage per zone and never infer that an
unscanned zone's devices are offline.

**Why:** A phone cannot necessarily observe devices across routed, NAT-isolated,
or otherwise restricted zones.

## D-004: Persistent Device Registry

**Decision:** Keep devices and history persistently. New discoveries are marked
New; missing devices become Not currently observed only after confirmation;
removal is a manual archive action.

**Why:** Scan misses and temporary network changes must not destroy useful
history or create false alerts.

## D-005: Fast Scan first, explicit diagnostics second

**Decision:** Fast Scan is the default. Deep Scan and targeted TCP port scans
are explicit owner actions.

**Why:** This keeps normal use quick and predictable while allowing deliberate
diagnostics without default exhaustive scanning.

## D-006: No control-plane features in the MVP

**Decision:** The MVP observes and exports. It does not manage routers, block
devices, shape bandwidth, change routes, or modify firewall/DHCP settings.

**Why:** Existing router policy remains under the owner's control and is outside
the first build's safety and integration scope.

## D-007: Future observation-point extension

**Decision:** Keep the scan model capable of accepting results from
owner-approved home-side observers later, while implementing only direct phone
observation in the MVP.

**Why:** Whole-home certainty in segmented networks requires visibility from
each relevant network path; it cannot be guaranteed from a single phone.
