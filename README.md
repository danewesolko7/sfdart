# SF-DART

Static HTML/CSS front end for **HUD SF-DART**, the Single Family Data Analysis and Reporting Tool from the U.S. Department of Housing and Urban Development (HUD).

SF-DART is a self-service business intelligence and analytics platform for HUD staff and FHA-approved servicers. Servicers use it to:

- View their quarterly **Tier Ranking System II (TRS II)** scores and grades
- Drill into the FHA case-level data behind each element score
- Review quarterly performance reports and analytics on servicing, defaults, claims and loss mitigation
- Report training toward the annual training credit

## Pages

| File | Purpose |
| --- | --- |
| [index.html](index.html) | Public landing page: program status, TRS II elements, sample scorecard, grade-to-tier table, how it works, help contacts |
| [sign-in.html](sign-in.html) | Username sign-in step with the system use notice and Security and Usage Agreement acknowledgment |

## Project structure

```text
css/
  base.css      Shared tokens, layout, gov banner, header, help, footer, motion
  home.css      Landing page styles
  sign-in.css   Sign-in page styles
img/
  hero-800.jpg, hero-1400.jpg   Responsive hero image (srcset)
  sfdart-logo.svg               Site seal
index.html
sign-in.html
```

There is no build step and there are no dependencies. Load `base.css` before the page stylesheet.

## Running locally

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000>.

## TRS II tiers

The landing page explains how annual TRS II scores map to grades and tiers. Scores are calculated monthly, averaged each quarter, then averaged over the October 1 – September 30 fiscal year.

The four scored elements are Foreclosure Prevention, Redefaults, SFDMS Reporting and Loss Mitigation Engagement.

## Compliance

### Accessibility: WCAG 2.2 Level AAA (target)

The site is built to the highest WCAG conformance level, which also exceeds the WCAG 2.0 Level AA baseline that Section 508 requires of federal websites.

| Level | Meaning | Status |
| --- | --- | --- |
| A | Minimum accessibility | Target met |
| AA | Section 508 / industry standard | Target met |
| **AAA** | Enhanced accessibility | **Design target** |

How the code addresses specific success criteria:

| Criterion | Level | Implementation |
| --- | --- | --- |
| 1.4.1 Use of Color | A | Standalone links are always underlined |
| 1.4.6 Contrast (Enhanced) | AAA | Every text/background pair is at least 7:1; ratios are documented on each color token in [css/base.css](css/base.css) |
| 2.2.2 Pause, Stop, Hide | A | Animations are short, play once and never loop |
| 2.3.1 Three Flashes | A | Nothing flashes |
| 2.3.3 Animation from Interactions | AAA | All motion runs only under `prefers-reduced-motion: no-preference`; turning on reduced motion mid-visit reveals everything immediately |
| 2.4.1 Bypass Blocks | A | "Skip to main content" link on every page |
| 2.4.7 Focus Visible / 2.4.13 Focus Appearance | AA / AAA | Two-tone focus ring (gold outline over dark halo) visible on light and dark backgrounds |
| 2.5.5 Target Size (Enhanced) | AAA | Links and controls are at least 44×44px |
| 3.1.4 Abbreviations | AAA | Every acronym (HUD, FHA, TRS II, SFDMS, MMIF…) is wrapped in `<abbr title>` |
| 3.3.1 Error Identification / 3.3.3 Error Suggestion | A / AA | Sign-in shows a text error, sets `aria-invalid` and moves focus to the field |

Additional support:

- **Forced colors / Windows High Contrast:** score bars, icons and focus rings switch to system colors.
- **No-JavaScript and print:** content is fully visible without scripts; the hidden scroll-reveal state applies only after the script adds `.js-motion`, and print always shows everything.
- **Responsive:** layouts reflow at 1100px, 960px and 600px.

AAA is the design target. Confirm conformance with automated tools (axe, WAVE) and manual testing with screen readers and keyboard before release.

### Federal website requirements

- **Official government banner:** "An official website of the United States government" with the .gov and HTTPS explanation, per the U.S. Web Design System pattern.
- **Executive Order 14224:** footer notice that English is the official language and the English-language version is authoritative.
- **System use notice:** sign-in displays the required warning (authorized use only, monitoring consent, 18 U.S.C. § 1030 penalties) and requires acknowledgment of the Security and Usage Agreement before continuing.
- **Required links:** HUD accessibility policy and privacy and security policies in every footer.
