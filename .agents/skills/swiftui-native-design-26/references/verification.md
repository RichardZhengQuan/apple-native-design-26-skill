# Verification Contract

Use this before finalizing any SwiftUI 26 UI or UX work. Do not claim that a
surface is SwiftUI-native, polished, or complete from compile success alone.

## Required Evidence

For every meaningful visual or UX change, gather the strongest practical
evidence available:

- Build result for the target SDK.
- Runtime launch on the target platform.
- Screenshot or live inspection of the changed surface.
- Compact and expanded size checks.
- Light and Dark appearance checks when visuals or materials changed.
- Accessibility pass for labels, focus, keyboard, contrast, Dynamic Type where
  applicable, and reduced transparency when glass/materials are used.
- State coverage for loading, empty, error, disabled, selected, hover/focus, and
  destructive/recovery paths where relevant.

If any evidence cannot be collected, state exactly what was not verified and
why.

## iOS and iPadOS Loop

- Build with the app's Xcode project or Swift package command.
- Use the iOS Simulator for runtime verification when possible.
- Inspect at minimum:
  - iPhone compact portrait.
  - iPhone landscape or compact-height when relevant.
  - iPad regular width, including split view/multitasking when relevant.
- Check:
  - Safe-area behavior around floating bars, toolbars, tab bars, sheets, and
    keyboard.
  - Dynamic Type at normal and large accessibility sizes for text-heavy
    surfaces.
  - Touch targets, icon labels, VoiceOver names, and keyboard/pointer access on
    iPad.
  - Search field placement, tab behavior, and sheet/menu presentation.
  - Reduced transparency fallback when custom glass or materials are used.

When available, use the installed `build-ios-apps:ios-debugger-agent` skill for
Simulator launch, screenshots, and runtime debugging.

## macOS Loop

- Build with `swift build`, `xcodebuild`, or the project-local script.
- Launch a foreground `.app` bundle for GUI verification. Do not judge macOS UI
  from a raw command-line executable when window activation, toolbar rendering,
  menu commands, or materials matter.
- Inspect at minimum:
  - Normal desktop window size.
  - Minimum supported window size.
  - A wide size where sidebars, inspectors, and toolbars can spread out.
- Check:
  - Toolbar grouping, search placement, command discoverability, menu items, and
    keyboard shortcuts.
  - Sidebar selection, list density, split-view resizing, inspector context, and
    settings entry points.
  - Hover, focus ring, default/cancel action, disabled state, and contextual
    menu behavior.
  - Light/Dark mode, vibrancy/material readability, reduced transparency, and
    text clipping.

When available, use the installed `build-macos-apps:build-run-debug` skill for
build, foreground `.app` launch, logs, and runtime verification.

## Screenshot Acceptance

A screenshot passes only when:

- Text does not clip, overlap, or escape its container.
- Important content is not hidden behind glass, tab bars, toolbars, sidebars,
  sheets, popovers, or the keyboard.
- Glass is legible and semantically grouped, not decorative.
- Primary action, current scope, and current selection are visually clear.
- Toolbar/search/sidebar/inspector placement matches the platform model.
- Empty/error/loading states are not visually broken.
- The screen still works at compact and expanded sizes.

## Failure Criteria

Treat any of these as blocking until fixed or explicitly accepted by the user:

- Fake system navigation, tab bar, toolbar, sidebar, inspector, sheet, popover,
  menu, or search when native SwiftUI can express the behavior.
- Compile success without runtime launch for a visual change.
- Runtime launch without screenshot or live visual inspection for a visual
  change.
- Unreadable glass, stacked glass, nested card-on-card layouts, or decorative
  translucent overlays.
- Missing primary task path, missing recovery path, inaccessible icon-only
  controls, clipped text, or overlapping controls.
- macOS GUI judged from a non-foreground executable.

## Final Response Requirement

In the final response after implementation or review, include:

- Build/run/screenshot evidence collected.
- Viewports or window sizes checked.
- Accessibility and state checks performed.
- Any known unverified items or residual risk.
