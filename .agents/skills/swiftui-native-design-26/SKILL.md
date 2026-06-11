---
name: swiftui-native-design-26
description: Design, audit, and implement SwiftUI-native UI and UX for iOS 26, iPadOS 26, and macOS 26. Use when building, modernizing, reviewing, or polishing SwiftUI 26 interfaces, Liquid Glass, native app structure, navigation, task flows, tab bars, toolbars, sidebars, inspectors, search, controls, states, accessibility, SF Symbols, app icons, verification, or official UI kit references.
---

# SwiftUI Native Design 26

## Overview

Use this skill for SwiftUI-first iOS, iPadOS, and macOS UI and UX work where the target
is iOS 26, iPadOS 26, or macOS 26. Build the native experience first, then style
it: task flow, information architecture, platform structure, controls,
presentation, focus, keyboard, accessibility, and runtime verification matter
more than screenshot-only visual imitation.

Keep this skill focused on SwiftUI 26 design decisions.

## Quick Start

1. Identify the target platform, deployment target, SDK/Xcode version, app
   architecture, and design source.
2. Define the UX contract before UI: target user, primary job, entry point,
   happy path, secondary actions, empty/error/recovery states, permissions, and
   success signal.
3. Inspect the existing SwiftUI code before designing. Reuse local navigation,
   state, spacing, icon, and naming conventions.
4. Choose native structures before custom chrome: `TabView`, `NavigationStack`,
   `NavigationSplitView`, `toolbar`, `searchable`, `inspector`, `sheet`,
   `popover`, `Menu`, `Form`, `List`, standard controls, and commands.
5. Apply SwiftUI 26 treatment after the structure is correct: system surfaces,
   Liquid Glass, adaptive layout, content-first hierarchy, SF Symbols, and
   Icon Composer guidance where relevant.
6. Verify with the platform-specific loop in `references/verification.md`.
   Do not claim SwiftUI-native polish until build, launch, screenshot inspection,
   accessibility, state coverage, and compact/desktop sizing have been checked.

When API availability or platform behavior may have changed, consult current
official developer documentation in addition to this skill's references.

## Task Paths

### Design Audit

- Lead with concrete mismatches: missing native APIs, fake system components,
  broken task flow, custom chrome that fights SwiftUI 26 behavior, unreadable
  glass, poor density, missing states, missing accessibility, or missing
  verification.
- Reference code paths and line numbers when reviewing implementation.
- Separate structure issues from visual polish; a visually close mockup is not
  correct if it lacks native navigation, focus, keyboard, or presentation.
- Load `references/swiftui-26-design.md`, `references/ux-contract.md`, and
  `references/verification.md`.
- Load `references/native-component-map.md` when auditing app shell, search,
  toolbar, sidebar, inspector, controls, Liquid Glass, sheets, tabs, menus, or a
  component catalog.

### Modernize Existing SwiftUI

- Read the root scene and nearest existing feature before editing.
- Preserve or improve the user task flow; do not modernize visuals while making
  primary actions harder to find or recovery states weaker.
- Replace fake sidebars, toolbars, search fields, tabs, inspectors, overlays,
  settings panels, and controls with native SwiftUI equivalents where possible.
- Remove opaque fills, nested cards, dark scrims, and bespoke blur layers that
  obscure system surfaces unless the product explicitly needs them.
- Add SwiftUI 26 APIs behind availability checks when the project still supports
  earlier OS versions.
- Preserve established local state ownership and file boundaries.
- Use `references/native-component-map.md` and the local component catalog when
  a matching native component pattern exists.

### Build A New Surface

- Choose the platform shell first: `TabView`, `NavigationStack`,
  `NavigationSplitView`, document window, settings scene, inspector, or utility
  window.
- Build the task model before the screen model: information hierarchy, primary
  action, secondary actions, contextual actions, and completion feedback.
- Define state ownership before UI code: view-local, route-owned, scene-owned,
  window-scoped, or app-wide.
- Use system-adaptive colors, materials, semantic foreground styles, SF Symbols,
  and standard control sizing before adding custom components.
- Include natural states for reusable UI: selected, disabled, hover, focus,
  loading, empty, error, compact, and expanded when relevant.
