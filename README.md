# IN ABSENTIA

Offline-first, client-side posthumous record builder that encrypts critical life logistics into a single, standalone, self-decrypting `inabsentia.html` file.

Live site: `https://inabsentia.app`

## Cryptographic Specification

All encryption and decryption operations run strictly inside the browser using the Web Crypto API (`window.crypto.subtle`). No data is ever transmitted, stored in browser storage, or sent to any server.

- **Key Derivation:** `PBKDF2` with `HMAC-SHA256`, `600,000` iterations, and a fresh 128-bit (`16`-byte) cryptographically random salt (`crypto.getRandomValues`).
- **Cipher:** `AES-256-GCM` with a fresh 96-bit (`12`-byte) cryptographically random initialization vector (IV) per seal.
- **Compression:** Raw deflate compression (`CompressionStream` / `DecompressionStream` when supported) before encryption.
- **Standalone Longevity:** The exported `inabsentia.html` contains zero external `<link>` or `<script>` URLs and relies solely on native system serif and monospace font stacks so it remains readable and decryptable offline decades from now.

## Offline Verification

To verify that zero network activity occurs during record creation, sealing, or decryption:

1. Open `https://inabsentia.app` (or open `index.html` directly from disk).
2. Open browser Developer Tools (`F12`) and select the **Network** tab.
3. Disconnect Wi-Fi or enable Airplane Mode.
4. Complete the `RITUS` flow, seal the record, and verify the downloaded `inabsentia.html` file in `SOLVE` or by opening `inabsentia.html` directly.

## Cloudflare Pages Deployment

This repository requires zero build steps and zero npm dependencies.

- **Framework preset:** None
- **Build command:** (leave empty)
- **Build output directory:** `/`

## Repository Structure

- `index.html`: Complete self-contained application.
- `_headers`: Cloudflare Pages security and CSP headers (`connect-src 'none'`).
- `robots.txt`: Crawler directives referencing `https://inabsentia.app/sitemap.xml`.
- `sitemap.xml`: XML sitemap for `https://inabsentia.app/`.
- `og-card.svg`: 1200x630 Open Graph preview image.
- `README.md`: Documentation, cryptographic specification, and deployment guide.
- `LICENSE`: MIT License.

## License

MIT. See [LICENSE](LICENSE).
