# SF-DART website (public pages)

This repository holds the public-facing web pages for **SF-DART**, the Single Family Data Analysis and Reporting Tool run by the U.S. Department of Housing and Urban Development (HUD).

SF-DART is a website where HUD staff and FHA-approved mortgage servicers (companies that collect payments on FHA-insured home loans) can:

- See their quarterly **Tier Ranking System II (TRS II)** scores, the grades HUD gives servicers for how well they handle loans that fall behind
- Look at the individual loans (FHA cases) behind each score
- Read quarterly performance reports on servicing, defaults, claims and loss mitigation
- Report training they've completed toward the annual training credit

## What's in this repository, and what isn't

**In this repository:** two pages, the home page and the first step of sign-in. They are plain HTML and CSS files: no frameworks, no build tools, nothing to install.

**Not in this repository.** These are separate systems that these pages link to:

| Item | Where it lives |
| --- | --- |
| Password step and the rest of sign-in | The sign-in form sends the username to `/sign-in/continue`, which must be provided by the SF-DART server. Opened from this folder on its own, the form goes nowhere. |
| Scores, reports and case data (the actual application) | SF-DART application, after sign-in |
| Training reporting | <https://sfdart.hud.gov/dashboard-ta.html> |
| Security and Usage Agreement | <https://sfdart.hud.gov/sfdart_user_agreement.pdf> (PDF) |

## The pages

### Home page: [index.html](index.html)

From top to bottom:

1. **Government banner:** "An official website of the United States government", with a "Here's how you know" explanation that opens and closes.
2. **Header:** SF-DART logo (links back to this page) and navigation: What's inside, How it works, Report Training, Help, and a Sign In button.
3. **Introduction:** what SF-DART is, a Sign In button and a photo.
4. **Status strip (green):** current evaluation round, most recent TRS II scores and system status. **This text is typed in by hand. It does not update itself and must be edited every quarter.**
5. **What's inside (dark blue):** the four TRS II score elements, a sample scorecard (made-up data, labelled as such), a table showing how grades map to tiers, and the data sources behind SF-DART.
6. **How it works:** four steps from getting an account to looking at case details.
7. **Annual training credit (light gray):** a "Report your training" button that opens the training reporting site.
8. **Help (green):** technical support email, the FHA Resource Center phone number, and resource links.
9. **Footer:** support contact, accessibility and privacy policy links, and the required official-language notice.

### Sign-in page: [sign-in.html](sign-in.html)

1. Same government banner and header as the home page, but with no navigation links. The logo links back to the home page.
2. **Sign-in card:** a username field and an "Agree and continue" button. Selecting the button means the user accepts the Security and Usage Agreement. If the field is left empty, an error message appears and is read out by screen readers.
3. Links for help signing in and for reporting training.
4. **Legal notice:** HUD's required warning about authorized use, monitoring and penalties. The client supplied this text word for word, so don't reword it without their approval.
5. Same footer as the home page.

## Viewing the pages on your computer

**Quickest:** double-click `index.html` to open it in your web browser.

**Closer to the live site:** run a small local web server, which is built into macOS and most Linux systems:

```sh
cd path/to/sfdart
python3 -m http.server 8000
```

Then open <http://localhost:8000> in a browser. Press `Ctrl+C` in the terminal to stop the server.

## Files

```text
index.html          Home page
sign-in.html        Sign-in page
css/
  base.css          Styles shared by both pages: colors, header, footer, buttons, banner, help section
  home.css          Styles used only on the home page
  sign-in.css       Styles used only on the sign-in page
img/
  hero-800.jpg      Home page photo, smaller version for phones
  hero-1400.jpg     Home page photo, larger version for desktops
  sfdart-logo.svg   SF-DART seal shown in the header
```

Each page loads `base.css` first, then its own stylesheet. The order matters.

### Common edits

| To change… | Edit |
| --- | --- |
| Status strip (round, latest scores, system status) | `index.html`, the section marked `class="status"` |
| Legal notice text | `sign-in.html`, the section marked `class="notice"` (client-approved wording) |
| Support email address | Search all `.html` files for `sfdart-support@hud.gov`; it appears in several places |
| Colors | `css/base.css`, top of the file. Each color notes its contrast ratio; recheck contrast after any change (see Accessibility below). |

