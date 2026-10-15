# Developer API Dependencies

This frontend currently documents public price, health, and WebSocket endpoints.
It has no API-key management, request-activity, quota, replay, or feed-schema
compatibility endpoints. The entries below record the backend contracts needed
before the corresponding user-facing features can be implemented. They are
requirements, not claims that those endpoints or behaviors exist.

## Feed-schema compatibility before upgrades (#803)

**Status:** Blocked on backend schema/version compatibility data.

The published OpenAPI document describes one current API schema and has no
feed-schema version history or compatibility results. Before this frontend can
show whether a client upgrade is safe, the backend must provide versioned
schemas (or an equivalent compatibility check) for the current feed and the
proposed client version. A result must identify both versions, state whether
they are compatible, and describe any breaking changes. Unknown versions and
unavailable or stale results must be distinguishable from a successful
compatibility check. The frontend must not infer compatibility from the
current schema alone or initiate an upgrade automatically.

## Read-only request replay (#804)

**Status:** Blocked on a persisted diagnostics record and a server-enforced
read-only replay operation.

The frontend has no diagnostics view or request history endpoint. The backend
must provide an authenticated, owner-scoped way to select a recorded request
and replay it under a server-enforced read-only policy. Results must identify
success or failure and expose only a safe response preview and relevant
diagnostic metadata. Credentials, signing material, and other sensitive
headers or values must be excluded or redacted; the client must not replay
arbitrary user-supplied requests or rely on a UI-only read-only restriction.
The contract must distinguish unavailable records and replay errors.
