# PAKHI ID Store — Admin Panel

Node.js + SQLite starter project. Includes admin login, editable per-ID rate, editable UPI ID/payee, amount-specific UPI QR generation, news and announcement management, ID/password inventory, encrypted passwords at rest, UTR order submissions, and manual approve/reject/credential assignment.

## Important payment limitation
A UPI QR creates a payment intent; it does **not** verify that money was received. Admin must check their bank/UPI app before approving an order. Automatic payment confirmation requires a supported payment gateway with server-side webhook/signature verification. Never trust a UTR string alone. This starter does not automatically send credentials to customers; credentials are visible to admin after approval.

## Setup
1. Install Node.js 18+.
2. Copy `.env.example` to `.env`.
3. Create admin password hash: `node -e "require('bcryptjs').hash('YourStrongPassword',12).then(console.log)"`; paste output into `ADMIN_PASSWORD_HASH`.
4. Generate encryption key: `node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"`; paste into `CREDENTIAL_ENCRYPTION_KEY`. Keep it safe or saved passwords cannot be decrypted.
5. Set a long random `SESSION_SECRET` and choose `ADMIN_USERNAME`.
6. Run `npm install`, then `npm start`.
7. Visit `http://localhost:3000/admin/login`, sign in, set price/UPI, add news and inventory.

## Render deployment
- Use a Node.js Web Service with Build Command `npm install` and Start Command `npm start`.
- Attach a persistent disk mounted at `/var/data`, then set `DATA_DIR=/var/data` in environment variables. The app stores both SQLite database files on that disk. Free Render instances do not support persistent disks.
- Configure `SESSION_SECRET`, `ADMIN_USERNAME`, `ADMIN_PASSWORD_HASH`, and `CREDENTIAL_ENCRYPTION_KEY` as private environment variables. Use a 64-character hex encryption key.
- Never upload `.env`, database files, real credentials, or secret values to GitHub. Use HTTPS and test before real orders/payments.

## Production checks added
- `/health` endpoint for basic service health checks.
- Production startup refuses to run when required security environment variables are missing or malformed.
- Duplicate UTR/RRN submissions are rejected. Admin must still verify payment in their bank/UPI app.

## Important Render free-plan note
This app uses SQLite for orders, inventory, settings, and sessions. SQLite data is not persistent on a typical Render free web service filesystem and can be lost on restart/redeploy. Do not use this as a live store with real orders or credentials until durable storage is configured (for example, a persistent disk on a plan that supports it, or a migration to a managed persistent database). Never treat a submitted UTR as proof of payment.
