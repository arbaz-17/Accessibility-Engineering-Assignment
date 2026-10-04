# DPMIS Accessibility Audit — Phase 9 Zoom & Responsive Accessibility

## Scope

Phase 9 reviewed the DPMIS registration page at **200% browser zoom** and at a **narrow/mobile viewport**. The focus was on reflow, clipping, overlap, horizontal scrolling, form usability, navigation availability, CAPTCHA layout, and the DAB/TAB section.

## 200% Zoom Results

### Passed / Usable
- No general text clipping was observed.
- Form controls remained available and usable.
- No horizontal page scrolling was required.
- CAPTCHA remained usable.
- DAB/TAB controls remained usable.

### Confirmed Visual/Reflow Problem
Near the end of the registration form, the **voice/instruction area overlaps the Register / Already registered area** at 200% zoom.

This creates a visual collision even though the page remains generally operable.

**Status:** Confirmed zoom/reflow issue  
**Relevant WCAG:** 1.4.10 — Reflow (final conformance wording should note that the exact CSS viewport width was not recorded)

### Additional Observation
The navigation becomes unusually tall and poorly arranged at 200% zoom. This is a responsive-quality concern, but it was not separately classified as a violation because the navigation remained usable.

## Mobile / Narrow Viewport Results

### 1. Navigation content disappears
On the tested mobile layout, only the Login control remained visible. The desktop **Register** and **Instructions** navigation items were no longer visible, and no separate menu control was observed that exposed them.

**Status:** Confirmed responsive loss of visible navigation in the tested state  
**Relevant WCAG:** 1.4.10 — Reflow / preservation of content and functionality

### 2. Registration form becomes visually cramped
The form remains readable and usable, but internal spacing becomes very tight and controls/content appear pressed against the form boundaries.

**Status:** Usability/design concern; not counted as a separate accessibility violation by itself

### 3. Dropdown UI extends outside the mobile viewport
During mobile testing, dropdown content extended beyond the visible screen boundary rather than fitting cleanly within the viewport.

**Status:** Confirmed responsive usability issue observed during testing; retain as part of the reflow/responsive finding rather than creating a duplicate issue

### Passed / Usable
- Main informational content remained readable.
- Verification and Himmat Card cards remained visible.
- The registration form remained generally usable.
- CAPTCHA continued to work.
- DAB/TAB section remained usable.
- No general horizontal page scrolling was observed.

## Phase 9 Conclusion

The page remains broadly usable under zoom and mobile conditions, but responsive behavior is not fully robust. The strongest issues are the overlap around the voice/registration controls at 200% zoom, loss of navigation items in the mobile layout, and dropdown content extending beyond the mobile viewport. These should be consolidated into a responsive/reflow finding rather than reported as several unrelated violations.
