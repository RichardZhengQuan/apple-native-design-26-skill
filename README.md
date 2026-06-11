# SwiftUI Native Design Skills

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](LICENSE)

Codex skills for building SwiftUI interfaces that feel like real native apps,
not screenshots of native apps.

This repository packages versioned SwiftUI design workflows for iOS, iPadOS,
and macOS. Each skill gives Codex a reusable process for designing, auditing,
implementing, and verifying SwiftUI-native UI/UX with the right design files,
native components, accessibility checks, Liquid Glass restraint, and runtime
evidence.

## Included Skills

| Skill | Target | Use when |
| --- | --- | --- |
| `$swiftui-native-design-27` | iOS 27, iPadOS 27, macOS 27 | Building or reviewing against the newest OS 27 design files and Xcode 27-era behavior. |
| `$swiftui-native-design-26` | iOS 26, iPadOS 26, macOS 26 | Maintaining, modernizing, or reviewing apps still targeting the OS 26 design system. |

Use the newest skill for new work unless the app is explicitly pinned to the
older SDK/design resources.

## Why This Exists

Most AI-generated "SwiftUI-style" UI gets the surface wrong in predictable ways:

- It draws fake sidebars, fake tab bars, fake toolbars, and fake glass instead
  of using SwiftUI's native structures.
- It treats Liquid Glass as decoration instead of an interaction and hierarchy
  system.
- It makes a screen look plausible while leaving the actual user flow, empty
  states, error recovery, keyboard access, and accessibility undefined.
- It stops after compile success, without launching the app or checking a
  screenshot at real device/window sizes.

These skills make Codex slow down at the right moments: define the UX contract,
choose native SwiftUI components, apply version-specific visual treatment only
after the structure is right, then verify the result like native UI work
actually needs to be verified.

## What Codex Gets

| Area | What the skills enforce |
| --- | --- |
| UX contract | Target user, primary job, entry points, happy path, recovery, permissions, and success signal before UI work. |
| Native structure | `TabView`, `NavigationStack`, `NavigationSplitView`, `toolbar`, `searchable`, `inspector`, sheets, popovers, menus, forms, lists, and commands before custom chrome. |
| Versioned design | Separate 26 and 27 references for UI kits, Liquid Glass behavior, design sessions, and OS-specific checks. |
| Component evidence | Native component maps and optional local catalog references so Codex can ground decisions in real SwiftUI examples. |
| Verification | iOS/iPadOS Simulator and macOS foreground `.app` verification loops, screenshot acceptance criteria, accessibility checks, and blocking failure cases. |

## Install

This repository is laid out as repo-scoped Codex skills:

```text
.agents/skills/
├── swiftui-native-design-26/
└── swiftui-native-design-27/
```

Open this repository in Codex and mention the skill you want:

```text
Use $swiftui-native-design-27 to audit this SwiftUI app for OS 27 native UI/UX.
```

To install both skills globally for your local Codex setup, copy the folders
into your user skills directory:

```bash
mkdir -p "$HOME/.agents/skills"
cp -R .agents/skills/swiftui-native-design-26 "$HOME/.agents/skills/"
cp -R .agents/skills/swiftui-native-design-27 "$HOME/.agents/skills/"
```

Some Codex app builds also scan `$HOME/.codex/skills`. If the skills do not
appear in your skills list, use the path shown in your Codex skills panel or
restart Codex after copying.

## Example Prompts

Use the OS 27 skill for new work:

```text
Use $swiftui-native-design-27 to implement this iOS 27 SwiftUI screen. Define
the UX contract first, use native tabs/search/toolbars/Liquid Glass where
appropriate, then verify in Simulator.
```

Audit an existing macOS app:

```text
Use $swiftui-native-design-27 to review this macOS SwiftUI app. Findings first:
native component mismatches, UX flow issues, accessibility gaps, Liquid Glass
misuse, and missing verification.
```

Maintain an OS 26 target:

```text
Use $swiftui-native-design-26 to modernize Sources/App/ContentView.swift for an
app that still targets macOS 26. Keep the 26 design files as the reference and
verify with build/run/screenshots.
```

Review a design-to-code result:

```text
Use $swiftui-native-design-27 to compare this SwiftUI implementation against the
provided design. Separate UX issues, native-structure issues, visual fidelity
issues, and verification gaps.
```

## Skill Contents

```text
.agents/skills/
├── swiftui-native-design-26/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
│       ├── swiftui-26-design.md
│       ├── native-component-map.md
│       ├── ux-contract.md
│       └── verification.md
└── swiftui-native-design-27/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
        ├── swiftui-27-design.md
        ├── native-component-map.md
        ├── ux-contract.md
        └── verification.md
```

- `SKILL.md`: the main workflow Codex reads when a skill is invoked.
- `swiftui-26-design.md` / `swiftui-27-design.md`: versioned design rules and
  official source links.
