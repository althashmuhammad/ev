# Responsive Testing

## Method and scope

The original viewport simulation covered the 13 primary screens and major workflow/map states. The 16 viewport sizes below were used in the browser. Across 332 screen/step-by-viewport combinations, checks found no horizontal overflow, unnamed active buttons, or active targets below 44 CSS px. After adding routes 14–20, the welcome, guest vehicle setup, Kochi test-location, More, catalog, cart, and confirmation pages were spot-checked at 320x640 with no horizontal overflow after transitions settled. The clean customer-test Home, More, charging Address/Setup/Arrival steps, and the demo emergency battery card were also checked at 320x640 after transitions settled; no horizontal overflow was detected. This is browser emulation only; no physical phones/tablets or operating-system accessibility services were used.

## Viewport matrix

| Viewport | Target | Screen/step coverage | Overflow | Layout/touch result | Representative screenshot |
|---|---|---|---|---|---|
| 320x640 | Small mobile | Original primary routes and sampled steps; routes 14–19 and guest charging flow spot-checked after the matrix | None detected after transitions settled | Pass; content scrolls within viewport; More and shop pages scroll vertically; active targets >=44px in original sweep | [Home](screenshots/after/Home-320x640.png) |
| 320x700 | Small mobile | Charging setup step | None detected | Pass; stepper targets 48px, radio targets >=51px, price/payment reachable by scrolling | — |
| 360x800 | Mobile | Same | None detected | Pass | [Home](screenshots/after/Home-360x800.png) |
| 375x812 | Mobile | Same | None detected | Pass | [Home](screenshots/after/Home-375x812.png) |
| 390x844 | Mobile/reference | Same | None detected | Pass | [Current Home](screenshots/after/Audit-Home-Carwash-Map-390x844.png) |
| 414x896 | Mobile | Same | None detected | Pass | [Home](screenshots/after/Home-414x896.png) |
| 430x932 | Large mobile | Same | None detected | Pass | [Home](screenshots/after/Home-430x932.png) |
| 480x900 | Large mobile | Same | None detected | Pass | [Home](screenshots/after/Home-480x900.png) |
| 600x960 | Small tablet | Same | None detected | Pass | [Home](screenshots/after/Home-600x960.png) |
| 768x1024 | Tablet | Same | None detected | Pass | [Home](screenshots/after/Home-768x1024.png) |
| 900x600 | Short landscape/tablet | Same | None detected | Pass; scrollable content remains reachable | [Home](screenshots/after/Home-900x600.png) |
| 1024x1366 | Tablet/portrait | Same | None detected | Pass | [Home](screenshots/after/Home-1024x1366.png) |
| 1280x800 | Desktop | Same | None detected | Pass | [Home](screenshots/after/Home-1280x800.png) |
| 1366x768 | Desktop | Same | None detected | Pass | [Home](screenshots/after/Home-1366x768.png) |
| 1440x900 | Desktop | Same | None detected | Pass | [Home](screenshots/after/Home-1440x900.png) |
| 1920x1080 | Large desktop | Same | None detected | Pass | [Home](screenshots/after/Home-1920x1080.png) |

## Screen coverage

Each screen below was included in the viewport sweep. The `390x844` capture is representative; the full viewport-specific captures are in `reports/screenshots/after/`.

| Screen/state | Layout result | Screenshot |
|---|---|---|
| Home | Pass | [Home](screenshots/after/Audit-Home-Carwash-Map-390x844.png) |
| Quick Charge | Pass | [Charge](screenshots/after/Charge-390x844.png) |
| Live Tracking | Pass | [Tracking](screenshots/after/Tracking-390x844.png) |
| Stations | Pass | [Stations](screenshots/after/Stations-390x844.png) |
| Station Details | Pass | [Station Details](screenshots/after/Station-Detail-390x844.png) |
| Jump Start | Pass | [Jump Start](screenshots/after/Jump-Start-390x844.png) |
| Towing | Pass | [Towing](screenshots/after/Validated-Towing-320x640.png) |
| Activity | Pass | [Activity](screenshots/after/Activity-390x844.png) |
| My Vehicles | Pass | [Vehicles](screenshots/after/Vehicles-390x844.png) |
| Add Vehicle | Pass | [Add Vehicle](screenshots/after/Add-Vehicle-390x844.png) |
| Account | Pass | [Account](screenshots/after/Account-390x844.png) |
| Fuel & Gas | Pass | [Fuel](screenshots/after/Fuel-Delivery-390x844.png) |
| Carwash | Pass | [Carwash](screenshots/after/Carwash-390x844.png) |
| Wallet subview | Pass | [Wallet](screenshots/after/Wallet-390x844.png) |
| Home Setup subview | Pass | [Home Setup](screenshots/after/Home-Setup-390x844.png) |
| Theme presets | Pass | [Pure Black map](screenshots/after/Audit-Home-Map-PureBlack-390x844.png); other `Validated-Theme-*` captures |

## Accessibility checks and limitations

- The responsive sweep found no unnamed active buttons or active targets below 44 CSS px.
- Account/Home navigation was verified with a pointer at 390x844.
- Global reduced-motion rules shorten animation/transition durations, but the complete animation system was not rechecked under reduced-motion preference in this audit.
- Contrast ratios across every theme/state, keyboard-only coverage, screen-reader announcements, zoom/reflow, and physical safe-area behavior were not formally tested. No WCAG 2.2 AA compliance claim is made.
- Viewport simulation cannot substitute for physical device, mobile keyboard, or assistive-technology testing.
- The Home map's background layers and route were checked in all nine themes; its theme palette changes without suppressing the map. The final status-bar, map, and Car Wash artwork changes are captured at 390x844 above. Other viewport-specific screenshots predate those visual changes; they did not alter screen dimensions or layout geometry.
