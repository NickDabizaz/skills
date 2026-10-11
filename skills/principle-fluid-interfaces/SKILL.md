---
name: principle-fluid-interfaces
description: Make gesture-driven and interactive UI feel physical: direct manipulation, interruptibility, springs, velocity handoff, momentum, rubber-banding, and spatial consistency. Use when building or reviewing drag, swipe, sheet, or any touch interaction.
---

# Fluid Interfaces

An interface feels alive when motion starts from the current on-screen value, inherits the user's velocity, projects momentum forward, and can be grabbed and reversed at any instant. Springs make this natural because they are interruptible and velocity-aware.

## Response

Kill latency. Feedback on pointer-down, not on release. Audit debounces, artificial timers, and the tap delay. Feedback must be continuous during the interaction, not only at the end.

## Direct manipulation

When the user drags, the element stays glued to the finger and respects the offset from where they grabbed it. Use pointer capture so tracking continues outside the element. Track a short position and time history so you have velocity at release.

## Interruptibility (the most important principle)

Every animation must be interruptible and redirectable at any moment. Never lock out input during a transition. Always animate from the presentation (current) value, never the target. Avoid CSS transitions and keyframes for anything gesture-driven. When a gesture reverses, carry velocity through the re-target; do not hard-cut it. Decompose 2D motion into independent X and Y springs.

## Springs

Think in two designer parameters, not mass/stiffness/damping:

- **Damping ratio:** overshoot. `1.0` is critically damped, no bounce. Lower is bouncier.
- **Response:** how quickly it reaches the target, in seconds. Lower is snappier. This is not a fixed duration.

Start most UI at damping `1.0`. Add bounce (around `0.8`) only when the gesture itself carried momentum.

| Interaction | Damping | Response |
| --- | --- | --- |
| Move / reposition | `1.0` | `0.4` |
| Rotation | `0.8` | `0.4` |
| Drawer / sheet | `0.8` | `0.3` |

## Velocity handoff and momentum

When a gesture ends, the animation continues at the finger's exact velocity, so there is no seam. Project the resting position from velocity, like scroll deceleration, then snap to the target nearest that projection:

```
projected = current + (v / 1000) * d / (1 - d)   // d ~ 0.998
```

Then hand off the release velocity to the spring.

## Spatial consistency

Enter and exit along the same path. Anchor interactions to their source (set `transform-origin` to the trigger). Mirror the easing on reversible transitions.

## Boundaries

At an edge, resist progressively instead of stopping hard. A hard stop reads as frozen; continuous resistance reads as responsive with nothing more here. Apply damping that grows the further past the boundary the user drags.

## Frame smoothness

Keep per-frame change below the perception threshold. For very fast motion, a subtle blur encodes speed. Animate only compositor-friendly properties (`transform`, `opacity`) and hint with `will-change` where motion is imminent.
