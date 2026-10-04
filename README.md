## Accessibility Engineering - Week 11 Assignment

## GOVT Website - Disabled Person Management Information System (DPMIS)

# DPMIS Accessibility Audit — Final README

## Overview

This audit reviews the **Punjab Disabled Person Management Information System (DPMIS) Registration Page** for accessibility issues.

- **Target:** https://dpmis.punjab.gov.pk/register
- **Audit Date:** 4 October 2026
- **Browser:** Google Chrome 154.0.8037.93 (64-bit)
- **OS:** Windows 11
- **Standard Used:** WCAG 2.1 AA
- **Audit Type:** Public production website audit
- **Source Code Access:** None

No changes were made to the live government website. The work consists of **accessibility findings, evidence, keyboard verification, and recommended remediation only**.

---

## Methodology

The audit included:

- Lighthouse accessibility testing
- axe DevTools automated testing
- semantic HTML and landmark inspection
- accessible name / role / state inspection
- form accessibility review
- keyboard-only testing
- focus behavior testing
- color-contrast review
- 200% zoom testing
- mobile / narrow viewport testing
- CAPTCHA accessibility review
- validation and error review
- dynamic-content and basic screen-reader-oriented DOM inspection

---

## Automated Baseline

### Lighthouse

- **Accessibility Score:** 81 / 100

Main automated findings included:

- select controls without associated labels
- insufficient color contrast
- non-sequential heading structure
- missing main landmark
- possible multiple-label issue

### axe DevTools

- **Total Automatic Issues:** 20
- **Critical:** 5
- **Serious:** 15
- **Moderate:** 0
- **Minor:** 0

The 20 axe instances mainly represented:

- **5** select controls without accessible names
- **15** color-contrast failures

Automated results were consolidated by root cause rather than counted as separate violations.

---

# Consolidated Accessibility Findings

| ID | Severity | Finding | Main WCAG |
|---|---|---|---|
| A11Y-01 | High | Core registration controls lack programmatic labels / accessible names | 1.3.1, 3.3.2, 4.1.2 |
| A11Y-02 | Medium | Page title `SW&BM` does not describe the page purpose | 2.4.2 |
| A11Y-03 | Medium | Heading hierarchy does not clearly represent the page structure | 1.3.1 |
| A11Y-04 | Medium | CAPTCHA refresh button has a non-descriptive accessible name (`↻`) | 2.4.6 |
| A11Y-05 | Medium | DAB/TAB map links look disabled but remain keyboard focusable and do not expose disabled state | 4.1.2 |
| A11Y-06 | Medium | Navigation toggle contains a nested interactive Login link inside a button | 4.1.2 |
| A11Y-07 | Medium | Confirm Password input is incorrectly associated with an additional `Instruction` label | 1.3.1 |
| A11Y-08 | Medium | Multiple text/UI elements fail minimum contrast requirements | 1.4.3 |
| A11Y-09 | Medium | Zoom/mobile layouts cause overlap, missing navigation items, and dropdown overflow | 1.4.10 |
| A11Y-10 | High | Visual CAPTCHA has no equivalent non-visual CAPTCHA alternative | 1.1.1 |
| A11Y-11 | Medium | Required fields are not clearly identified before submission and error guidance is weak | 3.3.1, 3.3.2 |

---

## A11Y-01 — Missing Programmatic Labels / Accessible Names

Several important registration controls have visible nearby text but no associated `<label>`, `aria-label`, or `aria-labelledby`.

Affected controls include:

- registration-method select
- CNIC / B-Form
- CRMS / Birth Certificate
- phone number
- Province
- Division
- District
- Medical Board
- CAPTCHA input

This can make the form difficult to understand for screen-reader users, especially when several similar controls appear one after another.

**Recommended remediation:** associate every form control with a meaningful native `<label>` where possible.

---

## A11Y-02 — Non-Descriptive Page Title

The document title is:

```text
SW&BM
```

It does not clearly identify DPMIS or the Registration page.

**Recommended remediation:**

```html
<title>PWD Registration — DPMIS | Government of Punjab</title>
```

---

## A11Y-03 — Weak Heading Hierarchy

Observed hierarchy:

```text
H1  For Already Registered PWD
H1  Verification
H1  Himmat Card Verification
H3  DAB AND TAB LOCATION OR ADDRESS
H5  Urdu DAB/TAB heading
H5  District Assessment Board (DAB)
H5  Tehsil Assessment Board (TAB)
```

The main registration form has no clear primary heading, while secondary cards use top-level headings.

**Recommended remediation:** define one logical page hierarchy and use heading levels to represent structure rather than appearance.

---

## A11Y-04 — CAPTCHA Refresh Name

The refresh control is:

```html
<button type="button">↻</button>
```

It has no descriptive accessible name.

**Recommended remediation:**

```html
<button type="button" aria-label="Refresh CAPTCHA">↻</button>
```

---

## A11Y-05 — Disabled Map-Link State Is Not Exposed

The DAB/TAB Google Map controls visually appear disabled, but:

- they remain in the keyboard tab order
- `aria-disabled` is absent
- their computed `tabIndex` is `0`
- `href="#"` remains present

Keyboard testing confirmed that focus still lands on both links.

**Recommended remediation:** use a true button/link state that is not interactive until available, or expose `aria-disabled="true"` and remove it from normal activation/focus behavior where appropriate.

---

## A11Y-06 — Nested Interactive Navigation Markup

The navigation toggle contains a Login link inside a button:

