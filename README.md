# Ingredient Check

A halal ingredient screener that runs entirely in the browser. Scan a barcode, or
photograph an ingredient label, and it flags what needs checking — and says why.

## How it works

1. **Barcode** → looked up in [Open Food Facts](https://world.openfoodfacts.org),
   a free open food database. Returns the ingredient list and pre-parsed E-numbers.
2. **Label photo** → cropped, converted to greyscale and contrast-stretched, then read
   with [Tesseract.js](https://tesseract.projectnaptha.com/) on the device.
3. Either source feeds the same classifier: a built-in table of E-numbers and ingredient
   names, each marked prohibited, source-dependent, or permissible.

Verdicts are **Contains prohibited**, **Needs checking**, **Nothing flagged**, or
**No ingredient list**. Every flag shows the ingredient that triggered it and the reason.

If a product is certified vegan, source-dependent flags (E471, glycerine, mono- and
diglycerides) are marked resolved, since the animal-or-plant question is settled.

## What it cannot do

It reads ingredient lists. It cannot know how an animal was slaughtered, what a factory
shares equipment with, or what an undisclosed "natural flavouring" contains. **Needs
checking** means ask the manufacturer or look for certification — not that something is
forbidden. Scholars differ on several entries in the table; the reasoning is shown for
every flag so you can judge it yourself.

## Running it

Open `index.html` in a browser. No build step, no dependencies to install.

Served over HTTPS it also installs to a phone home screen and works offline, apart from
barcode lookup and the first OCR run (which downloads ~15 MB of language data, then caches it).

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app: UI, ruleset and classifier |
| `sw.js` | Offline cache. Bump `CACHE` when the app changes |
| `manifest.webmanifest` | Home-screen install metadata |

Product data from Open Food Facts, used under the
[Open Database License](https://opendatacommons.org/licenses/odbl/1-0/).
