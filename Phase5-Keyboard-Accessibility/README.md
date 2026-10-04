# DPMIS Accessibility Audit — Phase 6 Keyboard-Only Testing

## Scope

Phase 6 tested the DPMIS registration page using keyboard navigation only. The audit focused on Tab/Shift+Tab navigation, select operation, CAPTCHA refresh, navigation controls, dependent dropdowns, DAB/TAB controls, focus order, and keyboard traps.

## Overall Result

The page is generally keyboard operable. Interactive controls can be reached in a logical order, native selects can be operated with the keyboard, and no keyboard trap was observed.

## Passed Checks

- Interactive controls were reachable using `Tab`.
- Focus order generally followed the visible page flow.
- No important interactive control was observed to be skipped.
- No keyboard trap was observed.
- Native select controls could be opened and changed using keyboard keys.
- Province → Division → District → Medical Board dependent selects worked during the successful retest.
- CAPTCHA refresh was reachable with `Tab` and could be activated with `Enter`.
- DAB/TAB hospital selectors were keyboard operable.
- Navigation/Login controls were keyboard reachable and usable.
- Reaching the end of the page and continuing with `Tab` returned focus to the beginning of the page, which is normal browser focus cycling.

## Confirmed Keyboard-Related Issue

### Visually disabled DAB/TAB map links remain keyboard focusable

Before a hospital is selected, the two map links visually appear disabled. Previous DOM inspection showed that they:

- use a visual `disabled` class
- use `pointer-events: none`
- have reduced opacity
- do not expose `aria-disabled="true"`
- do not use `tabindex="-1"`
- have a computed `tabIndex` of `0`

Keyboard testing confirmed that focus still lands on:

- `View DAB Location on Google Map`
- `View TAB Location on Google Map`

This confirms a mismatch between the visual disabled state and the keyboard/programmatic state.

**Status:** Confirmed accessibility issue  
**Relevant WCAG:** 4.1.2 — Name, Role, Value

## Non-Reproducible Observation

During the first keyboard attempt, selecting Punjab did not populate the Division options. After reloading and repeating the same interaction, the dependent dropdowns populated correctly.

Because the behavior was not reproducible during the immediate retest, it was not classified as an accessibility violation.

## Phase 6 Conclusion

Keyboard support is one of the stronger areas of the current page. The main registration flow, native selects, navigation, CAPTCHA refresh, and DAB/TAB selectors can all be operated without a mouse. The key exception is the DAB/TAB Google Maps controls, which appear disabled visually but remain in the keyboard tab order.
