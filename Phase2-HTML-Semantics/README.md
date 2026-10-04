# DPMIS Accessibility Audit — Phase 3 Semantic HTML & Structure

## Scope

Phase 3 reviewed the underlying document structure of the DPMIS registration page, including language, page title, landmarks, headings, links, buttons, lists, and non-semantic clickable elements.

## Confirmed Findings

### 1. Page title does not describe the page
The document title is:

```text
SW&BM
```

This does not clearly identify DPMIS, the registration page, or the purpose of the page.

**Status:** Confirmed accessibility violation  
**WCAG:** 2.4.2 — Page Titled

---

### 2. Heading structure does not represent a clear hierarchy
The page contains:

```text
H1  For Already Registered PWD
H1  Verification
H1  Himmat Card Verification
H3  DAB AND TAB LOCATION OR ADDRESS
H5  Urdu DAB/TAB heading
H5  District Assessment Board (DAB)
H5  Tehsil Assessment Board (TAB)
```

The main registration task has no clear heading, while several secondary card headings are marked as top-level `H1`s. The hierarchy also jumps from `H1` to `H3` and then `H5`.

**Status:** Confirmed semantic-structure issue  
**Relevant WCAG:** 1.3.1 — Info and Relationships

## Structural Concern Requiring Final WCAG Assessment

### Missing main landmark
The detected landmark-related elements were:

```text
NAV
HEADER
HEADER
```

No `<main>` or `[role="main"]` was present. No skip-to-main-content link was found among the page links.

**Status:** Confirmed structural deficiency; keep under manual/final WCAG assessment rather than treating the missing `<main>` element alone as an automatic failure.

## Passed / Positive Checks

- Document language is declared as `lang="en"`.
- A native `<nav>` element is present.
- Navigation is represented with a valid `<ul>` list.
- Native `<button>` elements are used for the detected button controls.
- No clickable `div`, `span`, `p`, or `img` elements were detected by the Phase 3 non-semantic-control check.
- Basic link and list semantics are generally native HTML.

## Items Passed Forward for Later Verification

These are not Phase 3 violations yet:

- Two verification-related links have empty `innerText`; their computed accessible names need checking in Phase 4.
- The CAPTCHA refresh button uses the visible `↻` symbol and has no `aria-label`; the usefulness of its accessible name will be checked in Phase 4.
- The navigation toggle/button exposes `aria-label="Toggle navigation"` while visible text output included `Login`; its actual purpose/name relationship needs inspection.
- Urdu text should be checked later for appropriate language declaration where relevant.
- DAB/TAB map links use `href="#"` and visually disabled states; keyboard/state behavior will be reviewed in later phases.

## Phase 3 Conclusion

The page uses some appropriate native HTML, but the semantic structure has important weaknesses. The clearest confirmed issues are the non-descriptive page title and the heading hierarchy. The missing main landmark is retained as a structural concern for final assessment, while control names and states are intentionally deferred to the dedicated Names / Roles / States phase.
