# SBP QR Scanner

A lightweight browser-based QR scanner for Russian Faster Payments System (SBP) payment links.

The app scans a QR code with the device camera, recognizes SBP payment links from `qr.nspk.ru`, extracts useful values, and hands the payment link to a supported banking app so the user can complete and confirm the payment there.

Live demo: <https://zemamba.github.io/sbp-qr-scanner/>

Source: <https://github.com/zemamba/sbp-qr-scanner>

## Features

- Scans QR codes directly in the browser.
- Supports SBP payment links issued through `qr.nspk.ru`.
- Parses GOST R 56042 payment details that start with `ST0001`.
- Shows the original QR payload and extracted fields.
- Opens supported Android banking apps through intent links:
  - Gazprombank
  - Alfa-Bank
  - T-Bank
- Falls back to the system app picker when a direct Android intent is not available.
- Keeps recent scan history in the current browser session UI only.
- Runs as a static single-page app with no custom backend.

## Privacy

Camera frames are processed locally in the browser. This project does not upload scanned QR contents or camera data to a custom server.

SBP payment links are passed to the banking app selected by the user. The bank app then requests payment details from NSPK and asks the user to confirm the payment inside the bank app.

The QR decoding library is loaded from jsDelivr by default:

```html
https://cdn.jsdelivr.net/npm/jsqr@1.4.0/dist/jsQR.min.js
```

If you need a fully offline build, vendor this dependency locally and update the script tag in `index.html`.

## Usage

Open `index.html` from an HTTPS origin or from `localhost`. Camera access will not work on ordinary insecure HTTP pages in modern browsers.

For a quick local preview:

```bash
python3 -m http.server 8080
```

Then open:

```text
http://localhost:8080
```

## Deployment

This is a static web app. It can be deployed to GitHub Pages, Netlify, Cloudflare Pages, or any static hosting provider.

## Compatibility Notes

- Android Chrome supports package-targeted intent links for direct bank handoff.
- Other browsers and platforms usually open the SBP link through the system handler.
- GOST R 56042 details are displayed for copying because most banking apps do not accept those details through external deep links.

## Security Notes

Always verify the recipient, amount, and payment purpose in your bank app before confirming a payment. This scanner only reads and forwards QR data; it does not validate merchant legitimacy and does not execute or confirm payments.

## License

This project is licensed under the GNU General Public License v3.0 or later. See [LICENSE](LICENSE).

Derivative versions must remain free software under the same license family and must preserve attribution to the original author/project. See [NOTICE](NOTICE).
