# tvOS

- Build primary interaction around the focus engine, not touch. Flag layouts that assume direct tap/drag input as the main path.
- Prefer standard focusable controls (`Button`, `Toggle`, `NavigationLink`) over custom gesture targets, so directional navigation and selection work correctly.
- Use `@FocusState` and `.focused()` to set initial focus and to recover focus after navigation, sheet dismissal, or data reloads. Avoid forcing focus changes on every state update.
- Use `.focusSection()` to keep large screens navigable and prevent ambiguous directional jumps.

## 10-foot layout

- Design for distance viewing: prefer larger typography, clearer hierarchy, and stronger spacing than iOS equivalents.
- Keep content away from screen edges and overscan-risk areas; avoid edge-aligned critical controls.
- Prefer horizontal shelf-style browsing where appropriate, and avoid dense, phone-style forms packed with small controls.

## Siri Remote interaction

- Implement remote-specific commands where relevant, such as `onPlayPauseCommand` and `onExitCommand`.
- Do not hijack directional input that should be handled by the focus engine.
- Treat scrubbing, transport controls, and playback shortcuts as first-class remote interactions for media experiences.

## Platform differences and unavailable APIs

- Gate iOS-only code paths with `#if os(tvOS)` / `#if !os(tvOS)` and availability checks instead of assuming API parity.
- Flag iOS-specific interaction patterns that do not translate to Apple TV (for example, swipe-first interaction models).
- Ensure shared SwiftUI views provide a tvOS-specific branch when behavior differs in focus, input, or presentation.

## Top Shelf and media

- If the app includes a Top Shelf extension, validate that it surfaces current, high-value content and routes into the correct in-app destination.
- Keep Top Shelf metadata and deep-link targets consistent with in-app models to avoid stale or broken entry points.
- For playback-heavy apps, ensure tvOS playback flows are built for remote-first control and full-screen media expectations.

## Multi-user

- Validate that personalized rows (Continue Watching, recommendations, watchlist) update for the active tvOS user profile.
- Avoid caching user-specific content globally without user scoping; account for user switching behavior.
