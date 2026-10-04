# DPMIS Accessibility Audit — Phase 12 Dynamic UI & Screen-Reader Basics

## Scope

Phase 12 reviewed dynamic updates and the accessibility information exposed for dependent dropdowns, CAPTCHA refresh, status messages, and basic screen-reader/accessibility-tree behavior.

## Dynamic UI Findings

### No live/status regions were found
The page returned no elements using:

- `aria-live`
- `role="status"`
- `role="alert"`
- `aria-busy`

The Province → Division → District → Medical Board controls also expose no `aria-live`, `aria-busy`, or `aria-describedby` relationships.

When the dependent selections update, their option lists are populated dynamically, but no dedicated status mechanism was found to communicate that loading or completion state.

**Status:** Needs Verification / accessibility concern, not a standalone confirmed WCAG violation by itself.

The absence of a live region does not automatically fail WCAG. A failure would depend on whether an important status message or change needs to be communicated without moving focus.

## CAPTCHA Dynamic Behavior

The CAPTCHA image exposes:

```text
alt="CAPTCHA"
```

but no live-region or status semantics are attached to the image or refresh control.

The refresh button also has no descriptive `aria-label`.

Manual testing from earlier phases showed that:

- the refresh control is keyboard operable
- focus remains on the refresh control after refresh
- the CAPTCHA image changes successfully

The larger accessibility failure remains the lack of an equivalent non-visual CAPTCHA alternative, already recorded in Phase 10.

## Basic Screen-Reader / Accessibility-Tree Conclusions

Existing DOM and accessibility inspection already established several important screen-reader-facing issues:

- core registration selects have no accessible names
- CNIC, CRMS, phone, and CAPTCHA inputs lack programmatic labels
- the CAPTCHA refresh control has a non-descriptive name
- the Confirm Password field has an unrelated `Instruction` label association
- the page title is non-descriptive
- the main registration flow lacks a clear semantic heading structure

These findings were recorded in earlier phases and should not be duplicated as new Phase 12 violations.

## Phase 12 Conclusion

No new standalone accessibility violation was confirmed in Phase 12. The page does not expose live/status semantics for dynamic dropdown loading or CAPTCHA refresh, but the absence of those attributes alone is not enough to claim a WCAG failure. The main screen-reader-facing problems are already captured by the confirmed naming, labeling, semantic-structure, and CAPTCHA findings from earlier phases.
