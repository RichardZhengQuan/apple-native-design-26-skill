# Apple Native Design 26 Skill

`apple-native-design-26` is a Codex skill for designing, auditing, implementing,
and verifying Apple-native SwiftUI UI/UX for iOS 26, iPadOS 26, and macOS 26.

The skill focuses on native platform structure first, then Apple 26 visual
treatment: task flow, information architecture, navigation, tabs, toolbars,
sidebars, inspectors, search, Liquid Glass, SF Symbols, app icons,
accessibility, and platform-specific verification.

## What It Covers

- SwiftUI-first Apple 26 UI/UX workflow.
- UX contract before visual implementation.
- Native component selection and audit rules.
- Apple 26 design rules for tabs, search, toolbars, controls, Liquid Glass, and
  scroll edge effects.
- iOS/iPadOS Simulator and macOS foreground app verification loops.
- Screenshot acceptance and blocking failure criteria.

## Use In Codex

Invoke it explicitly in a prompt:

```text
Use $apple-native-design-26 to audit this macOS SwiftUI app for Apple 26 native UI/UX.
```

Examples:

```text
Use $apple-native-design-26 to redesign Sources/App/ContentView.swift for macOS 26. Use native sidebars, toolbar/search, inspector patterns, and verify with build/run/screenshots.
```

```text
Use $apple-native-design-26 to implement this iOS 26 SwiftUI screen. Define the UX contract first, use native tabs/search/toolbars/Liquid Glass where appropriate, then verify in Simulator.
```

## Install

This repository is already laid out as a repo-scoped Codex skill:

```text
.agents/skills/apple-native-design-26/
```

To use it inside this repository, open the repo in Codex and mention
`$apple-native-design-26`.

To install it globally for your own Codex setup, copy the skill folder into the
user skill directory used by your Codex installation, for example:

```bash
mkdir -p "$HOME/.agents/skills"
cp -R .agents/skills/apple-native-design-26 "$HOME/.agents/skills/"
```

Some local Codex setups also scan `$HOME/.codex/skills`; use the directory that
your Codex installation lists in its skills panel.

## Source Policy

The skill references official Apple design and developer resources, including
Apple Design Resources, Human Interface Guidelines, SF Symbols, Icon Composer,
and Apple iOS/macOS 26 UI kits.

It does not vendor, copy, or redistribute Apple or Sketch assets. Official UI
kits are treated as live reference material only.

## License

Apache-2.0. This is a permissive open-source license with an explicit patent
grant, which is a good default for reusable developer tooling and workflow
assets.