### Where every external link goes

| Link text | Destination |
| --- | --- |
| Report your training | <https://sfdart.hud.gov/dashboard-ta.html> |
| Security and Usage Agreement (PDF) | <https://sfdart.hud.gov/sfdart_user_agreement.pdf#page=1> |
| "click here" in the legal notice | Same PDF, opened at page 3 (the Security Addendum) |
| TRS II servicer narrative (PDF) | <https://www.hud.gov/sites/dfiles/SFH/documents/spsnarrative.pdf> |
| FHA lender performance | <https://www.hud.gov/hud-partners/single-family-lender-performance> |
| Accessibility policy | <https://www.hud.gov/accessibility> |
| Privacy and security policies | <https://www.hud.gov/privacy> |
| Support email | <mailto:sfdart-support@hud.gov> |
| FHA Resource Center | (800) 225-5342 |

## Accessibility

### What's required

Federal websites must be usable by people with disabilities under **Section 508** of the Rehabilitation Act. In practice, Section 508 means meeting **WCAG 2.0 Level AA**, part of the Web Content Accessibility Guidelines.

WCAG has three levels:

| Level | What it means | For this site |
| --- | --- | --- |
| A | The basics | Required |
| AA | The standard most organizations meet | **Required (Section 508)** |
| AAA | The strictest level; often not possible for every type of content | Met where practical, not required |

### Current status

- **Level AA:** no known problems. Met according to a line-by-line review of the code on October 20, 2026.
- **Level AAA:** met for everything the code controls. Two content items fall short, and AAA isn't required:
  - The legal notice is written at a higher reading level than AAA asks for.
  - Industry terms such as "partial claim" have no glossary.
- **Keyboard test:** passed on October 20, 2026. Everything on both pages can be reached and used with the keyboard alone.
- **Zoom test:** passed on October 20, 2026. Both pages work at 200% and 400% zoom with nothing cut off and no sideways scrolling.
- **Automated scan:** passed on October 20, 2026. pa11y with the axe and HTML_CodeSniffer engines found no errors at Level AA or AAA on either page, including the sign-in page with its error message showing.
- **VoiceOver (Mac):** worked on October 20, 2026, in an informal check of both pages.
- **Recommended before release:** a check with NVDA or JAWS on Windows, the screen readers most federal users rely on. Section 508 doesn't require testing with any particular screen reader, but HUD's Section 508 office may run its own test (often JAWS) before launch. The linked PDFs must also be checked before the site is described as 508 compliant.

### What was built in

Each item lists the WCAG success criterion number it addresses, for auditors.

| What | Why it matters | WCAG |
| --- | --- | --- |
| All text has strong contrast against its background (at least 7:1; AA requires 4.5:1) | Readable for people with low vision or color blindness | 1.4.3, 1.4.6 |
| Links in text are underlined | Links don't rely on color alone | 1.4.1 |
| "Skip to main content" link at the top of each page | Keyboard users can jump past the header | 2.4.1 |
| A thick gold-and-dark outline shows which item is selected when using the keyboard | Keyboard users can always see where they are | 2.4.7, 2.4.13 |
| Buttons and links are at least 44×44 pixels | Easy to tap and click, including with limited hand control | 2.5.5 |
| Animations are short, never flash or loop, and turn off when the visitor's device is set to reduce motion | Safe for people with motion sensitivity or seizure disorders | 2.2.2, 2.3.1, 2.3.3 |
| Abbreviations (HUD, FHA, TRS II…) show their full name | Unfamiliar acronyms are explained | 3.1.4 |
| Text line length, line spacing and paragraph spacing are controlled | Easier reading for people with dyslexia or low vision | 1.4.8 |
| The support contact is the first footer link on every page | Help is always in the same place | 3.2.6 |
| Sign-in errors appear as text, are announced by screen readers and move the cursor to the field | Everyone knows what went wrong and how to fix it | 3.3.1, 3.3.3, 4.1.3 |
| Lists, headings, the table and page regions are marked up so screen readers can announce them | Blind users can understand the page structure and navigate it | 1.3.1 |
| Layout adapts from wide desktop screens down to phones, and to 400% zoom | No sideways scrolling or cut-off content | 1.4.4, 1.4.10 |
| Score bars, icons and outlines switch to system colors in Windows High Contrast mode | Works for people who use high-contrast settings | n/a |
| All content shows without JavaScript and when printed | Nothing is hidden if scripts fail or are blocked | n/a |

