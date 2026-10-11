---
name: principle-mobile-native
description: Make a web app feel native on a phone: the small CSS and meta fixes around hover, tap, viewport height, input zoom, scroll, safe areas, and status bar. Use when a web app is built for or reviewed on mobile, or when something feels wrong on a phone.
---

# Mobile Native

Most "janky on mobile" reports are not animation problems. They are a tap delay, a gray flash, or a hover state that will not let go. Most of these are one line. Emulation does not reproduce them; test on real hardware.

## Symptom to fix

| Problem | Fix |
| --- | --- |
| Hover state stuck after tap | Wrap in `@media (hover: hover) and (pointer: fine)` |
| Gray or blue flash on tap | `-webkit-tap-highlight-color: transparent` |
| Wrong layout height | `100dvh` for an app shell, `100svh` for a hero |
| Page zooms into an input | Inputs at 16px minimum; fix the cause, never disable zoom |
| Tap feels laggy | Feedback on pointer-down plus `touch-action: manipulation` |
| Pull-to-refresh hijacks scroll | `overscroll-behavior: none` on `html, body`, `contain` on inner scrollers |
| Content stops at the notch | `viewport-fit=cover` plus `env(safe-area-inset-*)` |
| Long-press selects control text | `user-select: none` on controls, never on body content |
| Carousel scrolls the wrong way | `touch-action: pan-y` (or `pan-x`) on the gesture surface |
| Status bar color wrong | One `theme-color` per `prefers-color-scheme` |
| Wrong on a phone but right in Chrome | Test on real hardware |

## Rules

- **Media queries over device sniffing.** `(hover)`, `(pointer)`, `env()`, `dvh` tell you what the device can do. Never branch on user agent or screen width to guess touch.
- **Touch and mouse are not exclusive.** Write for both at once; gate by capability.
- **Never disable zoom.** `user-scalable=no` and `maximum-scale=1` are accessibility failures.
- **Feedback on press, not release.** Native controls respond the instant a finger lands. Use `:active`, or `pointerdown`, not `click`.

## Baseline

```css
html {
  -webkit-tap-highlight-color: transparent;
  -webkit-text-size-adjust: 100%;
  overscroll-behavior: none;
}
input, textarea, select { font-size: 16px; }
button, a, [role="button"] {
  touch-action: manipulation;
  user-select: none;
}
@media (hover: hover) and (pointer: fine) {
  /* all :hover rules live here */
}
```
