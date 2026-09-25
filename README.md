# Idea Factory Quest - deployment guide

## What is included
- `index.html`: the complete mobile-friendly game.
- `assets/factory-future.png`: the 11-piece reveal image.
- `qr-codes/`: print-ready PNG QR codes, one for each booth.
- `booth-codes.csv`: booth-to-code mapping for event staff.

## The 11 booth codes
Keep `booth-codes.csv` with event staff. Give each booth only its own QR image/code.

## Test locally
1. Unzip the folder.
2. Start a local web server from inside the folder. For example, with Python installed: `python -m http.server 8000`.
3. Open `http://localhost:8000` in a browser.
4. Enter a code listed in `booth-codes.csv`.
5. Camera access is normally available on `localhost`. On phones, deploy the site over HTTPS.

## Recommended deployment: Azure Static Web Apps
1. Create a GitHub repository and upload the contents of this folder, not the outer folder itself.
2. In the Azure portal, create a **Static Web App**.
3. Select the GitHub repository and branch.
4. Choose **Custom** as the build preset.
5. Set **App location** to `/` and leave API/output locations empty.
6. Complete creation. Azure will publish an HTTPS URL.
7. Open the URL on an event phone and test manual entry and camera scanning.
8. If required, add a custom domain in the Static Web App settings.

## Alternative deployment: GitHub Pages
1. Upload the folder contents to a GitHub repository.
2. Open **Settings > Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select the main branch and root folder.
5. Save and use the HTTPS Pages URL.

## Event-day setup
1. Print each file in `qr-codes/` and place it only at the matching booth.
2. Keep the matching text code visible below the QR as an accessibility/fallback route.
3. Ask staff to issue the code only after an idea has been submitted.
4. Test all 11 QR codes with the deployed site before opening the event.
5. Progress is stored in the participant's browser using local storage. Clearing site data, using private browsing, changing browsers, or changing devices resets progress.

## Change the image
Replace `assets/factory-future.png` with another landscape PNG using the same filename. A 3:2 aspect ratio works best.

## Change booth codes
Edit `CODE_TO_PIECE` near the bottom of `index.html`, then regenerate the QR images so the QR payloads match. Codes are case-insensitive.

## Important implementation notes
- Camera scanning uses the `html5-qrcode` JavaScript library from the unpkg CDN and needs internet access when the page first loads.
- Camera access on phones requires HTTPS and user permission.
- This is a static, browser-based experience. It does not collect names or idea submissions and does not centrally track completion.
- For centrally managed, single-use codes or participant analytics, add a backend and authentication before the event.
