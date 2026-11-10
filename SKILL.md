---
name: external-api-contracts
description: Use when integrating or reviewing external REST APIs or WebSocket feeds, investigating provider schema drift, or building contract fixtures and replay tests for missing, duplicate, stale or out-of-order events.
---

# External API contracts

Inspect the actual adapter, schemas, provider documentation and existing tests. Separate the provider's wire format from the application's normalized model. A passing test against an invented response proves neither provider compatibility nor live availability.

## Establish evidence

Prefer existing approved captures and documented sandbox endpoints. Record provider, endpoint/event type, capture date, API/schema version if known, and provenance. State when only documentation or synthetic samples are available. Fetching production data or writing to a provider requires the user's existing authorization; do not initiate writes for contract discovery.

Before persisting or publishing a fixture, remove authorization headers, cookies, signed URLs, query credentials, personal data and sensitive identifiers, including nested/free-text/error fields. Use synthetic replacements while preserving types, precision, relationships and event ordering. Keep raw private captures outside version control; do not publish them. Review the entire proposed diff and history before publication. Public fixtures must be synthetic or explicitly approved sanitized examples. Mark synthesized values and provenance honestly.

## Verify the boundary

Compare actual payloads with the parser: required versus optional versus null, added fields, enum changes, numeric strings, decimal precision, timestamp units/timezones, pagination and error envelopes. A number-to-string change requires an explicit compatibility decision, not silent coercion. Preserve exact money/quantity semantics with the project's existing decimal representation. Avoid logging rejected payloads containing secrets.

Replay fixtures through the real adapter and assert normalized values, meaningful errors and application effects. Keep transport fakes separate from parser tests; mock success alone cannot establish integration correctness. Validate only fields whose semantics matter, tolerating documented additive changes as appropriate.

## Stateful feeds

For reconnects, duplicates, missing events and reordered messages, inspect the provider's sequence/version/snapshot guarantees. Replay the relevant cases and assert that stale events cannot overwrite newer state, duplicates cannot double-count effects, and gaps trigger the existing reconciliation path. Do not assume timestamps establish a total order or that a feed supports gap-free replay. If identifiers or recovery guarantees are absent, explicitly report that limit and choose the smallest supported reconciliation strategy.

## Report

Identify which contract changed, which adapter behavior was checked, fixture provenance, and remaining live checks. Distinguish offline replay, sandbox integration and production verification. Use the existing tests and libraries; this skill does not require a new schema framework, polling service or dependency.
