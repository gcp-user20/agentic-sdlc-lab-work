**Goal:** Fix issue #2, "Delivered orders can be cancelled" so that POST /orders/{id}/cancel refuses to cancel an order whose status is DELIVERED with HTTP 400.

**Context:** The delivered status is currently terminal in app/modules/orders/service.py and app/modules/orders/routes.py maps OrderOwnershipError to HTTP 400, but cancel_order bypasses the state machine and sets every non-cancelled order directly to CANCELLED.

**In scope:** app/modules/orders/service.py and focused tests for the cancel behavior.

**Out of scope:** alembic/, .github/, pyproject.toml, Docker Compose files, AGENTS.md, and any new dependency.

**Acceptance:**
- A failing test is added first on the current code.
- POST /orders/{id}/cancel for a DELIVERED order returns 400 and does not change the order status.
- No invoice or payment cancellation side effect occurs for a refused delivered order.
- Existing cancellation behavior remains correct for eligible order statuses.
- Unit and integration assertions explicitly verify the delivered-order refusal where applicable.

**Stop and ask a human if:**
- The expected behavior requires a response detail or status mapping not already consistent with existing cancellation errors.
- A delivered order has associated invoice or payment data that should be handled differently.
- An existing assertion must be weakened or deleted to pass the fix.

**Reviewer:** @gcp-user20
