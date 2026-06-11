# SwiftUI 26 Design Reference

Use this file as the source map and design rulebook for SwiftUI iOS 26,
iPadOS 26, and macOS 26 design work. Consult the linked official documentation
live when exact API names, availability, or platform guidance matters.

## Official Sources

- SwiftUI technology overview:
  https://developer.apple.com/documentation/technologyoverviews/swiftui
- Design Resources:
  https://developer.apple.com/design/resources/
- Adopting Liquid Glass:
  https://developer.apple.com/documentation/TechnologyOverviews/adopting-liquid-glass
- Liquid Glass technology overview:
  https://developer.apple.com/documentation/technologyoverviews/liquid-glass
- iOS 26 UI Kit on Sketch:
  https://www.sketch.com/s/f63aa308-1f82-498c-8019-530f3b846db9
- macOS 26 UI Kit on Sketch:
  https://www.sketch.com/s/7e5d41a8-dbde-4372-abf1-59792d73bc7c
- Human Interface Guidelines:
  https://developer.apple.com/design/human-interface-guidelines
- HIG materials:
  https://developer.apple.com/design/human-interface-guidelines/materials
- HIG layout:
  https://developer.apple.com/design/human-interface-guidelines/layout
- HIG navigation and search:
  https://developer.apple.com/design/human-interface-guidelines/navigation-and-search
- HIG tab bars:
  https://developer.apple.com/design/human-interface-guidelines/tab-bars
- HIG toolbars:
  https://developer.apple.com/design/human-interface-guidelines/toolbars
- HIG sidebars:
  https://developer.apple.com/design/human-interface-guidelines/sidebars
- HIG app icons:
  https://developer.apple.com/design/human-interface-guidelines/app-icons/
- SF Symbols:
  https://developer.apple.com/sf-symbols/
- Icon Composer:
  https://developer.apple.com/icon-composer/
- WWDC25 - Build a SwiftUI app with the new design:
  https://developer.apple.com/videos/play/wwdc2025/323/
- WWDC25 - Get to know the new design system:
  https://developer.apple.com/videos/play/wwdc2025/356/

## Source Notes

- The official design resources expose iOS/iPadOS 26 and macOS 26 UI kits,
  including Sketch links. Treat those files as visual references, not vendored
  assets.
- The provided Sketch links identify as `iOS 26 UI Kit` and
  `macOS 26 UI Kit`. Use them when a task depends on exact component
  shape, spacing, or visual treatment.
- SF Symbols should be the default icon source for interface actions because
  symbols align with San Francisco, text scale, localization, mirroring, and
  platform rendering.
- Icon Composer is the relevant tool for layered Liquid Glass app icons across
  SwiftUI-supported platforms.

## SwiftUI 26 Design Model

- Native structure is the design system's foundation. Prefer standard SwiftUI
  navigation, tab, toolbar, search, sheet, popover, menu, form, list, sidebar,
  inspector, and control APIs before custom drawing.
- Content should remain primary. Liquid Glass and scroll edge effects clarify
  where controls and content meet; they are not decorative overlays and should
  not darken or block content.
- Persistent UI and contextual UI must stay separate. Persistent elements such
  as tab bars can hold persistent accessories, but screen-specific actions
  belong near the content they affect.
- Use one clear primary action per decision surface. Keep it visually distinct
  from secondary actions through native placement, semantic tint, or prominent
  button style.
- Use system-adaptive typography, color, materials, and symbols. Avoid fixed
  light backgrounds, one-note palettes, and custom icon systems unless the app
  already owns them.

## Native Structure Checklist

- Does the app use the native container for the job?
  `TabView`, `NavigationStack`, `NavigationSplitView`, `List(selection:)`,
  `Form`, `sheet`, `popover`, `Menu`, `toolbar`, `searchable`, `inspector`,
  commands, and settings scenes should be preferred before custom containers.
- Is the search attachment level correct?
  App-wide search belongs on the app shell or split view; feature-local search
  belongs near the feature container.
- Are sidebars, inspectors, toolbars, tabs, sheets, and popovers still native
  enough to preserve keyboard, pointer, focus, accessibility, and presentation?
- Are reusable components backed by real state and variants rather than static
  screenshot-only values?
- Are custom controls wrapping native controls where possible?

## Navigation, Tabs, And Search

- Use tabs for persistent top-level sections. Do not use tabs for temporary
  filters, step controls, or screen-local actions.
- Use `NavigationStack` for drill-in flows and explicit route state.
- Use `NavigationSplitView` for multi-column iPad/macOS hierarchies where
  sidebar selection and detail content should remain visible.
- Search has two main SwiftUI 26 patterns:
  toolbar search, and a dedicated search tab/page.
- Attach `searchable` to the container matching the scope. App-wide split-view
  search belongs on `NavigationSplitView`; tab-wide search belongs on `TabView`
  when using a search-role tab.
- On iPhone, toolbar search can adapt toward the bottom of the display or
  minimize to a toolbar button. On iPad and Mac, app-wide search commonly
  appears in the top-trailing toolbar area.
- If search is secondary, prefer `searchToolbarBehavior(.minimize)` over a
  custom search button plus fake field.
- If search is a dedicated app section, give the tab a search role and provide
  useful browse suggestions before the user types.

## Toolbars And Controls

- Use system toolbar grouping first. On macOS and iPad, group commands with
  native toolbar placement and `ToolbarSpacer` rather than custom chrome.
- Keep toolbar commands compact and action-oriented. Do not place dense
  settings, long labels, or content metadata directly in the toolbar.
