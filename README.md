# TikTok Coins UI Prototype

A personal frontend portfolio project demonstrating a coin-package storefront, profile lookup, and a simulated checkout journey. The interface uses HTML, CSS, and vanilla JavaScript, with a small Node.js/Express server for demo accounts, JSON records, and profile caching.

**This is an independent learning prototype.** It is not affiliated with TikTok or the payment providers shown in the interface. It does not process payments or deliver TikTok coins. Prices, discounts, payment confirmations, and delivery messages are demonstration content.

## My contribution

- Planned the original UI design, page structure, and interaction flow.
- Directed and refined the frontend implementation using AI assistance.
- Integrated the prototype screens, artwork, animations, and demo interactions.

The project demonstrates my frontend design and development practice. Its backend is a learning prototype rather than a production payment or authentication service.

## Features

- Responsive storefront with a three-card rotating showcase and manual carousel controls.
- Coin-package selection, custom coin quantities, and a dynamic order summary.
- Payment-method selection with card and mobile-wallet form demonstrations.
- Order review, a simulated processing countdown, a receipt screen, and confetti animation.
- Demo registration, login, profile editing, and transaction history.
- TikTok username/link input, an attempted public-profile lookup, local caching, and generated fallback profiles.
- Help, FAQ, and other informational modals.

## Technology

- Frontend: HTML, CSS, vanilla JavaScript, Font Awesome, and Google Fonts.
- Backend: Node.js and Express.
- Declared dependencies: Express, Axios, CORS, and Cheerio; the current server's live lookup uses Jina Reader and its Markdown parser.
- Storage: local JSON files and an image cache.

## Project files

```text
index.html
style.css
script.js
server.js
package.json
package-lock.json
README.md
.gitignore
images/                 Website artwork and logos
data/                   Created at runtime; excluded from Git
```

Keep the complete `images` folder when copying or cloning the project. The main page references its assets directly. The separate local folders `tiktok-app` and `tiktok-3d-cards` are not imported by the main website and are excluded from this repository's setup.

## Run locally

Use a supported Node.js LTS release; Node.js 24 LTS is recommended. Install Node.js from [nodejs.org](https://nodejs.org/en/download).

Open a terminal in the project root, where `package.json` is located.

For a fresh clone with the committed lockfile:

```powershell
node --version
npm --version
npm ci
npm start
```

Open [http://localhost:3000](http://localhost:3000). Keep the server terminal open while using the website. Press `Ctrl + C` to stop it.

The `start` script runs `node server.js`. Port `3000` is fixed in the current server.

`npm ci` installs the versions recorded in `package-lock.json`; it requires that the lockfile matches `package.json`. If dependencies are intentionally changed, use `npm install` and commit the updated manifest and lockfile together.

The server creates missing runtime files automatically:

- `data/users.json` starts as an empty array.
- `data/transactions.json` starts as an empty array.
- `data/tiktok_cache.json` starts as an empty object.
- `data/image_cache/` stores fetched images.

Existing runtime files are kept. Register a fictional demo account through the interface; no preloaded user database is needed.

## Demo behavior and limitations

- Checkout writes a demonstration transaction and displays a simulated success receipt. There is no payment gateway integration or coin-delivery API.
- The browser masks the card number before sending its demo order request and does not send the CVV in that request. Wallet fields can still be saved in local demo transactions. Use fictional payment, identity, and contact information only.
- Profile lookup relies on third-party network services. It can return cached or generated sample data when live lookup is unavailable. A displayed "Verified" label does not verify identity, account ownership, account existence, or the accuracy of follower/like counts.
- Passwords are stored as plain text in the current local JSON account store. Login state is kept in browser local storage; profile updates and transaction queries do not have production session authorization. Use new throwaway passwords and fictional accounts for this prototype.
- JSON storage has no concurrency controls or transactional database guarantees.
- The server exposes only the entry page, frontend CSS/JS, and the `images` directory as public files. Runtime JSON files and server source cannot be downloaded as static files. This restriction does not turn the demo APIs into a production authentication system.
- Fonts, icons, profile lookup, avatar generation, and image proxies can require an internet connection.

## Local checks

To list any referenced image files missing from the project, run this in PowerShell from the project root:

```powershell
$tiktokAssets = Select-String -Path .\index.html, .\script.js, .\style.css -Pattern 'images/[A-Za-z0-9_.-]+' -AllMatches |
    ForEach-Object { $_.Matches.Value } |
    Sort-Object -Unique
$tiktokAssets | Where-Object { -not (Test-Path -LiteralPath $_) }
```

No output means that all referenced image paths exist. If filenames appear, add the corresponding artwork to those paths before publishing the repository.

1. Open the homepage and confirm all images load at desktop and mobile widths.
2. Create a fictional account, sign in, and edit its demo profile.
3. Select a package or custom quantity and confirm the order summary changes.
4. Complete checkout using fictional card/wallet details and inspect the demo receipt and history.
5. Try profile lookup; treat any fallback statistics as sample data.
6. Confirm `/data/users.json`, `/server.js`, and `/package.json` return `404` when opened on the running local server.

## References

- [Express: serving static files](https://expressjs.com/en/starter/static-files/)
- [npm: clean installs with npm ci](https://docs.npmjs.com/cli/v11/commands/npm-ci/)
- [Node.js releases](https://nodejs.org/en/about/previous-releases)

## Author

Muhammad Amir — [GitHub](https://github.com/amirownsthis-code)