### Testing still needed before release

1. **Automated scan** (passed October 20, 2026 with no errors at AA or AAA; repeat after changes). Install Node.js from <https://nodejs.org>, start the local server described above, then save this as `pa11y.json` somewhere outside the project:

   ```json
   { "chromeLaunchConfig": { "args": ["--force-prefers-reduced-motion"] } }
   ```

   and run:

   ```sh
   npx pa11y --runner axe --runner htmlcs --standard WCAG2AA --config pa11y.json http://localhost:8000/index.html
   npx pa11y --runner axe --runner htmlcs --standard WCAG2AA --config pa11y.json http://localhost:8000/sign-in.html
   ```

   The config turns on the "reduce motion" setting so every section is visible at once. Without it, the scanner checks text while it is still fading in and reports false contrast errors, and it skips sections that haven't been scrolled into view yet.

   Also scan the sign-in page with its error message showing, by adding `"actions": ["click element #signin-form button", "wait for element #username-error to be visible"]` to the config.

   Warnings you can expect and ignore:
   - The logo image has empty alt text on purpose: the site name right next to it is the link's text.
   - Some text is "absolutely positioned": this is screen-reader-only text that isn't visible on screen.
   - "Consider using a caption" on the grades table: the table is already labelled by the heading above it.

   Alternatively, install the free **axe DevTools** or **WAVE** extension in Chrome or Firefox and scan each page.
2. **Keyboard only** (passed October 20, 2026; repeat after changes). Use Tab, Shift+Tab, Enter and Space to reach and use everything on both pages without a mouse.
3. **Screen readers.** VoiceOver (built into Macs, turn on with Cmd+F5): checked October 20, 2026. Recommended: NVDA (free) or JAWS on Windows. Without a Windows computer, ask HUD's Section 508 office, or use a Windows virtual machine or a hosted testing service such as Assistiv Labs. Listen for: page title and headings announced in order, every link and button making sense on its own, the username field announced with its label, and the error read out after selecting "Agree and continue" with the field empty.
4. **Zoom** (passed October 20, 2026; repeat after changes). Zoom the browser to 200% and 400%. Nothing should be cut off, and you shouldn't need to scroll sideways.
5. **Linked PDFs.** The Security and Usage Agreement and TRS II narrative PDFs must also be accessible. They are maintained outside this repository.

Automated tools catch only about a third of accessibility problems, so steps 2–4 are required, not optional. Repeat the keyboard and zoom tests whenever a page changes.

## Other federal website requirements

- **Official government banner** at the top of every page, following the U.S. Web Design System pattern.
- **Executive Order 14224 notice** in every footer: English is the official language, and the English version of the site is authoritative.
- **Legal notice** on the sign-in page, which users must accept ("Agree and continue") before signing in.
- **Required links** to HUD's accessibility policy and its privacy and security policies in every footer.

## Terms used in this README

| Term | Meaning |
| --- | --- |
| FHA | Federal Housing Administration, the part of HUD that insures home loans |
| Servicer | A company that collects mortgage payments and works with borrowers who fall behind |
| TRS II | Tier Ranking System II, how HUD grades servicers (Tier 1 is best, Tier 4 is lowest) |
| Loss mitigation | Ways a servicer helps a borrower who is behind on payments avoid foreclosure |
| Section 508 | The federal law requiring government technology to be accessible to people with disabilities |
| WCAG | Web Content Accessibility Guidelines, the international standard Section 508 points to |
| Screen reader | Software that reads the screen aloud for people who are blind or have low vision |
