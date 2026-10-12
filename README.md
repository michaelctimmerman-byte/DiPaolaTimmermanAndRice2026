# DiPaola, Timmerman & Rice for Emerson: campaign website

A fast, single-page static website. There are no build tools, databases, or server code.

```
index.html            page structure (rarely edited)
assets/js/content.js  ALL campaign text, statuses, FAQ, links, settings   <- edit this
assets/js/app.js      turns content.js into the page (no routine edits)
assets/css/styles.css design
assets/img/           photos, each saved in two or three sizes
```

## Preview it

Double-click `index.html` to open it in a browser. Everything works locally except the web fonts (when offline) and sending the form (until the Google Form is connected).

## Put it online (about 10 minutes)

**Netlify (simplest):** go to https://app.netlify.com/drop, sign in, and drag the whole `emerson-campaign-site` folder onto the page. To update later, drag the folder again under "Deploys." Connect your own domain under "Domain management."

Vercel, GitHub Pages, and Cloudflare Pages also work if you upload the folder as-is.

**After you have a domain:** in `index.html`, change `content="assets/img/og-image.jpg"` to the full address, for example `https://www.yourdomain.com/assets/img/og-image.jpg`. That makes the share preview appear on Facebook and in text messages.

## Edit content

Open `assets/js/content.js` in any text editor (TextEdit in plain-text mode, Notepad, or VS Code). Change the text between the quotation marks, save, and re-upload. Keep the commas and quotation marks intact. If a link isn't ready yet, leave its `url` as `""` and the site will show "Link coming soon."

Each fact carries a `basis` label shown to readers:
- `record`: confirmed in an official public document
- `campaign`: supplied by the campaign
- `projection`: an estimate, not a guarantee
- `proposal`: a plan

Each status board item has a `status` of `completed`, `progress`, `anticipated`, or `proposed`. Only use `completed` for finished work.

## Setup notes and launch mode

`showSetupNotes: true` at the top of content.js shows amber "Setup" notes and "Photo needed" frames, so the team can see what's unfinished. **Set it to `false` before launch.** That hides every note, and sections still waiting for a photo switch to a clean text-only layout.

## The Google Form (connected)

The campaign's Google Form ("Connect with DiPaola, Timmerman & Rice") is embedded in the Connect section. Responses go to the form's Responses tab, or to a Google Sheet if you link one there. Edit the questions in Google Forms anytime; the website updates automatically.

- If you add questions and the embedded form shows its own scrollbar, raise `embedHeight` in content.js.
- To use a different form, replace `viewUrl` in content.js with its share link (ending in `/viewform`).
- The private preview link can't show embedded Google pages, so it shows an "Open the request form" button instead. The live site shows the form itself.

**Optional native mode:** the site also includes its own styled form. To use it instead, add `action` and the `entry.` codes from your form's "Get pre-filled link" to `googleForm` in content.js. Its question choices must match the Google Form's wording exactly.

## Campaign disclaimer

The footer shows the `disclaimer` from content.js: "Paid for by Timmerman and Rice for Emerson Council." Before launch, confirm with your treasurer or counsel:
- whether New Jersey requires the committee's **address** with the paid-for-by line (if so, put it in `disclaimerAddress`), and
- whether a site that also promotes Mayor DiPaola needs joint wording or a cost allocation with her committee, since the named committee is a council committee.

## Add or replace photos

Save each photo as a JPEG in two widths, 800 and 1600 pixels (candidate portraits: 480 and 960, in a 4:5 shape). Name them like the existing files, e.g. `downtown-800.jpg` and `downtown-1600.jpg`, and put them in `assets/img/`.

Then in content.js, replace an issue's `slot: { ... }` line with:

```
photo: "assets/img/downtown",
alt: "Storefronts along Kinderkamack Road in Emerson",
caption: "Kinderkamack Road.",
```

Never label a photo as a place or project it doesn't show. Keep a note of the source and permission for every image you add.

## Rebuild the single-file preview (optional)

`python3 build.py` creates `build/preview.html`, a one-file version with images embedded, plus a clean copy of the site folder. You don't need this to deploy.
