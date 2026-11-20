# User Workflow Testing

Browser-based checks were performed against the local prototype. "Pass" means the tested UI path behaved as described; it does not mean a real transaction, API call, or backend write occurred.

## Executed workflows

| ID | Workflow and steps | Expected result | Actual result | Status |
|---|---|---|---|---|
| WF-01 | Home > Charge my EV > select Schedule > confirm | Booking appears in Activity with scheduled status, not Live Tracking. | Scheduled item appeared in Activity after routing fix. | Pass |
| WF-02 | Home > Charge now/Emergency > confirm | Order opens Live Tracking with an ETA. | Tracking opened; emergency route remained intact. | Pass |
| WF-03 | Wallet prepayment > confirm > change global payment option > cancel order | Cancellation returns the prepayment once to the wallet. | Refund used the payment method captured on the order; repeat cancellation is guarded. | Pass |
| WF-04 | Set battery to 0% > view Home range | No positive stale range is shown. | Home displayed approximately 0 km. | Pass |
| WF-05 | Mark all notifications read > return to Home | Unread badge is removed at zero. | Badge was hidden when unread count reached zero. | Pass |
| WF-06 | Add supported Bharat-series registration `22BH1234AB` | Valid plate is accepted and saved in normalized form. | Saved as `22 BH 1234 AB`. | Pass |
| WF-07 | Home > Car Wash > complete the available request flow | Car Wash flow is reachable and presents its simulated completion state. | Flow completed in the prototype. | Pass (simulation) |
| WF-08 | Home/More > Towing > complete the request flow | Towing flow is reachable and transitions to its expected UI state. | Flow completed in the prototype. | Pass (simulation) |
| WF-09 | More > Fuel & Gas > complete the request flow | Fuel flow is reachable and displays a confirmation/tracking state. | Flow completed in the prototype. | Pass (simulation) |
| WF-10 | More > Jump Start > complete the request flow | Jump-start flow is reachable and displays its expected result. | Flow completed in the prototype. | Pass (simulation) |
| WF-11 | Stations > search/filter stations | Matching station list/detail can be reached. | Search flow worked. | Pass (static data) |
| WF-12 | Station detail > choose a bay/slot > reserve | Reservation flow produces the expected local hold state. | Reservation flow worked; no server hold exists. | Pass (simulation) |
| WF-13 | Notifications > select a notification | Selected notification opens its conversation view. | Chat view opened. | Pass (local UI) |
| WF-14 | Notification chat > send a reply | Reply appears in the conversation. | Reply flow worked locally; no external message was sent. | Pass (simulation) |
| WF-15 | Open/update/read notification detail | View/update state is reflected and unread badge updates. | Tested view/update/read behavior worked. | Pass (local UI) |
| WF-16 | Account > Theme > choose a preset | Selected theme applies while keeping the same screen layout. | Theme selection worked; nine presets remain available. | Pass |
| WF-17 | Home > expand map > Back | Map-only state hides the other Home cards; Back restores Home. | Expand/back restored the expected state. | Pass |
| WF-18 | My Vehicles > Add Vehicle > submit invalid/valid values | Validation rejects invalid values and accepts supported registration input. | Add-vehicle validation and supported plate normalization worked. | Pass |
| WF-19 | Home > Account tab > Home tab | Bottom navigation changes the active screen. | Pointer hit-test and navigation passed at 390x844; browser returned to Home. | Pass |

## Journeys not implemented or not verifiable

| Journey | Expected production behavior | Actual project state | Status |
|---|---|---|---|
| New user: registration > login > profile > add vehicle | Authenticated account and server-persisted profile/vehicle | Registration, login, password reset, and session management are absent. Account profile is demo data. | Not implemented |
| Wallet: top-up/payment success/failure/history | Payment provider response and durable transaction history | Balance and payment choices are local simulation; no payment request or transaction record is created. | Not verifiable |
| Charging: dispatch > live van/vehicle telemetry > completion | Server-backed status, location, and completion update | Driver, route, ETA, and status are static/simulated. | Not verifiable |
| Retry/error recovery: timeout, offline, unauthorized, duplicate request | Actionable network error and safe retry without duplicate transaction | No network layer exists, so these conditions cannot be injected into real service operations. | Blocked |
| Vehicle management: server-backed edit/delete | Durable ownership-checked updates | Local prototype controls only; no server authorization or persistence. | Not verifiable |
| Receipt download/call/SOS | Real file download, phone call, or emergency contact | UI feedback only; no actual download, phone call, or verified emergency service integration. | Not verifiable |

## Notes

- No auth or API workflow was invented to make a journey appear complete.
- The prototype has hard-coded demo location/vehicle/order values. A successful UI transition is not evidence that an external service operation succeeded.
- The automated/browser regression evidence is summarized in [FINAL_TEST_RESULTS.md](FINAL_TEST_RESULTS.md).
