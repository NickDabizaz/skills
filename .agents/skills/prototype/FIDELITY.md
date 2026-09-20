# UI fidelity contract

Read when a supplied design or approved prototype governs UI work. The target is 1:1 visual and behavioural parity for the agreed screens, states, and viewports. Framework and library choices change code organisation, not this target.

## Establish the baseline

- **HTML/CSS**: inspect and run the supplied code with its fonts, images, icons, and styles. Reuse it as the starting point; adapt markup and event wiring to the target stack while preserving the rendered result and agreed behaviour.
- **JPG/PNG**: inspect the image at its original dimensions. Reproduce visible layout, spacing, typography, colours, assets, copy, and controls. Obtain missing assets or measurements when they affect fidelity; mark unavailable ones unresolved rather than silently substituting them. An image proves only the shown state and viewport: hidden behaviour and responsive layouts come from settled requirements, otherwise ask before building those parts.
- **Both**: compare the rendered code and image. If they disagree and the user has not selected authority, ask which governs, listing the differences together.

Read existing approvals before asking. Reconcile conflicts with `DESIGN.md` or requirements once, record the selected source and scoped exceptions in the plan, and update affected design tokens or patterns to the approved choice where `DESIGN.md` exists. Legacy projects keep the decision in their plan. A functional requirement absent from a screenshot still applies; a contradiction needs a decision. Existing library defaults never override the baseline silently.

## Preserve the agreement

The approved prototype is the implementation baseline; when the user proceeds directly from a supplied design, that approved design is the baseline. At approval, preserve an immutable copy of its source and assets (or a reproducible code revision with its run command). Keep original references. Assign a revised candidate its own version only after approval; existing tickets keep their version until their scope is reconciled. Record approval, source paths, version, and agreed cases in `baseline.md` beside the prototype, linking the plan rather than duplicating its inventory. Preserve older approved versions when editing the current entry point.

The plan's UX flow names each screen, its baseline path and version, approved viewports/states, and any explicit deviations. Keep the field and action inventory once, initially in the brief if present and then reconciled into the spec (or the agreed conversation plan):

- Fields, in display order: identifier, exact label, control type, required/optional, options, initial value, validation, and visible error.
- Actions and states: trigger, visible result, navigation, and empty/loading/error/success behaviour. Preserve agreed copy and representative data.

Extract known details from the artifacts; ask only for missing decisions. Differences between brief, prototype, and spec are reconciled before handoff. Tickets link the applicable screen contract and baseline and carry its acceptance criteria; they do not recreate the inventory. Behavioural criteria and render parity are both required. Later approved changes update the affected spec criteria and open tickets, not just the prototype file.

## Verify parity

Run the candidate UI and compare it with the baseline at every agreed viewport and state, using the same data, fonts, assets, browser, zoom, and device scale where reproducible. For images, match the captured viewport and document any unknown capture conditions. Wait for fonts and assets to load and settle animations before capturing.

Inspect paired screenshots side by side and with an overlay or image diff where available. Check geometry, spacing, typography, colours, borders, icons, imagery, copy, and responsive behaviour; exercise the field/action inventory separately. A screenshot of the candidate alone or a passing functional suite is not evidence of parity.

Keep evidence beside the ticket or prototype: baseline version, candidate code revision (or working-tree snapshot identifier), routes and commands, viewport/state/data, paired captures, differences, and their resolution. Review checks evidence against the current candidate; changes affecting the comparison require fresh captures. Backend-only work does not require another visual comparison when its UI output and data contract are unchanged.

Done means every agreed case was compared, every field/action matches, and no unapproved difference remains. Pixel differences from rendering noise must be identified and explained; a blanket similarity score cannot excuse missing fields or altered layout. Technical constraints require a specific user-approved deviation recorded before implementation. Missing render access, assets, or coverage means **unverified**, never a fidelity PASS: state what remains and obtain the missing evidence or an explicit change of scope before closure.
