# DPMIS Accessibility Audit — Phase 4 Names, Roles & States

## Scope

Phase 4 reviewed important interactive controls using the **Role → Name → State** model. The focus was on select controls, navigation controls, CAPTCHA refresh, verification links, and DAB/TAB map actions.

## Confirmed Findings

### 1. Core select controls do not have accessible names
The following native `<select>` elements have no associated native label or ARIA naming mechanism:

- `#optr`
- `#province`
- `#division`
- `#district`
- `#board`

Their native roles are correct, but their purpose is not programmatically named.

**Status:** Confirmed accessibility violation  
**Primary WCAG:** 4.1.2 — Name, Role, Value

---

### 2. CAPTCHA refresh button has a non-descriptive accessible name
The CAPTCHA refresh control is:

```html
<button type="button" ...>↻</button>
```

It has no `aria-label` or `title`, so its accessible name is effectively the symbol `↻`, which does not clearly communicate the control's purpose.

**Status:** Confirmed meaningful-label issue  
**Relevant WCAG:** 2.4.6 — Headings and Labels

---

### 3. DAB/TAB map links appear disabled visually but remain programmatically active/focusable
Both map links use a visual `disabled` class, `pointer-events: none`, and reduced opacity, but:

- they have no `aria-disabled="true"`
- they have no `tabindex="-1"`
- their computed `tabIndex` is `0`
- their `href` remains `#`

This means the disabled state is not exposed consistently to assistive technology and the links remain keyboard focusable.

**Status:** Confirmed state/semantics issue  
**Primary WCAG:** 4.1.2 — Name, Role, Value

---

### 4. Navigation toggle contains a nested interactive link
The navigation toggle is a native `<button>` with `aria-label="Toggle navigation"` and `aria-expanded="false"`, but it contains a clickable `<a>` element for **Login** inside the button.

Nested interactive controls create conflicting semantics and can cause confusing keyboard and assistive-technology behavior.

**Status:** Confirmed semantic/interaction issue  
**Relevant WCAG:** 4.1.2 — Name, Role, Value; keyboard behavior to be verified in later phases

## Passed Checks

- The verification image links receive meaningful names from their image `alt` text:
  - `Verification`
  - `Himmat Card Verification`
- Separate text links for those same destinations also have meaningful link text.
- The **REGISTER** control is a native submit button with clear visible text.
- The navigation toggle exposes `aria-expanded` and `aria-controls`, which are appropriate state/relationship attributes for a collapsible navigation control.

## Notes for Later Phases

- Keyboard behavior of the nested navigation button/link will be tested in Phase 6.
- Focusability and activation behavior of the visually disabled map links will also be tested in Phase 6.
- CAPTCHA behavior and alternatives will receive a dedicated review in Phase 10.
- Form labeling, required states, instructions, and validation relationships will be reviewed comprehensively in Phase 5.

## Phase 4 Conclusion

Phase 4 confirmed that several controls use correct native roles, but important accessibility problems remain in their names and states. The strongest issues are the unnamed select controls, non-descriptive CAPTCHA refresh button, visually disabled but keyboard-focusable map links, and nested interactive navigation markup.
