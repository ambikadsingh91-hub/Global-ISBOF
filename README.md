# LOT Ecosystem — Local v5

This is a **local-only browser prototype**. It does not use Firebase Authentication or an API for login, signup, code redemption, wallet, listings, orders, or the simulated stock market.

## What's new in v5
- Three-line menu opens a grouped sidebar: Overview, Money & Markets, and Your Account.
- Each major area opens separately instead of showing every feature on one long page.
- Redeem Codes page for users.
- Admin-only code manager: create code, choose LOT reward and maximum claims, remove codes, and inspect who claimed each code and when.
- No default redeem codes are created.
- Seller order history displays buyer username, quantity, order ID, and purchase timestamp.
- Admin user-management list with local ban/unban, plus existing balance adjustment, password reset, and audit history.

## First-run demo administrator
- Username: `Virat`
- Password: `09872`

The demo administrator is seeded locally only if there is no `Virat` account in this browser's local account list. If the browser already has a Virat account, the seed does not overwrite that account's password or role.

## Important limitations
- Accounts, passwords (stored as salted SHA-256 hashes), balances, codes, code claims, listings, purchases, and audit logs are saved in `localStorage` on the current browser/device only.
- This is not secure authentication. Users with access to browser storage can alter local data; local admin access is not secure.
- There is no cross-device or cross-user shared database. Seller purchase history and admin claim history only reflect data recorded in this browser's local storage.
- Do not use this prototype for real money, sensitive information, or production user accounts.
- Firebase-related files remain in the ZIP as legacy/reference files; the local frontend does not use them for these features.

## Deploy
Deploy the contents of `public/` as static website files using your usual hosting provider. Test in a browser. Existing local browser data may remain after deploying; use a fresh browser profile if you want to test the first-run demo admin without touching existing accounts.
