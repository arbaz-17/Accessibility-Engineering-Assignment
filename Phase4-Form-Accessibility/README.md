# DPMIS Accessibility Audit — Phase 5 Form Accessibility

## Scope

Phase 5 reviewed the registration form controls for programmatic labels, required states, input types, autocomplete, instructions, grouping, and ID integrity.

## Confirmed Findings

### 1. Important form controls are not programmatically labelled
The following controls have visible nearby text or placeholders but no associated `<label>`, `aria-label`, or `aria-labelledby`:

- `#optr` — registration method
- `#cnic` — CNIC / B-Form
- `#crms` — CRMS / Birth Certificate
- `input[name="phoneno"]` — phone number
- `#province`
- `#division`
- `#district`
- `#board`
- `input[name="captcha"]`

This means visual text is not reliably exposed as the control's programmatic label.

**Status:** Confirmed accessibility violation  
**Relevant WCAG:** 1.3.1 — Info and Relationships; 3.3.2 — Labels or Instructions; 4.1.2 — Name, Role, Value where the control has no effective accessible name

### 2. Confirm Password has an unrelated third label
`#password_confirmation` is associated with three labels:

- `Confirm Password`
- Urdu translation
- `Instruction`

The `Instruction` label is incorrectly tied to the Confirm Password input and may be announced as part of that field's accessible name.

**Status:** Confirmed incorrect label association  
**Relevant WCAG:** 1.3.1 — Info and Relationships

## Positive Findings

- `Name`, `Email`, `Password`, and `Confirm Password` have explicit native labels.
- English and Urdu labels are both associated with those controls.
- `Name` uses `autocomplete="name"`.
- Password fields use `autocomplete="new-password"`.
- Email correctly uses `type="email"`.
- Password fields correctly use `type="password"`.
- Important required inputs use native `required`.
- `#dabSelect` and `#tabSelect` have proper associated labels.
- No duplicate IDs were detected.
- No fieldset issue was recorded; the current form does not contain a radio/checkbox group that clearly requires one.

## Items for Later Verification

- Email and phone do not expose autocomplete tokens such as `email` and `tel`; this will be treated as a potential improvement unless further evidence establishes a WCAG input-purpose failure.
- `CNIC` and `CRMS` are both marked `required` in the initial DOM even though the registration-method selector suggests conditional enablement. Dynamic behavior needs verification.
- Division, District, and Medical Board selects are initially enabled in the DOM even when they contain no options. Their keyboard and screen-reader behavior will be reviewed later.
- Important helper/instruction text is not connected through `aria-describedby`; this is included in the broader form-association review rather than counted as a separate violation.
- Validation/error associations will be tested in the dedicated error-validation phase.

## Phase 5 Conclusion

The strongest form-accessibility issue is inconsistent programmatic labelling. Several core registration fields show understandable visual text but do not expose that relationship to assistive technology. The form also contains an incorrect `Instruction` label association on the Confirm Password field. Native input types, required states, unique IDs, and the DAB/TAB selectors provide some positive implementation examples.
