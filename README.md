# Recipe Box

A cookbook web app styled like a 1950s recipe tin. Photograph a recipe card or cookbook page, and it reads the text on your phone and fills in the ingredients and steps. Rate recipes, scale them, keep kitchen notes, and send a grocery list to the Notes app. Installs to the iPhone Home Screen and works offline.

No server, no accounts, no API keys. Everything runs and is stored on the device.

## Features

- **Scan recipes** from photos (multiple photos per recipe, e.g. front and back of a card). Text recognition runs on the phone with Tesseract.js. Results land in an editable form so you can fix anything before saving.
- **Recipe cards** with star ratings, favorites, categories, servings and times, "I made this" counter, photos of the original, and kitchen notes that save as you type.
- **Scaling** ½×, 1×, 2×, 3× with proper kitchen fractions (1½ cups, not 1.5).
- **Cooking help**: cross off ingredients you have, tick off steps as you go, keep the screen on.
- **Grocery list** grouped by aisle or by recipe, with check-off, manual items, and **Send to Notes** (iOS share sheet).
- **Search and sort** by name, ingredient, rating, or how often you've made it.
- **Backup and restore** to a JSON file.
- Works **offline** after the first visit; light and dark mode.

## Put it on GitHub Pages

1. Create a new repository on GitHub (for example `recipe-box`).
2. Upload everything in this folder to the root of the repository: `index.html`, `sw.js`, the `icons/` folder, and the hidden `.nojekyll` file.
   - On github.com: **Add file → Upload files**, then drag the files and folders in.
   - Or with git:
     ```bash
     git init
     git add .
     git commit -m "Recipe Box"
     git branch -M main
     git remote add origin https://github.com/YOUR-USERNAME/recipe-box.git
     git push -u origin main
     ```
3. In the repository, open **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, branch **main**, folder **/ (root)**, then **Save**.
4. After a minute or two the site is live at `https://YOUR-USERNAME.github.io/recipe-box/`.

All paths are relative, so it works under any repository name.

## Install on your iPhone

1. Open the GitHub Pages link in **Safari**.
2. Tap the **Share** button.
3. Tap **Add to Home Screen**, then **Add**.

The Home Screen app keeps its own storage, separate from Safari. Add recipes from the Home Screen app, or move them across with **Backup & settings → Save a backup file / Restore from backup**.

## Sending the grocery list to Notes

Tap **Send to Notes** on the grocery list and pick **Notes** in the share sheet. The list arrives as plain lines grouped by aisle. To turn them into checkboxes, select the lines in Notes and tap the checklist button. **Copy list** is there too, for pasting anywhere.

## Getting good scans

- Lay the card flat, in good light, and fill the frame with it.
- Printed and typed recipes read best. Handwriting is hit and miss, so expect to tidy those up.
- Recipes with "Ingredients" and "Directions/Method" headings parse most reliably. Without headings, the app guesses: lines starting with amounts become ingredients, and sentences become steps.
- The first scan needs internet to download the text reader (about 5 MB). After that, scanning works offline.
- **Show the scanned text** under the scan button shows everything that was read, so you can copy anything the parser missed.

## Updating the app

When you change `index.html`, open `sw.js` and bump `VERSION` (for example `'v1'` → `'v2'`) before you push. Phones pick up the new version the next time the app opens (sometimes it takes a second launch).

## Files

All the app's HTML, CSS and JavaScript live in `index.html`, in this order: styles, install manifest, storage, recipe parser, text recognition, then the app screens. Each section starts with a labeled comment banner so you can find your way around.

| File | What it does |
| --- | --- |
| `index.html` | The whole app |
| `sw.js` | Offline support. Browsers only run a service worker from its own file, so this can't be folded into `index.html`. If you delete it, the app still works and installs, but won't open offline. |
| `icons/` | Home Screen and app icons |
| `.nojekyll` | Tells GitHub Pages to serve files as-is |

## Your data

Recipes, photos and the grocery list are stored in the browser on your device (IndexedDB). Nothing is uploaded anywhere; the only network requests are for fonts and the text-recognition library. Deleting the Home Screen app deletes its data, so keep a backup.
