---
name: principle-worst-case-data
description: Test UI against the realistic worst case of every value it renders: long names, unbreakable strings, missing fields, counts of one, empty and huge lists, long labels, non-Latin text, emoji. Use when stress-testing a component or hunting edge cases.
---

# Worst-Case Data

Demo data is chosen to make the design look good: names that fit, counts that never need separators, every optional field filled. Undo that choice, one field at a time.

## Rules

- **Plausible or schema-backed, never random.** Each value is a realistic example or the actual limit from the validation schema, database column, or API contract. `"aaaa..."` proves nothing and gets dismissed. If you find no limit, say "unbounded" and test something believable.
- **Change the data, not the component.** Enter the worst case through the same boundary the demo data does: the fixture, the mock, the props, the API stub. Never hand-edit markup to force a break.
- **One dataset, many failures.** A single worst-case dataset should hit every applicable row at once; spread different failures across the first rows since that is what is on screen.
- **Cover more than one dataset.** Empty (zero items), one (and every count exactly 1), and huge (the realistic upper bound, 1,000+ rows if unpaginated).
- **Report before fixing.** Some breaks are design decisions. List them all with a proposed fix, then stop.

## What to check

At the component's real container width, then at 320px and the widest layout; with browser zoom at 200%; in dark mode and RTL if supported.

## Failure signatures

| What you see | Cause | Fix |
| --- | --- | --- |
| Avatar squished to an oval | Flex child shrinking | `flex-shrink: 0` on fixed-size boxes |
| Text overflows instead of wrapping | Flex/grid child `min-width: auto` | `min-width: 0` on the text column |
| Email or URL runs past the edge | No break opportunities | `overflow-wrap: anywhere` |
| Trailing action pushed off-screen | Middle content took the space | `min-width: 0` on the middle, `flex-shrink: 0` on the action |
| Badge wraps to two lines | Badge allowed to shrink | `white-space: nowrap; flex-shrink: 0` |
| Wrong initials, broken emoji initial | Naive `split(' ')[0][0]` | Grapheme-aware initials, first plus last word, fallback icon |
| Orphaned dash or empty line | Placeholder for a missing field | Omit the line or reserve its height |
| "1 members", "0 member" | Hardcoded plural | `Intl.PluralRules` |
| Numbers jitter, columns misalign | Proportional figures | `font-variant-numeric: tabular-nums` |
| `NaNs`, raw digits | Raw number rendered | `Intl.NumberFormat`, guard null |
| Diacritics or tall scripts clipped | Tight line-height with overflow hidden | Looser line-height or no clipping |
| Broken-image icon | No `onError` fallback | Fall back to initials |
| Long translated label overflows | Fixed-width control | Width from content with a `min-width` |
| 1,000 rows stutter | Every row rendered | Virtualize or paginate |

## Truncate, wrap, or clamp

Decide per field, not globally:

- **Wrap** what identifies something: names, titles in a detail view.
- **Truncate at the end** for secondary metadata: role, description, preview. Pair with a way to see the full value.
- **Truncate in the middle** when items differ at the end: file names, emails sharing a domain, paths, hashes.
- **Clamp** multi-line previews.
- **Never truncate** numbers, amounts, or dates the user compares.
