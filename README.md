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

Deploy on a Node.js host with persistent disk for SQLite, HTTPS, and environment variables configured privately. Never upload `.env` or `store.db` publicly. Review and test before using with real customers/payments.
