# LOT Ecosystem — Firebase / LOTsome

This version replaces the localStorage prototype with Firebase Authentication, Cloud Firestore, Firebase Storage, and trusted Cloud Functions for balances and transactions. The Firebase project configured in `public/firebase-config.js` is **`lotsome`**.

## Included
- Username + password accounts using Firebase Authentication. Usernames are reserved uniquely in Firestore; account/profile creation runs through a Cloud Function.
- One shared server-authoritative LOT balance across VPay, LOT Shop, VStocks, redeem codes, and minigames.
- Marketplace listings, image uploads, stock quantity, purchases, seller credits, buyer/seller order history, and ledger entries stored in Firebase.
- VPay transfers and VStocks trades run through Cloud Functions and Firestore transactions. Prices are virtual/simulated, not real-world securities.
- Three answer-based minigames: Quick Math, Memory Flip, and Number Guess. Correct answers receive a server-generated reward from **1–100 LOT**. Maximum 10 successful rewards per account per UTC day, with a 10-second cooldown. Challenges expire after two minutes; failed answers do not award LOT.
- Server-side redeem-code creation/claim limits and claim history. No codes are created by default.
- Admin balance adjustment, password reset, user ban/unban, code/claim review, and one-time Virat admin bootstrap through server-side functions.
- Refined VStocks cards with ticker, simulated unit price, portfolio and trade history.

## Setup and deployment

1. In the Firebase Console, open project **lotsome**. Enable **Authentication → Sign-in method → Email/Password**. Create a **Cloud Firestore** database and enable **Storage**.
2. Install Node.js 20 and the Firebase CLI. From this `lot-ecosystem/` directory, run:

   ```bash
   npm install
   cd functions && npm install && cd ..
   firebase login
   firebase use --add
   ```

   Select the `lotsome` project when prompted. The `.firebaserc.example` file shows the intended project ID; rename it to `.firebaserc` if you prefer to select the project without the interactive command.

3. Set the one-time admin bootstrap secret. Use a long, unique value and do not put it in source code or share it:

   ```bash
   firebase functions:secrets:set LOT_ADMIN_BOOTSTRAP_SECRET
   ```

4. Deploy the backend, security rules, Storage rules, and website:

   ```bash
   firebase deploy --only functions,firestore:rules,storage,hosting
   ```

5. Open the deployed site and create the account named **Virat** with a password of at least 6 characters. Sign in to that account. In **Dashboard**, use **One-time Virat admin setup** and enter the secret you configured in step 3. This function only allows the Virat username to bootstrap, and refuses if another administrator already exists. Keep the secret private and do not reuse it elsewhere.

6. Test signup/login, LOT Shop purchases, VPay transfers, VStocks trades, code claims, and minigames with separate accounts. Firebase may ask you to enable billing or select a suitable plan for Cloud Functions/Storage deployment, depending on your project and region.

## Important security notes
- The Firebase web config and API key are public client configuration; they are not server secrets. Security comes from Firebase Auth, Firestore/Storage Rules, and Cloud Functions validation. Never put service-account credentials or private secrets in `public/`.
- LOT is virtual in-app currency only. VStocks prices are simulated, not investment data. Minigame rewards are limited server-side, but review the rules, quotas, monitoring, and abuse controls before opening a public service to many users.
- This ZIP configures the app and backend but does **not** deploy anything to Firebase by itself. You must complete the console setup and deployment steps above.
- The code does not create default redeem codes or give new accounts a starting LOT balance.
