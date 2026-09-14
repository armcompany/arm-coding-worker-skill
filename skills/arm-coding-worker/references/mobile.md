# Mobile execution

Detect the framework and each supported platform from manifests, native projects, configuration, and CI. Inspect navigation, networking, auth/secure storage, app lifecycle, deep links, permissions, native modules, push notifications, offline behavior, keyboard handling, and platform-specific files only as affected.

Follow React Native/Expo, Android Kotlin/Java, iOS Swift, Flutter, or multiplatform conventions actually present. Preserve native configuration and plugins; shared source does not guarantee identical Android and iOS behavior.

For API-integrated changes, inspect client contracts, error handling, token lifetime, offline/retry behavior, and navigation outcomes. Password recovery may require server token semantics plus deep-link routing, app cold start, expired/reused token errors, and Android/iOS link configuration; use the existing architecture to determine which layers need edits.

Validate shared logic, contracts, and navigation first, then relevant native targets and device/simulator behavior. Include background/foreground transitions, permission denial, keyboard and link handling where changed. Confirm that a build command produces a local artifact rather than submitting an app or sending an over-the-air release.

Record platform outcomes separately. An Android pass does not establish an iOS pass; JavaScript tests and a web build do not establish native module compatibility. When Xcode, Android SDK, simulator/device, signing, or backend access is unavailable, run independent checks and report the exact remaining platform gate.
