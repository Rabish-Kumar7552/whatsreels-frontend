# WhatsApp + Reels — Backend

## Setup (pehli baar)

1. **Node.js install karo** (agar nahi hai): https://nodejs.org (LTS version)

2. **MongoDB install karo** — 2 options:
   - **Local:** https://www.mongodb.com/try/download/community install karo
   - **Cloud (easier, recommended):** https://www.mongodb.com/cloud/atlas free account banao, connection string milega

3. **Terminal mein backend folder ke andar jaake:**
   ```bash
   npm install
   ```

4. **.env file banao:**
   - `.env.example` ko copy karke `.env` naam se save karo
   - `MONGO_URI` mein apna MongoDB connection string daalo
   - `JWT_SECRET` mein koi bhi random long string daal do (jaise `mySuperSecretKey123!@#`)

5. **Server chalu karo:**
   ```bash
   npm run dev
   ```
   Agar sab sahi hai toh terminal mein dikhega:
   ```
   ✅ MongoDB Connected: ...
   🚀 Server running on http://localhost:5000
   ```

## Abhi tak ke APIs (test karne ke liye Postman/Thunder Client use karo)

### Auth
- `POST /api/auth/send-otp` — body: `{ "phoneNumber": "+919876543210" }`
- `POST /api/auth/verify-otp` — body: `{ "phoneNumber": "+919876543210", "otp": "123456" }`
  → response mein `token` milega, isko save kar lo
- `PUT /api/auth/complete-profile` — header: `Authorization: Bearer <token>`, body: `{ "name": "Rabish", "about": "..." }`

### Reels
- `POST /api/reels` — header: `Authorization: Bearer <token>`, body: `{ "videoUrl": "...", "caption": "..." }`
- `GET /api/reels/feed?page=1&limit=5` — header: `Authorization: Bearer <token>`
- `PUT /api/reels/:id/like` — header: `Authorization: Bearer <token>`
- `POST /api/reels/:id/comment` — body: `{ "text": "Nice reel!" }`
- `POST /api/reels/:id/share`
- `PUT /api/reels/:id/save`

## Testing tip

OTP verification ke liye abhi Twilio connect nahi kiya hai (paisa/setup lagta hai).
Development mode mein, jo OTP generate hota hai wo terminal console mein print ho jata hai —
wahan se copy karke `verify-otp` mein use kar lo. Baad mein Twilio integrate karenge jab
real users ke liye ready ho.

## Agla step (jo hum saath banayenge)

- [ ] Chat routes (send message, get chat history) + Socket.io real-time events
- [ ] Status routes (upload, view, 24hr auto-delete)
- [ ] Group chat routes
- [ ] File upload (Cloudinary/Multer integration)
- [ ] Frontend ko in APIs se connect karna