- Use `badge` for toolbar status when the item naturally owns the count or
  notification state.
- Use `sharedBackgroundVisibility` only when an item should intentionally stand
  apart from a shared toolbar background.
- Prefer `Label` for menu and toolbar actions so symbol placement, localization,
  and accessibility stay native.
- Bordered buttons in the new design trend toward capsule shape at larger
  sizes; macOS mini/small/medium controls preserve denser rounded-rectangle
  treatment.
- Use `controlSize` deliberately. Inspectors, settings, and dense tool panes
  usually need smaller controls than primary content surfaces.
- For sliders with discrete values, pass `step` or provide ticks. For values
  that expand around a baseline, use a neutral value when the API is available.

## Liquid Glass And Scroll Edges

- Use Liquid Glass on meaningful controls and system surfaces, not as ambient
  decoration.
- Keep glass visually separated from content. Controls should sit on a system
  material or coordinated glass surface, not directly on busy content.
- Avoid mixing or stacking scroll edge effects. Use one edge treatment per view;
  split panes can each have their own when heights align.
- Soft scroll edge treatment is the default fit for most iOS/iPadOS interactive
  controls. Harder treatment is more suitable on macOS when text, table headers,
  or controls need a stronger boundary.
- Use `GlassEffectContainer` for adjacent custom glass elements that should
  coordinate visually.
- Use stable `glassEffectID` values only where morphing or matched transitions
  are visible and semantic.
- Use `backgroundExtensionEffect` for expansive visual content, hero imagery,
  or tinted surfaces that should extend behind an inset sidebar while keeping
  the subject centered.
- Use `ConcentricRectangle` when a custom glass/card shape needs to align with
  the system's concentric corner treatment.

## Minimum SwiftUI Liquid Glass Patterns

Use native system styles before custom glass:

```swift
Button("Done", action: complete)
    .buttonStyle(.glassProminent)

Button("Options", action: showOptions)
    .buttonStyle(.glass)
```

Group adjacent custom glass controls:

```swift
GlassEffectContainer(spacing: 8) {
    HStack(spacing: 8) {
        Button(action: run) {
            Label("Run", systemImage: "play.fill")
        }
        .buttonStyle(.glassProminent)

        Button(action: stop) {
            Label("Stop", systemImage: "stop.fill")
        }
        .buttonStyle(.glass)
    }
}
```

Use explicit shapes for non-default glass surfaces:

```swift
content
    .padding()
    .glassEffect(.regular, in: .rect(cornerRadius: 16))
```

Use matched glass identity only when a visible relationship exists:

```swift
@Namespace private var glassNamespace

control
    .glassEffectID("primary-action", in: glassNamespace)
```

Gate SwiftUI 26-only APIs when the project targets earlier OS versions:

```swift
if #available(iOS 26, macOS 26, *) {
    modernGlassView
} else {
    fallbackMaterialView
}
```

## App Icons And Symbols

- Use SF Symbols for interface actions unless the app already has a coherent
  symbol system. Symbols should align with text, weight, scale, localization,
  and reading direction.
- Use animation and multi-layer symbol variants only when they clarify state or
  interaction.
- For app icons, use Icon Composer or its layered-icon model. Create a single
  layered source that adapts across appearance modes and can export flattened
  marketing versions when needed.
- Do not hand-paint Liquid Glass icon effects into ordinary UI controls.

## SwiftUI 26 Visual Checklist

- Prefer system-adaptive colors and semantic foreground styles.
- Use Liquid Glass for meaningful controls and system surfaces, not ambient
  decoration.
- Keep glass readable. Avoid placing dense text over busy media or highly
  detailed content.
- Group related custom glass controls together with stable identity when they
  visually coordinate.
- Avoid nested cards, nested glass panels, decorative floating blobs, fake blur
  bars, and hand-built sidebars or inspectors.
- Let content hierarchy, native chrome, spacing, typography, and controls carry
  the design before adding custom visuals.
- Use accent color for semantic emphasis or primary action, not as blanket
  decoration.

## Platform Checks

### iOS and iPadOS

- Top-level sections use native tabs when persistent navigation is needed.
- Drill-in flows use `NavigationStack` with explicit route state.
- Floating bars, bottom accessories, sheets, menus, and system controls keep
  important content readable and reachable.
- Dynamic Type, safe areas, orientation, multitasking, keyboard, and pointer
  states are considered.
- Icon-only controls have labels or accessibility labels.
- Permission prompts and destructive actions appear at the point of need and
  provide a clear reason, confirmation, and recovery path.

### macOS

- App shells use desktop navigation patterns rather than touch-first stacked
  flows when a sidebar/detail or inspector model is more natural.
- Toolbar grouping, search, commands, menus, keyboard shortcuts, and settings
  are discoverable.
- Sidebar rows stay scannable. Put dense metadata in detail or inspector
  surfaces instead of making every sidebar row a card.
- Inspectors are contextual and lighter than the content they inspect.
- Minimum window size, compact widths, hover, focus, and keyboard navigation
  are verified.
- Menus and keyboard shortcuts expose primary desktop actions. Settings live in
  a settings scene or system-appropriate preferences surface, not as ordinary
  content navigation.

## Verification

- Build against the target SDK and fix availability problems directly.
- Run the app or preview the relevant view before claiming visual fidelity.
- Inspect screenshots when the request is visual: check overlap, clipping,
  glass readability, toolbar grouping, sidebars, inspectors, compact widths,
  and text inside controls.
- For reviews, lead with concrete findings and include file paths and line
  numbers when code is available.
