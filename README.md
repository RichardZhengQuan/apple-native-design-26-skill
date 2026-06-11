# Apple Native Design 26 Skill

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](LICENSE)

A Codex skill for building SwiftUI interfaces that feel like real Apple apps,
not screenshots of Apple apps.

`apple-native-design-26` gives Codex a reusable workflow for designing,
auditing, implementing, and verifying Apple-native UI/UX for iOS 26, iPadOS 26,
and macOS 26. It focuses on the parts that usually separate polished native
software from a nice-looking mockup: task flow, platform structure, system
components, accessibility, Liquid Glass restraint, and runtime verification.

## Why This Exists

Most AI-generated "Apple-style" UI gets the surface wrong in predictable ways:

- It draws fake sidebars, fake tab bars, fake toolbars, and fake glass instead
  of using SwiftUI's native structures.
- It treats Liquid Glass as decoration instead of an interaction and hierarchy
  system.
- It makes a screen look plausible while leaving the actual user flow, empty
  states, error recovery, keyboard access, and accessibility undefined.
- It stops after compile success, without launching the app or checking a
  screenshot at real device/window sizes.

This skill makes Codex slow down at the right moments. It pushes the agent to
define the UX contract first, choose native Apple components, apply Apple 26
visual treatment only after the structure is right, and verify the result like
native UI work actually needs to be verified.

## What Codex Gets From This Skill

| Area | What the skill enforces |
| --- | --- |
| UX contract | Target user, primary job, entry points, happy path, recovery, permissions, and success signal before UI work. |
| Native structure | `TabView`, `NavigationStack`, `NavigationSplitView`, `toolbar`, `searchable`, `inspector`, sheets, popovers, menus, forms, lists, and commands before custom chrome. |
| Apple 26 design | Practical guidance for tabs, search placement, toolbar grouping, controls, Liquid Glass, scroll edge effects, SF Symbols, and layered app icons. |
| Component evidence | A native component map and optional local catalog reference so Codex can ground decisions in real SwiftUI examples. |
| Verification | iOS/iPadOS Simulator and macOS foreground `.app` verification loops, screenshot acceptance criteria, accessibility checks, and blocking failure cases. |

## Install

This repository is already laid out as a repo-scoped Codex skill:

```text
.agents/skills/apple-native-design-26/
```

Open this repository in Codex and mention the skill by name:

```text
Use $apple-native-design-26 to audit this SwiftUI app for Apple 26 native UI/UX.
```

To install it globally for your local Codex setup, copy the skill folder into
your user skills directory:

```bash
mkdir -p "$HOME/.agents/skills"
cp -R .agents/skills/apple-native-design-26 "$HOME/.agents/skills/"
```

Some Codex app builds also scan `$HOME/.codex/skills`. If the skill does not
appear in your skills list, use the path shown in your Codex skills panel or
restart Codex after copying.

## Example Prompts

Audit an existing macOS app:

```text
Use $apple-native-design-26 to review this macOS SwiftUI app. Findings first:
native component mismatches, UX flow issues, accessibility gaps, Liquid Glass
misuse, and missing verification.
```

Modernize a screen:

```text
Use $apple-native-design-26 to redesign Sources/App/ContentView.swift for macOS
26. Replace fake chrome with native sidebars, toolbar/search, inspector
patterns, and verify with build/run/screenshots.
```

Build a new iOS surface:

```text
Use $apple-native-design-26 to implement this iOS 26 SwiftUI screen. Define the
UX contract first, use native tabs/search/toolbars/Liquid Glass where
appropriate, then verify in Simulator.
```

Review a design-to-code result:

```text
Use $apple-native-design-26 to compare this SwiftUI implementation against the
provided design. Separate UX issues, native-structure issues, visual fidelity
issues, and verification gaps.
```

## Skill Contents

```text
.agents/skills/apple-native-design-26/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── apple-26-design.md
    ├── native-component-map.md
    ├── ux-contract.md
    └── verification.md
```

- `SKILL.md`: the main workflow Codex reads when the skill is invoked.
- `apple-26-design.md`: distilled Apple 26 UI rules and official source links.
- `ux-contract.md`: task flow, information architecture, state coverage,
  permissions, recovery, and platform UX requirements.
- `native-component-map.md`: native SwiftUI component choices and local catalog
  grounding.
- `verification.md`: platform-specific build, launch, screenshot,
  accessibility, and failure criteria.

## Design Principles

The skill is opinionated:

- Native structure first, visual polish second.
- UX before pixels.
- SwiftUI system components before custom drawing.
- Liquid Glass only where it clarifies hierarchy or interaction.
- SF Symbols and Icon Composer before one-off icon styling.
- Runtime verification before claiming the UI is polished.
- Apple and Sketch design files as references, not bundled assets.

## Official References

The skill links to, but does not copy, official Apple material. The complete
source set currently used by the skill is:

### Apple Design And Technology

- [Apple Design Resources](https://developer.apple.com/design/resources/)
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

### Apple UI Kits

- [Apple iOS 26 UI Kit on Sketch](https://www.sketch.com/s/f63aa308-1f82-498c-8019-530f3b846db9)
- [Apple macOS 26 UI Kit on Sketch](https://www.sketch.com/s/7e5d41a8-dbde-4372-abf1-59792d73bc7c)

### WWDC Design Sessions

- [WWDC25: Build a SwiftUI app with the new design](https://developer.apple.com/videos/play/wwdc2025/323/)
- [WWDC25: Get to know the new design system](https://developer.apple.com/videos/play/wwdc2025/356/)

The same URLs live in
`.agents/skills/apple-native-design-26/references/apple-26-design.md` so Codex
can load them while using the skill.

## What This Is Not

- It is not an Apple UI kit redistribution.
- It does not include Apple, Sketch, or Figma assets.
- It is not a replacement for compiling and running your app.
- It is not a promise that every generated interface is perfect on the first
  pass.

It is a workflow that makes Codex ask the right questions, use the right native
APIs, and collect the right evidence before it calls the work done.

## Validation

Run the skill validator after editing:

```bash
python /path/to/skill-creator/scripts/quick_validate.py \
  .agents/skills/apple-native-design-26
```

Expected result:

```text
Skill is valid!
```

For visual UI changes made with this skill, also run the project-specific build
and runtime checks described in `references/verification.md`.

## Contributing

Good contributions should make the skill more operational, not just longer.

Useful PRs include:

- Better Apple 26 component decision rules.
- More precise SwiftUI examples for native structures.
- Stronger iOS Simulator or macOS app verification guidance.
- Accessibility and Dynamic Type improvements.
- Corrections when Apple updates APIs or HIG guidance.

Please avoid:

- Copying Apple, Sketch, or Figma assets into the repository.
- Adding broad design advice that does not change Codex behavior.
- Expanding the skill into unrelated Apple platforms without a clear workflow.

## License

Apache-2.0.

Apache-2.0 is permissive and includes an explicit patent grant, which makes it a
good default for reusable developer tooling and agent workflow assets.
