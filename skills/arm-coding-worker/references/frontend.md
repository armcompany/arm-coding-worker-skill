# Frontend implementation

Before creating UI, locate the existing Design System: tokens, colors, typography, spacing, radius, elevation, components, layouts, icons, responsive rules, forms, dialogs, cards, inputs, and buttons. Inspect nearby screens and tests for composition conventions. Reuse these primitives and styling strategy, including existing CSS or Tailwind conventions.

An explicitly supplied parent Design System is the implementation authority within task scope. If it conflicts with current components, surface the concrete incompatibility; do not silently introduce a second system or redesign unrelated screens. In greenfield work, implement the supplied design or establish only the primitives needed for the current feature.

Trace route → component → state/form → API client → contract where applicable. Include loading, error, empty, success, and validation states relevant to the flow. Follow existing state management and data-fetching patterns. Preserve keyboard navigation, focus, semantics, labels, and responsive behavior. Avoid adding a global state library for a local interaction.

When browser tooling is available and the change warrants it, open the actual application, exercise the affected interaction and failure states, inspect rendering at relevant viewport sizes, and check console/network failures. Use keyboard and basic accessibility checks; a screenshot alone does not prove interactivity. Validate compatibility with supported browsers when affected.

A copy-only edit usually needs targeted checks, not an entire product redesign. New screens need route reachability and actual data/state behavior, not only component compilation. Report unavailable browser verification separately from passing static checks.