- `ux-contract.md`: task flow, information architecture, state coverage,
  permissions, recovery, and platform UX requirements.
- `native-component-map.md`: native SwiftUI component choices and local catalog
  grounding.
- `verification.md`: platform-specific build, launch, screenshot,
  accessibility, and failure criteria.

## Design Principles

The skills are opinionated:

- Native structure first, visual polish second.
- UX before pixels.
- SwiftUI system components before custom drawing.
- Liquid Glass only where it clarifies hierarchy or interaction.
- SF Symbols and Icon Composer before one-off icon styling.
- Runtime verification before claiming the UI is polished.
- Official design files and Sketch references, not bundled assets.

## Official References

The skills link to, but do not copy, official source material.

### Design And Technology

- [Design Resources](https://developer.apple.com/design/resources/)
- [SwiftUI technology overview](https://developer.apple.com/documentation/technologyoverviews/swiftui)
- [Adopting Liquid Glass](https://developer.apple.com/documentation/TechnologyOverviews/adopting-liquid-glass)
- [Liquid Glass technology overview](https://developer.apple.com/documentation/technologyoverviews/liquid-glass)
- [SF Symbols](https://developer.apple.com/sf-symbols/)
- [Icon Composer](https://developer.apple.com/icon-composer/)

### Human Interface Guidelines

- [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines)
- [HIG: Materials](https://developer.apple.com/design/human-interface-guidelines/materials)
- [HIG: Layout](https://developer.apple.com/design/human-interface-guidelines/layout)
- [HIG: Navigation and search](https://developer.apple.com/design/human-interface-guidelines/navigation-and-search)
- [HIG: Tab bars](https://developer.apple.com/design/human-interface-guidelines/tab-bars)
- [HIG: Toolbars](https://developer.apple.com/design/human-interface-guidelines/toolbars)
- [HIG: Sidebars](https://developer.apple.com/design/human-interface-guidelines/sidebars)
- [HIG: App icons](https://developer.apple.com/design/human-interface-guidelines/app-icons/)

### OS 27 UI Kits

- [iOS 27 UI Kit on Sketch](https://www.sketch.com/s/04c24d8b-38fb-4afb-8836-36617e022f02)
- [macOS 27 UI Kit on Sketch](https://www.sketch.com/s/57153a31-3379-4737-8ac6-dbfd6525f052)

### OS 26 UI Kits

- [iOS 26 UI Kit on Sketch](https://www.sketch.com/s/f63aa308-1f82-498c-8019-530f3b846db9)
- [macOS 26 UI Kit on Sketch](https://www.sketch.com/s/7e5d41a8-dbde-4372-abf1-59792d73bc7c)

### WWDC Design Sessions

- [WWDC26: What's new in SwiftUI](https://developer.apple.com/videos/play/wwdc2026/269/)
- [WWDC26: Platforms State of the Union](https://developer.apple.com/videos/play/wwdc2026/102/)
- [WWDC25: Build a SwiftUI app with the new design](https://developer.apple.com/videos/play/wwdc2025/323/)
- [WWDC25: Get to know the new design system](https://developer.apple.com/videos/play/wwdc2025/356/)

The same URLs live in each skill's versioned design reference so Codex can load
them while using the skill.

## What This Is Not

- It is not a UI kit redistribution.
- It does not include official, Sketch, or Figma assets.
- It is not a replacement for compiling and running your app.
- It is not a promise that every generated interface is perfect on the first
  pass.

It is a workflow that makes Codex ask the right questions, use the right native
APIs, and collect the right evidence before it calls the work done.

## Validation

Run the skill validator after editing:

```bash
python /path/to/skill-creator/scripts/quick_validate.py \
  .agents/skills/swiftui-native-design-26

python /path/to/skill-creator/scripts/quick_validate.py \
  .agents/skills/swiftui-native-design-27
```

Expected result for each skill:

```text
Skill is valid!
```

For visual UI changes made with these skills, also run the project-specific
build and runtime checks described in each skill's `references/verification.md`.

## Contributing

Good contributions should make the skills more operational, not just longer.

Useful PRs include:

- Better version-specific component decision rules.
- More precise SwiftUI examples for native structures.
- Stronger iOS Simulator or macOS app verification guidance.
- Accessibility and Dynamic Type improvements.
- Corrections when SwiftUI platform APIs or HIG guidance change.

Please avoid:

- Copying official, Sketch, or Figma assets into the repository.
- Adding broad design advice that does not change Codex behavior.
- Expanding the skills into unrelated platforms without a clear workflow.

## License

Apache-2.0.

Apache-2.0 is permissive and includes an explicit patent grant, which makes it a
good default for reusable developer tooling and agent workflow assets.
