# Royal Garden Water Billing System

Water (unit-based) + per-marla maintenance billing for Royal Garden society.

**Who sees what**
| Login | Can see / do |
|---|---|
| Admin | Everything: plots, readings, bills, payments, settings, logins |
| Meter reader | Only the reading screen (plot list + enter reading). Previous reading / owner name can be hidden in Settings |
| Resident (one per plot) | Only **their own plot's** bills and payments. Can download the bill and submit a payment (TID + screenshot) for approval |

Security is enforced by Firebase on the server (`firestore.rules`), not just hidden in the screen.

## One-time setup (about 10 minutes)

1. Go to https://console.firebase.google.com → **Add project** → name it `royal-garden-billing` (Google Analytics can be off).
2. **Build → Authentication → Get started → Sign-in method → Email/Password → Enable → Save.**
3. **Build → Firestore Database → Create database** → choose a location (e.g. `asia-south1` Mumbai) → **Start in production mode**.
4. Firestore → **Rules** tab → delete everything there, paste the whole `firestore.rules` file from this repo → **Publish**.
5. ⚙️ **Project settings → General → Your apps → Web (`</>`)** → app nickname `Royal Garden` → **Register app**. Copy the `firebaseConfig = { ... }` block.
6. In `index.html`, replace `null` between `/*CONFIG-START*/` and `/*CONFIG-END*/` with that config object.
   (The Firebase web config is meant to be public — your data is protected by the rules, not by hiding this key.)
7. Host the site (GitHub Pages: repo **Settings → Pages → Deploy from branch**). Then in Firebase **Authentication → Settings → Authorized domains** add your site domain (e.g. `yourname.github.io`).
8. Open the site straight away and create the **admin account** (the first account created becomes admin).
9. Import your Excel profile (or a backup from the old app), set rates and payment details in **Settings**, then go to **Logins → Create logins for all** and send each resident their username/password on WhatsApp.

Free Firebase (Spark) limits are far above what an ~200-house society needs.

## How it works
- **Bills:** per marla charges + (current − previous reading) × unit rate + previous balance + fines. Generated month-wise for all sold plots; regenerate keeps payments and fines.
- **Payments:** residents pay by JazzCash / bank / QR, then submit the TID and screenshot. The admin approves it on the Pending page and it is added to the bill.
- **Passwords:** shown only once when created/reset. Residents can change their own password. If someone forgets, the admin uses **Reset password**.
