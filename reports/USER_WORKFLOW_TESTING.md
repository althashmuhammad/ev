# User Workflow Testing

Browser-based checks were performed against the local prototype. "Pass" means the tested UI path behaved as described; it does not mean a real transaction, API call, or backend write occurred.

## Entry and customer-test flow

- **Customer test:** Welcome > Login as guest > continue with the fixed Tata Nexon EV > choose the illustrative Kochi test area > clean Home and local charging test flow.
- **Demo visit:** Welcome > Visit demo > existing Home without vehicle setup.
- Vehicle details are held in client memory for the guest session. No credentials, account, or server record are created; payment and service actions remain simulations.

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
| WF-20 | Load Home at 390x844 > inspect status bar | No decorative Dynamic Island/camera pill; time and system indicators remain. | Pill/dots were absent; Account and Home navigation still worked. | Pass |
| WF-21 | Select each theme > view Home map > activate Car Wash shortcut | Map remains visible in all themes; supplied Car Wash image loads; shortcut still opens Carwash. | Map background, map area, and route remained rendered for all nine presets; image loaded and action opened screen 13. | Pass |
| WF-22 | Demo: Charge my EV > Address > Setup (plug, kW, price/payment) > Arrival; test Now, Schedule, and Weekly | Plug, power, price, and payment stay together in Setup; selected details appear in review; each mode routes correctly; Weekly requires a repeat day. | Now reached tracking with selected values; Schedule and Weekly reached Activity; empty Weekly days showed validation and did not submit. | Pass (simulation) |
| WF-23 | Home > More > Accessories or Car Care > add item > review cart > adjust quantity > place demo order; also open Roadside Breakdown Assistance | More is a page; both product categories support a local cart and demo confirmation; no real payment/delivery is implied; breakdown assistance uses the existing recovery flow. | Both categories opened; cart totals and quantity updated; demo confirmation clearly stated no payment or order was sent; breakdown assistance still routes to towing. | Pass (local demo) |
| WF-24 | Welcome > Login as guest > continue with the fixed Nexon; separately choose Visit demo | Guest selects the fixed Tata Nexon EV without an account or vehicle form, then continues to the Kochi test-location step; demo bypass enters the existing Home directly. | Guest vehicle and Kochi location steps opened in sequence. Visit demo still opened the seeded Home with the existing vehicle and charging card. | Pass (local UI) |
| WF-25 | Login as guest > choose Kochi test area > Charge my EV > continue through address, setup, and arrival > create request | Customer mode starts without demo orders, battery telemetry, live map/station data, price, or payment; a local request ID/status and clearly labeled estimates appear only after submission. | Home began without a request or battery/range data. The Kochi test-area address was prefilled and editable. `TEST-001` displayed 25 kWh/CCS2/60 kW, a local 22-minute arrival estimate, and 25-minute charge-duration estimate after submission; pricing was unavailable and no payment occurred. | Pass (local test) |
| WF-26 | Login as guest > Schedule a test > enter address > choose local slot > save > cancel | A local schedule appears in Activity without a live ETA or provider dispatch; cancellation removes the schedule. | Schedule was labeled local-only, saved to Activity, and cancellation returned the empty scheduled state. | Pass (local test) |
| WF-27 | Login as guest > choose Weekly > continue without selecting weekdays > submit | No demo weekdays are preselected; a weekly request cannot be saved until the user chooses at least one day. | Weekday selection started empty; submission remained on the review step and showed the day-selection validation message. | Pass (local test) |
| WF-28 | Welcome > Visit demo | Demo entry retains the seeded demo Home independently of customer-test state. | The demo Home still showed its existing Van En Route card, 25 kWh / CCS2 / 60 kW detail, 14-minute tracking action, and seeded vehicle data. | Pass (demo path) |
| WF-29 | Guest > fixed Nexon EV > Kochi test location > create and complete a local charge request | The location step clearly identifies Kochi as illustrative and non-live; Activity shows only the request created in this session, moving it to Past History only after completion. | Kochi test location appeared on Home and the charge address. The local request showed its test ID and labeled estimates; after completion, Upcoming Request was empty and the request appeared in Past History. No sample history or station entries appeared. | Pass (local test) |
| WF-30 | Visit demo > remain on Home for five seconds | Battery readout animates to 15%; the charge card becomes an emergency red gradient with clear copy and a brief one-time attention motion. Guest test remains without fabricated battery data. | At 4.7 seconds the demo remained at 24% with the normal card. It then counted down to 15%, updated the battery fill and estimated range to ~49 km, and showed “Emergency / Charge your vehicle now” with a brief pop/shake. The guest test stayed disconnected after 6.5 seconds; the emergency palette and white text persisted across all nine themes. | Pass (demo animation) |

## Journeys not implemented or not verifiable

| Journey | Expected production behavior | Actual project state | Status |
|---|---|---|---|
| New user: authenticated registration/login > profile > durable vehicle | Verified identity, secure account session, and server-persisted profile/vehicle | Guest entry and local vehicle setup are available, but credential-based authentication, account persistence, password reset, and session management are absent. Existing account and service data remain demo values. | Not implemented |
| Wallet: top-up/payment success/failure/history | Payment provider response and durable transaction history | Balance and payment choices are local simulation; no payment request or transaction record is created. | Not verifiable |
| Charging: dispatch > live van/vehicle telemetry > completion | Server-backed status, location, and completion update | The demo path retains static sample data. Guest test requests and their arrival/charge-duration estimates are generated locally only; no provider dispatch, live telemetry, payment, or server update occurs. | Not implemented |
| Retry/error recovery: timeout, offline, unauthorized, duplicate request | Actionable network error and safe retry without duplicate transaction | No network layer exists, so these conditions cannot be injected into real service operations. | Blocked |
| Vehicle management: server-backed edit/delete | Durable ownership-checked updates | Local prototype controls only; no server authorization or persistence. | Not verifiable |
| Receipt download/call/SOS | Real file download, phone call, or emergency contact | UI feedback only; no actual download, phone call, or verified emergency service integration. | Not verifiable |

## Notes

- No auth or API workflow was invented to make a journey appear complete.
- The demo path retains hard-coded location/vehicle/order values. Guest test details and request history exist only in the current browser session; a successful UI transition is not evidence that an external service operation succeeded.
- The automated/browser regression evidence is summarized in [FINAL_TEST_RESULTS.md](FINAL_TEST_RESULTS.md).
