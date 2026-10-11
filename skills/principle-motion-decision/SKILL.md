---
name: principle-motion-decision
description: Decide whether a UI element should animate at all, and if so its purpose, easing, and duration. Use before writing any animation, and when reviewing one.
---

# Motion Decision

Before any animation, answer these in order.

## 1. Should it animate at all?

Frequency decides.

| Frequency | Decision |
| --- | --- |
| 100+ times/day (keyboard shortcuts, command palette toggle) | No animation, ever |
| Tens of times/day (hover, list navigation) | Remove or make near-imperceptible |
| Occasional (modals, drawers, toasts) | Standard animation |
| Rare or first-time (onboarding, success, celebration) | The delight budget lives here |

Never animate keyboard-initiated actions. They are repeated hundreds of times a day, and animation makes them feel slow and disconnected.

## 2. What is the purpose?

Name one before continuing: **feedback** (the interface heard the user), **spatial consistency** (where something came from or went), **state indication** (a state change made legible), **preventing a jarring change** (bridging content that would teleport), **explanation** (marketing or onboarding only), or **delight** (rare tier only). If you cannot name it in one of these words, do not animate.

Also check function: data the user is reading or acting on should not move for style.

## 3. Which easing?

- Entering or exiting -> `ease-out`.
- Moving or morphing on screen -> `ease-in-out`.
- Hover or color change -> `ease`.
- Constant motion (progress, marquee) -> `linear`.
- Default -> `ease-out`.

Never use `ease-in` on UI. It starts slow, delaying the moment the user is watching most. Built-in CSS easings are too weak; use strong custom curves:

```css
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);
```

When a curve is missing, take one from a curve library; do not hand-roll it.

## 4. How fast?

| Element | Duration |
| --- | --- |
| Press feedback | 100-160ms |
| Tooltips, small popovers | 125-200ms |
| Dropdowns, selects | 150-250ms |
| Modals, drawers | 200-500ms |

UI animations stay under 300ms. A 180ms dropdown feels more responsive than a 400ms one.

## Enter, exit, and interruption

- **Exit the way it entered.** Symmetric paths make swipe-to-dismiss feel obvious.
- **Transitions, not keyframes, for anything triggered rapidly** (toasts, toggles). Transitions retarget from the current value; keyframes restart from zero.
- **Springs for gestures**, because they carry velocity through an interruption.
- **Asymmetric timing** where the user is deciding: slow on the deliberate phase, snappy on the system response.

## Reduced motion

Reduced motion means fewer and gentler animations, not zero. Keep opacity and color changes that aid comprehension; drop movement and position changes.
