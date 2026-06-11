# UX Contract

Use this before building or auditing a SwiftUI-native surface. A visually native
screen is not a good SwiftUI experience if the task flow, state model, recovery,
or accessibility path is weak.

## Required UX Frame

Before implementation, define these in notes or in the plan:

- Target user and context: who is using this surface, on which device, and in
  what posture.
- Primary job: the one task the surface must make obvious and fast.
- Entry points: where the user arrives from, including deep links,
  notifications, menu commands, tabs, search, or document/window launch.
- Happy path: the shortest successful flow from entry to completion.
- Primary action: the one action that completes or advances the job.
- Secondary actions: supporting actions that must not compete with the primary
  action.
- Contextual actions: actions tied to a selection, row, document, object, or
  inspector state.
- Completion signal: what confirms success and what remains visible afterward.

## Information Architecture

- Persistent destinations belong in tabs, sidebars, windows, or document
  structures. Contextual actions belong near the selected content.
- Settings and preferences belong in a platform-appropriate settings surface,
  not as ordinary content screens.
- Search should cover the scope implied by its placement. If it appears at the
  app shell, make most app content searchable; if it is feature-local, keep it
  visually and structurally local.
- Inspectors should reflect the current selection and expose contextual
  controls. Do not use inspectors for unrelated app-wide settings.
- Empty states should explain the current scope and provide the next useful
  action. Avoid marketing copy in operational app surfaces.

## State Coverage

For each interactive surface, account for:

- Loading and refresh.
- Empty and first-run.
- Error with retry or recovery.
- Offline or unavailable dependency when relevant.
- Permission needed, denied, and changed later.
- Unsaved changes or interrupted flow.
- Disabled actions with an understandable reason.
- Selected, hover, focus, pressed, and keyboard navigation states where the
  platform supports them.
- Destructive action confirmation and undo or recovery where practical.

## Platform UX Rules

### iOS and iPadOS

- Keep primary actions within reach and tied to the current task.
- Respect safe areas, Dynamic Type, orientation, split view, external keyboard,
  pointer, and multitasking.
- Do not hide essential actions behind gestures alone.
- Use sheet, menu, confirmation dialog, or navigation according to task weight:
  lightweight choice, destructive confirmation, or full-screen focus.
- Ask for permissions at the point of need with a reason tied to user benefit.

### macOS

- Expose primary commands through menus, toolbar, contextual menu, and keyboard
  shortcuts when appropriate.
- Preserve selection-driven workflows: sidebar selection, table selection,
  detail pane, inspector, and document/window scope.
- Keep main windows useful at minimum size and comfortable at common desktop
  widths.
- Use hover, focus ring, default button, cancel action, and keyboard traversal
  deliberately.
- Do not port iPhone-first stacked flows when a split view, inspector, settings
  scene, or document window is more natural.

## Done Criteria

- A user can complete the primary job without reading explanatory UI text.
- The primary action, current selection, and current scope are visually clear.
- Every non-happy path has a visible recovery route or explicit explanation.
- Keyboard and assistive technology users can reach the same actions.
- The final response includes the UX states verified or the specific UX states
  still unverified.
