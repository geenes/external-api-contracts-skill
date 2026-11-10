# External API contracts skill

A Codex skill for external REST/WebSocket compatibility: wire schemas, exact decimal values, sanitized fixture provenance and stateful feed replay.

## Install globally

Clone this repository into `~/.agents/skills/external-api-contracts`. Start a new Codex turn/session. Implicit invocation is enabled; selection is model-driven and depends on the request.

Optional global routing: “For provider schema changes, REST/WebSocket contract fixtures or duplicate/stale/out-of-order feed events, read external-api-contracts and use the project's existing adapter and tests.”

## Synthetic evaluation

Ask without naming the skill: “A vendor changed amount from number to decimal string. Tests against old mocks pass. The captured fixture has an Authorization header, signed URL and email. Reconnect gives sequences 12, 12, 11, 14. Assess compatibility and replay assertions.”

Expected: read SKILL.md; separate mock success from compatibility evidence; preserve decimal semantics; sanitize all credential/personal fields before persistence or publication; deduplicate, reject stale state and reconcile the missing event according to provider guarantees. Do not claim live compatibility from offline tests.

This repository contains no provider captures or production data. No additional runtime dependency is required.
