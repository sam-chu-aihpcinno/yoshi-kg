# yoshi-kg

Password-protected personal page. The entire site is a single static `index.html` whose
content is encrypted (PBKDF2 + AES-GCM) and decrypted client-side in the browser after the
correct password is entered. It is published via GitHub Pages (`.nojekyll` present).

## Cursor Cloud specific instructions

- This repo has **no package manager, build step, lint, or test suite**. It is plain static
  files (`index.html`, `robots.txt`, `.nojekyll`). There are no dependencies to install.
- To run/develop, serve the static files over HTTP and open the page in a browser, e.g.
  `python3 -m http.server 8000` from the repo root, then visit `http://localhost:8000/`.
  Opening `index.html` via the `file://` protocol also works because all logic is inline,
  but a local HTTP server better matches GitHub Pages.
- The decrypted content cannot be viewed without the real password (it is intentionally
  secret). Entering any wrong password runs the full crypto path and shows the localized
  error `密碼錯誤，請再試一次 / Wrong password`, which is the expected way to verify the gate
  works without the secret.
- The "remember password" checkbox persists the password in `localStorage` under the key
  `yoshi-kg-pw`; on reload a stored password auto-submits. Clear that key to test the gate
  from a fresh state.
