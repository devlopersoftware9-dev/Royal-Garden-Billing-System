# Royal Garden Water Billing System

Society ke gharon ke liye water (unit base) + per marla charges ka billing system.

## Features
- 200 ghar, sold/unsold status (sirf sold gharon ka bill)
- Per marla charges (rate settings se badla ja sakta hai)
- Water bill: (nayi reading − pichli reading) × per unit rate
- Month-wise bill generate: ek ghar ya sab ghar
- Pichla baqaya khud agle bill mein, fine ka button (ek ghar / sab unpaid)
- Pending list, payments (Cash / JazzCash / Bank / Easypaisa), partial payment
- Urdu bill: PDF aur image download, WhatsApp message
- Settings: JazzCash, bank account, IBAN, QR code, reader PIN
- Meter reader mode (PIN ke saath) — sirf reading punch karne ka page

## Note
`index.html` Claude artifact ke taur par chalta hai aur data ke liye Claude ka shared database (`window.claude`) use karta hai.
Isay seedha browser ya GitHub Pages par kholne se data save nahi hoga — live app claude.ai artifact link se kholein.