```html
<button aria-label="Toggle navigation">
  <a href="/login">Login</a>
</button>
```

Nested interactive elements can create conflicting semantics and confusing keyboard/screen-reader behavior.

**Recommended remediation:** keep the navigation toggle and Login link as separate sibling controls.

---

## A11Y-07 — Incorrect Label Association

`#password_confirmation` is associated with:

- `Confirm Password`
- Urdu translation
- `Instruction`

The unrelated `Instruction` label may be announced as part of the field name.

**Recommended remediation:** remove the incorrect `for="password_confirmation"` association from the Instruction label and associate instruction content with the correct control/content.

---

## A11Y-08 — Insufficient Contrast

Confirmed examples include:

- information/video links: approximately **3.68:1**
- CAPTCHA refresh: approximately **2.80:1**
- DAB badge: approximately **2.41:1**
- TAB badge: approximately **3.04:1**
- DAB/TAB labels: approximately **4.48:1**

Normal text generally requires **4.5:1** under WCAG AA.

Disabled DAB/TAB map controls were not counted as contrast violations because inactive controls may be exempt.

---

## A11Y-09 — Zoom / Responsive Reflow Problems

At **200% zoom**:

- voice/instruction content overlaps the Register / Already Registered area
- navigation becomes poorly arranged, although still usable

At a **mobile/narrow viewport**:

- Register and Instructions navigation items disappear
- no equivalent menu control was observed to expose them
- the form becomes visually cramped
- dropdown content can extend outside the visible screen boundary

The page remained broadly usable, but the responsive implementation is not robust.

---

## A11Y-10 — CAPTCHA Has No Equivalent Non-Visual Alternative

The page uses a visual CAPTCHA:

```html
<img id="captcha-image" alt="CAPTCHA">
```

An audio player exists, but manual testing confirmed that it provides **general registration instructions only** and does not provide the current CAPTCHA challenge.

A user who cannot perceive the visual CAPTCHA may therefore be unable to complete registration.

**Recommended remediation:** provide an equivalent CAPTCHA challenge using a different sensory modality or another accessible anti-bot mechanism.

---

## A11Y-11 — Required Fields / Validation Communication

Native browser validation prevents empty submission, which is positive.

Required controls include:

- Name
- CNIC / B-Form
- CRMS
- Phone
- Password
- Confirm Password
- CAPTCHA

However:

- required fields are not clearly identified before submission
- no structured inline error system was observed
- no error summary was observed
- no `aria-describedby` error associations were found
- no dedicated `role="alert"` / `aria-live` error communication was found

The page relies heavily on browser-native messages such as:

```text
Please fill out this field.
```

**Recommended remediation:** clearly mark required fields, provide understandable inline errors, and programmatically associate error/help text with the affected control.

---

# Keyboard-Only Verification

Overall keyboard support was relatively strong.

### Passed

- interactive controls were reachable with `Tab`
- focus order was generally logical
- no keyboard trap was found
- native selects were keyboard operable
- Province → Division → District → Medical Board worked during retesting
- CAPTCHA refresh worked using keyboard input
- DAB/TAB selectors were keyboard operable
- navigation/Login controls were keyboard operable
- focus remained stable during dynamic dropdown loading and CAPTCHA refresh

### Keyboard Issue

The visually disabled DAB/TAB map links remained focusable, confirming the programmatic-state issue described in **A11Y-05**.

---

# Positive Accessibility Findings

The audit also identified several good behaviors:

- `<html lang="en">` is present
- native `<nav>` markup is used
- navigation list structure is valid
- native buttons and select controls are widely used
- no obvious clickable `div`/`span` controls were found
- important required inputs use native `required`
- Name uses `autocomplete="name"`
- password fields use `autocomplete="new-password"`
- DAB/TAB selects have proper labels
- duplicate IDs were not detected
- focus generally remains visible
- no keyboard trap was observed
- CAPTCHA refresh preserves focus
- general page content remains usable at 200% zoom
- no general horizontal page scrolling was observed

---

# Additional Concerns / Observations

These were recorded but not counted as standalone violations:

- no `<main>` / `role="main"` landmark was found
- no skip-to-main-content link was observed
- no `aria-live`, `role="status"`, `role="alert`, or `aria-busy` regions were found for dynamic dropdown loading
- some focus indicators inside form fields appeared lighter than others
- the first dependent-dropdown loading failure could not be reproduced after reload
- CNIC/CRMS/phone validation is basic, but this is mainly a data-validation issue unless inaccessible guidance prevents recovery

---

## Limitations

- The audit was performed against a **public production website**.
- The original source code was not available.
- No changes were made to the live website.
- Testing remained non-intrusive.
- No CAPTCHA bypass or security testing was attempted.
- Real or sensitive personal information was not used.
- Some deeper registration flows were intentionally not completed.
- Exact viewport dimensions were not recorded.
- Screen-reader testing was primarily based on DOM/accessibility-tree inspection and basic behavior rather than an expert end-to-end assistive-technology test.

---

## Conclusion

The DPMIS Registration Page is generally keyboard operable and contains several examples of appropriate native HTML. However, important accessibility barriers remain around **form labelling, CAPTCHA accessibility, contrast, semantic structure, validation communication, disabled-state semantics, and responsive reflow**.

The highest-impact findings are the **missing accessible names/labels on core registration controls** and the **lack of an equivalent non-visual CAPTCHA alternative**, because both can directly interfere with completing the registration process.

This audit documents the current production state and recommended remediation only. It does **not** claim that any fixes were implemented on the live Government of Punjab website.
