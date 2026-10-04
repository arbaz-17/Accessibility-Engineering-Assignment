# DPMIS Accessibility Audit — Phase 2 Automated Baseline

## Target

- **Website:** Punjab Disabled Person Management Information System (DPMIS)
- **Page:** Registration Page
- **URL:** https://dpmis.punjab.gov.pk/register
- **Audit Date:** 4 October 2026
- **Standard:** WCAG 2.1 AA

## Lighthouse

- **Accessibility Score:** **81/100**
- **Environment:** Emulated Desktop, Lighthouse 13.4.1, Chromium 154

### Main Findings

- Five `<select>` controls were reported without associated labels.
- Multiple low-contrast text/UI elements were detected.
- Heading levels were reported as non-sequential.
- The document was reported as missing a main landmark.
- A possible multiple-label condition was reported for the Name field.

## axe DevTools

- **Total Automatic Issues:** **20**
- **Critical:** **5**
- **Serious:** **15**
- **Moderate:** 0
- **Minor:** 0

### Issue Breakdown

#### 1. Select controls without accessible names
**5 occurrences — Critical**

Known affected controls:

- `#optr`
- `#province`
- `#division`
- `#district`
- `#board`

Both Lighthouse and axe detected this issue. axe confirmed that these selects do not have an explicit/implicit label, `aria-label`, `aria-labelledby`, or another valid accessible-name mechanism.

**Status:** Confirmed accessibility violation  
**Primary WCAG:** 4.1.2 — Name, Role, Value

#### 2. Insufficient color contrast
**15 occurrences — Serious**

One confirmed example:

- Foreground: `#6286c2`
- Background: `#ffffff`
- Measured contrast: **3.67:1**
- Required for normal text: **4.5:1**

The exact affected elements will be reviewed and grouped during the dedicated contrast phase, especially because inactive/disabled controls may require different treatment.

**Status:** Confirmed in supplied active-text example; remaining instances need review  
**Primary WCAG:** 1.4.3 — Contrast (Minimum)

## Items Requiring Manual Verification

These Lighthouse findings are not yet treated as confirmed violations:

- Possible multiple labels on the Name field
- Heading hierarchy / skipped heading levels
- Missing `main` landmark and overall landmark structure
