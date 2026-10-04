# DPMIS Accessibility Audit — Phase 8 Color & Visual Accessibility

## Scope

Phase 8 reviewed text/UI contrast using axe DevTools results, manual Chrome contrast checks, and computed-style sampling from the live DPMIS registration page.

## Confirmed Contrast Failures

### 1. Information and video links
Multiple informational links use approximately:

- Foreground: `#6286c2`
- Background: `#ffffff`
- Contrast: **3.68:1**
- Required for normal text: **4.5:1**

Affected examples include:

- DPMIS registration URL
- Android app link
- From Web
- From Android App
- Personal Info
- Medical Info
- Educational Info
- Job Info
- Complaint Submission

**Status:** Confirmed accessibility violation  
**WCAG:** 1.4.3 — Contrast (Minimum)

### 2. CAPTCHA refresh control
The CAPTCHA refresh button uses white content on approximately `rgb(35, 170, 181)`.

- Contrast: **2.80:1**
- Required for the displayed text/symbol: **4.5:1**

**Status:** Confirmed contrast issue  
**WCAG:** 1.4.3 — Contrast (Minimum)

### 3. DAB/TAB badges
The DAB and TAB badges fail normal-text contrast:

- DAB: **2.41:1**
- TAB: **3.04:1**
- Required: **4.5:1**

**Status:** Confirmed accessibility violation  
**WCAG:** 1.4.3 — Contrast (Minimum)

### 4. DAB/TAB labels
The two board-selection labels measured approximately:

- Contrast: **4.48:1**
- Required: **4.5:1**

This is a very small numerical failure but still below the stated threshold.

**Status:** Confirmed technical contrast failure  
**WCAG:** 1.4.3 — Contrast (Minimum)

## Items Not Counted as Contrast Violations

### Disabled Google Map links
The DAB/TAB Google Map links measured below 4.5:1, but they visually represent inactive controls before a hospital is selected. Inactive user-interface components can be exempt from minimum contrast requirements.

Their accessibility problem is tracked separately because they remain keyboard-focusable and do not expose a disabled state programmatically.

### Login measurement inconsistency
A manual check produced a passing ratio for one Login presentation, while the automated computed-style sampling found another nested Login instance with a low ratio. Because the page contains unusual nested navigation markup and responsive controls, this item is not counted as a confirmed Phase 8 contrast violation without further targeted verification.

### Focus indicators
Focus indicators were visible during Phase 7. Some form-field focus styling appeared lighter, but no contrast measurement was captured. This remains an observation rather than a confirmed failure.

## Color-Only Communication

No confirmed case was identified in this phase where important meaning was communicated by color alone. Error-state color behavior will be evaluated during the validation/error phase.

## Phase 8 Conclusion

The strongest visual-accessibility issue is insufficient contrast across the informational links, CAPTCHA refresh control, and DAB/TAB badge/label content. These failures align with the earlier Lighthouse and axe findings. Disabled map links are excluded from the contrast count and tracked separately for their keyboard/state semantics.
