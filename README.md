# lichtwerk

Marketing site for lichtwerk, ready to preview as static files and to paste into Squarespace. The layout, colors, and copy follow the locked design: ink black, paper white, signal yellow, a Swiss grid, and the dither drawings. Customers see the name as lowercase **lichtwerk**. The legal name Lichtwerk IT LLC appears only in the privacy policy, the terms, and the footer copyright line.

`src/` is the preview. `squarespace/` is what gets pasted. There is no build step.

## Preview the static site

1. In this repo, change into `src`.
2. Run `python3 -m http.server 8080`.
3. Open [http://127.0.0.1:8080/](http://127.0.0.1:8080/) for the homepage, [http://127.0.0.1:8080/privacy](http://127.0.0.1:8080/privacy) for the privacy policy, and [http://127.0.0.1:8080/terms](http://127.0.0.1:8080/terms) for the terms.
4. The page loads Archivo, Archivo Black, and Geist Mono from Google Fonts, so the preview needs a network connection. Serve it from `src` so the root-relative links resolve.

## Paste into Squarespace

You need a **Squarespace Core plan or higher**. Code Injection and Code Blocks are not on the Personal plan. Core, Plus, Advanced, and the commerce plans include both.

Paste each file in full, including any `<script>` tags. Use a Code block (the `</>` block), not a Markdown block. Markdown will show the tags as text and the seat calculator will not run.

1. In the site editor, open **Design → Custom CSS** (on newer editors this sits under Website Tools). Open `squarespace/custom-css.css`, select the entire file, paste it in, and save. Every design rule is scoped under `#lw`, so it does not restyle Squarespace's editor or pages that are not part of this site. A separate block hides the template header and footer only on pages that contain the lichtwerk markup, and pulls the section edge to edge.
2. Open **Settings → Advanced → Code Injection → Header**. Paste `squarespace/header-injection.html` and save. That snippet loads the three typefaces and the dither script used by the hero, the audit panel, and the two plan bands.
3. In the same Code Injection panel, paste `squarespace/footer-injection.html` into **Footer** and save. It redraws the dither art after layout, and it starts the seat calculator if a Code block strips the script tag. The snippet does nothing on pages that do not contain the calculator or the canvases.
4. Create the homepage. Add a blank page, set it as the site homepage, and set its URL to `/`. Remove any extra blocks and hide the Squarespace page title if the template adds one. The page should be a single section with a single Code block. Paste `squarespace/home.html` into that block. In the section settings, set the section width to full and the padding to zero. The custom CSS forces the same thing; the section setting keeps the editor from fighting it.
5. Create the privacy page. Add a blank page, set the URL slug to `privacy` (the footer links to `/privacy`), hide the template page title, and paste `squarespace/privacy.html` into one Code block.
6. Create the terms page the same way. The URL slug must be `terms`. Paste `squarespace/terms.html` into one Code block.
7. Save and open the homepage on a desktop window and on a phone. Drag the Users slider and switch between **$150 Managed IT** and **$200 + Compliance**. The lines should update. Five users on Managed IT reads **$1,030.00** for the month and **$849.75** for the first month after the assessment credit. The Squarespace header and footer should be gone on these three pages. Any other page that does not contain the lichtwerk block keeps the template chrome.
8. The legal pages use the supplied privacy policy and terms verbatim, so the bracketed placeholders are still in the text: `[DATE]`, `[EMAIL]`, `[MAILING ADDRESS]`, `[TOOL]`, and `[privacy@lichtwerk...]`. Replace those placeholders in the two Code blocks when the real values exist. Leave the surrounding sentences as they are.

If the live page is a narrow centered column, the section is not full width or the custom CSS did not save. If the template header is still visible, the Code block is missing `id="lw"` or the custom CSS was not saved. If the calculator does not respond, the block is Markdown rather than Code, or the header injection did not save. The footer injection is the backup that runs the same calculator.

## What the pages include

The footer links to Privacy Policy and Terms. Its contact lines are (240) 230-6468, PO Box 838, Chaptico, MD 20621, and lichtwerkit.com, plus the copyright. Office hours stay in the response-times section, in the design's words: Monday to Friday, 8 to 6 Eastern. They are not in the footer.

The locked design has no form. The booking area says "When you book, please don't include patient or health information." The Book buttons and "Ask about an audit" dial (240) 230-6468. To point them at a scheduler later, replace the `tel:+12402306468` hrefs on those buttons only, and leave the visible labels unchanged.

The seat calculator uses the locked math. Headcount times the plan price, raised to the $1,000 monthly minimum when that is higher, then 3 percent Maryland tax (`Math.round(subtotal * 3) / 100`). The first-month line subtracts the $175 assessment from the pre-tax subtotal and applies the same tax to what remains.

## Files

| Path | Paste target |
| --- | --- |
| `src/index.html` | Static homepage. Not pasted into Squarespace. |
| `src/privacy/index.html`, `src/terms/index.html` | Static legal pages. |
| `src/base.css`, `src/dither.js`, `src/site.css` | Locked source styles and the preview stylesheet. |
| `squarespace/custom-css.css` | Design → Custom CSS |
| `squarespace/header-injection.html` | Code Injection → Header |
| `squarespace/footer-injection.html` | Code Injection → Footer |
| `squarespace/home.html` | Code block on the homepage |
| `squarespace/privacy.html` | Code block on `/privacy` |
| `squarespace/terms.html` | Code block on `/terms` |
