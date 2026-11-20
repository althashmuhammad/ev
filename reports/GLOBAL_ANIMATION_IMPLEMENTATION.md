# Global Animation Implementation

## Status

Implemented in the existing standalone `index.html`. The app uses inline CSS and JavaScript with no animation-library dependency. Existing transitions and feedback were audited and extended rather than replaced.

## 1. Existing animation audit

The app already had directional screen transitions, button press states, animated sheets and overlays, loading spinners, map-location pulses, call waves, and reduced-motion CSS. Several motion values were hardcoded, sheet dismissal was immediate, bottom sheets had no shared drag control, and modal exits were abrupt.

## 2. Motion tokens

Added shared durations for button (130ms), icon (180ms), small state changes (200ms), cards (280ms), modal (320ms), page navigation (380ms), and complex motion (450ms). Shared ease-in, ease-out, ease-in-out, and spring curves are used by the updated controls and transitions.

## 3. Components updated

- Interactive buttons now have consistent press feedback and tokenized color, border, shadow, and transform transitions.
- Interactive cards respond to press; static cards retain surface transitions without being treated as buttons.
- Inputs, segmented controls, option buttons, and switches use shared transition timing.
- Bottom navigation has theme-aware active feedback and icon transitions.
- Staggered screen content is limited to containers with at most eight direct children.

## 4. Screens and navigation

The shared motion rules cover all 13 existing screen renderers. Push and pop transitions preserve the existing navigation direction; tab changes use a shorter fade. The Home map uses a restrained expansion transition. Existing screen state and business actions remain owned by the original renderers and handlers.

## 5. Modal and sheet behavior

Bottom sheets replay their entrance animation on open and animate out on dismissal. A shared, keyboard-accessible 44px handle closes a sheet on tap and supports downward drag-to-dismiss; a drag of 90px or more dismisses, while shorter drags snap back. Outside click and Escape continue to dismiss sheets, and focus restoration remains in place.

Chat and voice-call overlays now use shared enter and exit transitions. State changes, timers, calls, and messages are handled immediately; only the visual removal is animated.

## 6. EV-specific motion

The existing location pulse, active call waves, and live-dispatch indicators are retained. The Home map expansion and active status affordances use theme tokens. No vehicle movement or battery-progress animation is fabricated: the prototype has no live location or telemetry stream to drive those states.

## 7. Accessibility and themes

All motion uses theme-aware tokens where color or shadow is involved. `prefers-reduced-motion` shortens animations and transitions to 0.01ms and disables smooth scrolling; reduced-motion sheet dismissal is immediate. A reduced-transparency media rule disables glass blur where supported. Focus-visible styles and semantic status colors remain intact.

## 8. Performance considerations

Transitions favor transform and opacity. Persistent `will-change` hints were removed from one-shot page and sheet animations. Large content groups do not receive entrance staggering. No animation package or recurring simulated vehicle movement was added.

## 9. Validation

Browser checks at 390 × 844 verified:

- Car Wash Home shortcut image and Nexon front image loaded; Car Wash still opened its existing flow.
- Stations navigation retained its push transition.
- Sheet entrance, close animation, drag dismissal, and reduced-motion immediate dismissal.
- Chat and call overlays opened and closed through their existing actions.
- No browser page errors were observed.

The reduced-motion test reported a computed animation duration of 0.01ms. Browser emulation was used; physical-device frame-rate and assistive-technology testing were not performed.

## 10. Remaining limitations

- No real-device or 60-FPS profiling was available in this standalone prototype.
- Pull-to-refresh, swipe-to-delete, and list virtualization were not added; the app has no corresponding data-backed list behavior.
- Battery and live map marker animation remain dependent on future real telemetry.
- Payment APIs and network-backed loading states are not present, so server-side idempotency and real loading behavior cannot be validated here.
- The existing Tailwind CDN production-use warning remains unrelated to this motion change.
