# Native Component Map

Use this when choosing components, auditing a design, or implementing a
reusable Apple 26 surface. If `/Users/richardq/Documents/Components` exists,
use it as local implementation evidence for comparable SwiftUI patterns before
inventing a new component.

## Required Pattern

For any component catalog or reusable component, include:

- Component title and purpose.
- Native APIs used.
- Source path and symbol.
- Short code snippet proving the implementation uses real SwiftUI/AppKit
  structure.
- Supported states and layout variants.
- Verification evidence from build, runtime, screenshot, or tests when
  practical.

## Local Catalog Coverage

Canonical local catalog: `/Users/richardq/Documents/Components`

| Area | Native APIs | Reference implementation |
| --- | --- | --- |
| App shell | `NavigationSplitView`, `List(selection:)`, `.listStyle(.sidebar)`, `navigationSplitViewColumnWidth`, `scrollEdgeEffectStyle` | `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Catalog/ContentView.swift`, `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Layouts/AppShellDemoView.swift` |
| Inspector | `.inspector(isPresented:)`, `.inspectorColumnWidth`, `Toggle`, `Picker`, contextual selection state | `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Catalog/CatalogInspectorView.swift` |
| Toolbar and search | `toolbar`, `ToolbarSpacer`, `sharedBackgroundVisibility`, `badge`, `searchable`, `searchToolbarBehavior` | `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Catalog/ContentView.swift`, `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Layouts/ToolbarSearchDemoView.swift` |
| Floating command palette | `GlassEffectContainer`, `glassEffect`, `glassEffectID`, `glassEffectTransition`, `glassEffectUnion` | `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Components/FloatingGlassBar.swift` |
| Controls | `.buttonStyle(.glass)`, `.buttonStyle(.glassProminent)`, `Picker(.segmented)`, `Toggle`, `Slider(neutralValue:ticks:)` | `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Components/GlassControlCluster.swift`, `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Components/GlassStatusPill.swift` |
| Background and shape | `backgroundExtensionEffect`, `ConcentricRectangle`, `glassEffect`, semantic tint | `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Layouts/BackgroundShapeDemoView.swift` |
| Presentations | `.sheet`, `.popover`, `Form`, `controlSize` | `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Layouts/PresentationDemoView.swift` |
| Tabs and menus | `TabView`, tab items, `Menu`, `Label`, `keyboardShortcut` | `/Users/richardq/Documents/Components/Sources/LiquidGlassComponents/Views/Layouts/TabsMenusDemoView.swift` |

## Component Decisions

- Use `NavigationSplitView` for master/detail desktop shells and iPad layouts
  that benefit from visible hierarchy. Do not build a sidebar from a custom
  `HStack` unless SwiftUI cannot express required behavior.
- Use `List(selection:)` with `.listStyle(.sidebar)` for native sidebars,
  selection, keyboard behavior, and source-list density.
- Use `.inspector(isPresented:)` for contextual right-side detail panels tied
  to a selection or document state.
- Use root `.searchable` and `searchToolbarBehavior` for app-level search
  instead of placing a fake search field in content.
- Use toolbar items and `ToolbarSpacer` for command grouping. Use badges only
  where system toolbar items can own the state.
- Use `.sheet`, `.popover`, `Menu`, and confirmation dialogs for transient
  presentation. Do not replace them with custom overlay panels unless the
  design needs non-modal behavior SwiftUI cannot provide.
- Use `TabView` for persistent sections and `Menu` for command choices instead
  of custom segmented rows when the semantics are tabs or menus.
- Use native `Form`, `LabeledContent`, `Toggle`, `Picker`, `Slider`, `Button`,
  and keyboard shortcuts for settings and inspector controls.
- Use AppKit interop narrowly for window, panel, responder-chain, text-system,
  or other system behavior that SwiftUI cannot express cleanly.

## Minimum Snippets

```swift
NavigationSplitView {
    SidebarView(selection: $selection)
} detail: {
    DetailView(selection: selection)
}
```

```swift
.inspector(isPresented: $inspectorVisible) {
    InspectorView(selection: selection)
        .inspectorColumnWidth(min: 280, ideal: 320, max: 380)
}
```

```swift
.searchable(text: $searchText, placement: .toolbar)
.searchToolbarBehavior(.automatic)
```

```swift
TabView(selection: $selectedTab) {
    OverviewView()
        .tabItem { Label("Overview", systemImage: "square.grid.2x2") }
        .tag(AppTab.overview)
}
```
