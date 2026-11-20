# API & Business Logic Audit

## API inventory

| Check | Result |
|---|---|
| HTTP client / request calls | No `fetch`, Axios, XMLHttpRequest, or `/api/` usage was found in the application source. |
| Endpoints and HTTP methods | None present; no endpoint can be verified. |
| Request/response DTOs | None present. |
| Auth headers, token refresh, route authorization | None present. |
| API error/loading/timeout/retry behavior | Not applicable; there is no network integration. |
| Backend/database | No ASP.NET project, SQL schema, stored procedure, or database integration was found. |

Therefore API success, empty/null payload, validation error, unauthorized/forbidden, not-found, server error, timeout, slow response, duplicate request, and expired-session tests are **blocked**, not passed.

## Business logic reviewed

### Charging quote

[`chargeQuote`](../app1.1.html#L3283) selects a supported kWh option (defaulting to 25), obtains a rate from the local speed table (fallback 20), applies a minimum energy charge, adds a call-out fee (zero for Pro, otherwise 129 for prepayment or 149 for postpayment), and estimates duration/ETA from selected speed/payment mode.

The code path was reviewed and the charge confirmation/route flows were exercised. The source does not establish whether the price floor, fees, ETA, speed/rate table, or rounding match approved business policy. No real tariff, dispatch estimate, taxes, or server quote exists. These values require product/backend confirmation before they can be treated as financial rules.

### Orders, payment, and cancellation

[`placeOrder`](../app1.1.html#L2177) stores scheduled or active orders in client state. For wallet prepayment it checks and debits the local balance before creating the order. The order now captures its payment method, and [`cancelActiveOrder`](../app1.1.html#L2201) uses that method and a cancellation guard for a local refund. Regression checks passed after changing the global payment selection.

This is not a transactional payment/refund implementation: there is no provider authorization/capture, ledger, durable transaction, concurrency protection, server idempotency key, or reconciliation. UI messages such as "refund initiated" are not proof of an issued refund.

### Battery and vehicle data

Zero battery now displays approximately zero remaining range. Battery percentage, range conversion, vehicle model, connector, and registration data remain demo/client values; there is no vehicle-specific telemetry or server validation. The supported Bharat plate normalization case passed, but the prototype's validation must not replace authoritative registration checks.

### Schedule, station, and status data

- Schedule labels are static strings (`Tonight 9 PM`, `Tomorrow 9 AM`, `Sat 10 AM`); date, timezone, operating hours, slot availability, and expiry are not server-backed.
- Station availability, reservation holds, driver details, route, ETA, and charging-progress stages are mock values.
- The station UI can warn about a connector mismatch without preventing the hold action. Whether adapters are allowed is unresolved; no behavior change was made without a confirmed rule.
- Status values are local UI state and do not reflect a verified dispatch lifecycle.

## Data integrity and validation

- Fixed wallet refund dependence on mutable global payment selection and added repeat-cancellation protection; browser regression passed.
- Fixed supported Bharat-series plate normalization; browser validation passed.
- Fixed zero-range boundary and unread badge state; browser regression passed.
- All order, wallet, vehicle, station, and notification state other than theme preferences is in memory. Refresh/restart persistence, multi-user isolation, concurrency, and database transactions cannot be tested.
- Duplicate provider payments, partial failures, request retries, and backend/frontend reconciliation are untestable until an API contract and isolated test environment exist.

## Required follow-up

Define authoritative contracts for tariff/minimum charge/call-out fees, payment state/refund rules, supported connector/adapter policy, schedule timezone/availability, dispatch status/ETA, vehicle ownership/validation, and failure/retry behavior. Then add API integration tests with isolated test data. Do not infer these rules from mock labels.
