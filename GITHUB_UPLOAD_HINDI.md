# PAKHI ID Store — GitHub Upload Guide

## GitHub par upload
1. ZIP ko extract karein.
2. GitHub par naya repository banayein, jaise `pakhi-id-store`.
3. Extract kiye gaye folder ke andar ki files repository mein upload karein (`server.js`, `package.json`, `views/`, `public/`, `.env.example`, README files, etc.).
4. `.env` file, database, real IDs/passwords, UPI secrets ya encryption/session keys kabhi upload na karein.

## Important: GitHub Pages par nahi chalega
Yeh Node.js + SQLite backend app hai; GitHub Pages sirf static websites host karta hai. Is app ko Node.js hosting (jaise Render par Web Service) aur persistent disk/database chahiye.

## Run locally
- Node.js 20+ install karein.
- `.env.example` ko `.env` naam se copy karke sab secret values set karein.
- Dependencies: `npm install`
- Start: `npm start`
- Open: `http://localhost:3000`

Detailed security and deployment notes ke liye `README.md` dekhein. UTR ko bank/UPI app mein verify karke hi order approve karein; UTR text apne aap payment ka proof nahi hai.