- Load `references/ux-contract.md` and `references/native-component-map.md`
  before implementing non-trivial app shells or reusable components.

## Platform Guidance

### iOS and iPadOS 26

- Use `TabView` for persistent app sections and `NavigationStack` for drill-in
  flows. Avoid custom tab bars unless native tabs cannot express the product
  model.
- Let system navigation, tab bars, sheets, menus, and controls carry the
  SwiftUI 26 visual language before adding custom glass.
- Keep content visible and scannable around floating bars and bottom
  accessories. Do not place critical text behind busy translucent content.
- Design for Dynamic Type, touch targets, safe areas, orientation changes,
  multitasking, and keyboard/pointer use on iPad.
- Prefer `Label` and SF Symbols for icon-text controls so localization,
  mirroring, weight, and scale stay system-aligned.

### macOS 26

- Prefer desktop-native structure: `NavigationSplitView`, sidebar
  `List(selection:)`, inspectors, toolbars, search, settings, commands, menus,
  contextual actions, and keyboard shortcuts.
- Keep density calm and work-focused. Toolbars should be compact and
  command-oriented; sidebars and inspectors should be scannable.
- Attach `searchable` at the container level that matches the search scope.
- Use `ToolbarSpacer`, badges, and system toolbar grouping instead of custom
  toolbar backgrounds or hand-built command strips.
- Use AppKit interop only for window, responder-chain, text-system, panel, or
  system behavior SwiftUI cannot express cleanly.

## Liquid Glass Guardrails

- Prefer native Liquid Glass APIs and system-provided bars, sheets, controls,
  and surfaces over handmade blur stacks.
- Add custom glass only for meaningful custom controls or surfaces that standard
  SwiftUI components do not cover.
- Group related nearby custom glass elements in `GlassEffectContainer`.
- Use interactive glass only for interactive elements.
- Use tint only for semantic emphasis, status, or a primary action.
- Do not stack glass panels inside glass panels, build decorative glass blobs,
  or place text-heavy glass over busy content.
- Provide non-glass or softer material fallbacks when deployment targets,
  reduced transparency, or SDK availability require them.
- For API-level implementation details, load the exact companion skill for the
  platform when available:
  `build-ios-apps:swiftui-liquid-glass` for iOS/iPadOS,
  `build-macos-apps:liquid-glass` for macOS.

## Icons And Design Resources

- Use SF Symbols or the app's existing symbol system for interface icons.
- Use Icon Composer guidance for layered app icons instead of hand-painted
  one-off icon effects.
- Treat the official Sketch/Figma UI kits as reference material. Do not
  copy, vendor, or redistribute UI kit assets inside a skill or repo unless the
  user provides separate rights and asks for that explicitly.
- If a task depends on exact design-file details, inspect the live Sketch/Figma
  source or user-provided exported assets for that task only.

## References

- Load `references/swiftui-26-design.md` for official source links and distilled
  SwiftUI 26 UI rules.
- Load `references/ux-contract.md` for task-flow, information architecture,
  states, permissions, and recovery requirements.
- Load `references/native-component-map.md` whenever choosing or auditing
  native component structure. If `/Users/richardq/Documents/Components` exists,
  treat it as required evidence for comparable component patterns.
- Load `references/verification.md` before finalizing any visual or UX work.

## Companion Skills

Use these exact companion skills when they are installed and the request needs
their depth after this skill has established the design and UX direction:

- `build-ios-apps:swiftui-ui-patterns`: iOS/iPadOS SwiftUI navigation, state,
  async state, sheets, previews, and performance structure.
- `build-ios-apps:swiftui-liquid-glass`: iOS/iPadOS 26+ Liquid Glass API usage.
- `build-ios-apps:ios-debugger-agent`: Simulator build, run, screenshot, and
  runtime debugging.
- `build-macos-apps:swiftui-patterns`: macOS scenes, windows, commands,
  settings, split views, and inspectors.
- `build-macos-apps:liquid-glass`: macOS 26 Liquid Glass API usage.
- `build-macos-apps:build-run-debug`: macOS build, foreground `.app` launch,
  logs, and runtime verification.
