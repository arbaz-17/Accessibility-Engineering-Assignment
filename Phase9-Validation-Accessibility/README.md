# DPMIS Accessibility Audit — Phase 11 Validation & Error Accessibility

## Scope

Phase 11 reviewed required-field validation, browser error messages, error associations, invalid-state attributes, recovery guidance, and the distinction between accessibility problems and general data-validation quality.

## Confirmed Findings

### 1. Required fields are not clearly identified before submission
The DOM marks these controls as required:

- Name
- CNIC / B-Form
- CRMS
- Phone number
- Password
- Confirm Password
- CAPTCHA

However, the page does not provide a clear visible convention that distinguishes required fields from optional fields before the user attempts submission.

**Status:** Confirmed accessibility/usability issue  
**Relevant WCAG:** 3.3.2 — Labels or Instructions

### 2. Error guidance and programmatic associations are weak
For invalid required controls, the DOM showed:

- native browser validation messages such as `Please fill out this field.`
- no `aria-invalid`
- no `aria-describedby`
- no detected inline error elements
- no detected `role="alert"`
- no detected `aria-live`
- no error summary

The page therefore relies heavily on native browser constraint validation rather than providing a structured inline error system.

This is especially problematic for controls already confirmed to lack programmatic labels, because generic browser messages can be harder to interpret when the field itself is not clearly named.

**Status:** Confirmed weak error communication; consolidate with the existing form-labeling issue rather than double-counting every field  
**Relevant WCAG:** 3.3.1 — Error Identification; 3.3.2 — Labels or Instructions

## Passed / Positive Checks

- Empty submission is prevented by native browser validation.
- Required controls use the native `required` attribute.
- Browser validation messages are generated for invalid required fields.
- Email is **not** marked `required` in the initial DOM.
- Province, Division, District, and Medical Board are also not marked `required` in the initial DOM.

## Validation Quality Notes — Not Counted as Separate Accessibility Violations

- CNIC has `maxlength="13"` but no HTML `pattern`.
- CRMS has `maxlength="14"` but no HTML `pattern`.
- Phone has `maxlength="11"` but no HTML `pattern`.
- These fields may also use client-side input masking, so lack of a `pattern` attribute alone is not treated as an accessibility violation.
- General data-format enforcement is a validation/business-rule concern unless the expected format or recovery guidance is inaccessible.

## Focus Handling Note

Manual testing suggested that failed submission did not provide an obvious custom focus-management or error-summary experience. Because the browser's native constraint-validation UI can manage focus itself, this was not recorded as a separate confirmed WCAG failure without a dedicated programmatic focus check.

## Phase 11 Conclusion

The form blocks empty submission using native browser validation, which is positive. The accessibility weakness is that users are not clearly told which fields are required before submission, and the page provides no structured inline error relationships, error summary, or live error communication. These shortcomings are most significant when combined with the already-confirmed missing labels on several core form controls.
