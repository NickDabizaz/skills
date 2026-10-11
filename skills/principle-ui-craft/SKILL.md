---
name: principle-ui-craft
description: The invisible details that make an interface feel right: press feedback, entrance scale, origin-aware popovers, tooltip timing, interruptible transitions, blur to mask crossfades, and stagger. Use when building or reviewing any interactive component.
---

# UI Craft

Most details users never consciously notice. That is the point. When a feature behaves exactly as someone assumes it should, they proceed without a second thought.

## Component rules

- **Buttons must feel responsive.** Add `transform: scale(0.97)` on `:active` with a short `ease-out` transition. Apply to any pressable element; keep the scale subtle (0.95-0.98).
- **Never animate from `scale(0)`.** Nothing in the real world appears from nothing. Start from `scale(0.9-0.97)` plus `opacity: 0`.
- **Make popovers origin-aware.** Popovers, dropdowns, menus, and tooltips scale in from their trigger, not from center. Set `transform-origin` to the trigger. Modals are the exception: they stay centered because they are not anchored to a trigger.
- **Tooltips: skip delay and animation on subsequent hovers.** Delay the first appearance to avoid accidental activation, then open adjacent tooltips instantly with no animation.
- **Use transitions over keyframes for interruptible UI.** Transitions retarget mid-animation; keyframes restart from zero.
- **Use blur to mask imperfect crossfades.** When two states swap and the crossfade looks off, a subtle `filter: blur(2px)` during the transition blends them so the eye reads one transformation. Keep blur under 20px; heavy blur is expensive.
- **Animate enter states with `@starting-style`** where supported, so entry needs no JavaScript.
- **Stagger group entrances** with 30-80ms between items. Stagger is decorative; never block interaction while it plays.
- **Asymmetric timing.** Slow where the user is deciding (a hold), snappy where the system responds (release).

## Performance

- Animate `transform` and `opacity` only. They skip layout and paint and run on the GPU. Animating `width`, `height`, `margin`, `padding`, or `top` triggers all three.
- Do not drive a child's transform from a CSS variable on the parent; it recalculates styles for every child. Set `transform` on the element directly.
- Shorthand animation properties in some libraries are not hardware-accelerated under load; use the full `transform` string.

## Accessibility

- Honor `prefers-reduced-motion` with a gentler variant, not zero: keep opacity and color, drop movement.
- Gate hover motion behind `@media (hover: hover) and (pointer: fine)`; touch fires false hovers.

## Review checklist

| Issue | Fix |
| --- | --- |
| `transition: all` | Name the exact properties |
| `scale(0)` entry | `scale(0.95)` + `opacity: 0` |
| `ease-in` on UI | `ease-out` or a strong custom curve |
| `transform-origin: center` on a trigger-anchored popover | Set it to the trigger (modals exempt) |
| Animation on a keyboard action | Remove it |
| UI duration over 300ms | Reduce to 150-250ms |
| Ungated hover motion | Add the hover and pointer media query |
| Keyframes on a rapidly-triggered element | Use transitions |
| Everything entering at once | Add a 30-80ms stagger |
