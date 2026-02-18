# ⬡ SolForge — SPL Token Creator

A full-stack web application for creating SPL tokens on the Solana blockchain with a 3-tier package model.

## 🏗 Architecture

```
solana-token-creator/
├── backend/            # Node.js + Express API
│   ├── server.js       # Main server
│   ├── package.json
│   └── .env.example
├── frontend/           # React + Vite SPA
│   ├── src/
│   │   ├── App.jsx
│   │   ├── components/
│   │   └── utils/
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
├── package.json        # Root scripts
├── .env.example
├── Procfile            # Railway deploy
└── README.md
```

## 💎 Package Plans

| Plan    | Price   | Authorities      | Features                    |
|---------|---------|------------------|---------------------------  |
| Starter | 0.25 SOL | Always Revoked   | Token + metadata + mint     |
| Pro     | 0.45 SOL | Optional control  | +Advanced authority + update |
| Launch  | 0.85 SOL | Optional control  | +Liquidity pool + LP lock   |

## 🚀 Local Development

### Prerequisites
- Node.js 18+
- npm 8+
- Phantom Wallet browser extension
- (For mainnet) SOL in your wallet

### 1. Clone & Install

```bash
git clone https://github.com/YOUR_USERNAME/solana-token-creator.git
cd solana-token-creator
npm run install:all
```

### 2. Configure Environment

**Backend** (`backend/.env`):
```env
PORT=3001
NODE_ENV=development
SOLANA_NETWORK=devnet              # Use devnet for testing!
SOLANA_RPC_URL=https://api.devnet.solana.com
PLATFORM_WALLET_ADDRESS=YOUR_WALLET_ADDRESS
CORS_ORIGIN=http://localhost:5173
```

**Frontend** (`frontend/.env`):
```env
VITE_API_URL=http://localhost:3001
VITE_SOLANA_NETWORK=devnet         # Match backend
```

> ⚠️ **For testing**, use `devnet`. Get free SOL at https://faucet.solana.com

### 3. Run Development Servers

Open two terminals:

**Terminal 1 — Backend:**
```bash
npm run dev:backend
# Server starts on http://localhost:3001
```

**Terminal 2 — Frontend:**
```bash
npm run dev:frontend
# App opens on http://localhost:5173
```

### 4. Test the Flow

1. Set Phantom Wallet to Devnet
2. Get devnet SOL from https://faucet.solana.com
3. Open http://localhost:5173
4. Connect Phantom, select a plan, create a token

---

## 🚂 Deploy on Railway

### Backend Deployment

1. **Push to GitHub:**
```bash
git add .
git commit -m "Initial commit"
git push origin main
```

2. **Create Railway project:**
   - Go to https://railway.app
   - Click "New Project" → "Deploy from GitHub repo"
   - Select your repository

3. **Set Root Directory:**
   - In Railway settings, set `Root Directory` to `backend`

4. **Add Environment Variables** in Railway dashboard:
```
PORT=3001
NODE_ENV=production
SOLANA_NETWORK=mainnet-beta
SOLANA_RPC_URL=https://api.mainnet-beta.solana.com
PLATFORM_WALLET_ADDRESS=YOUR_MAINNET_WALLET_ADDRESS
CORS_ORIGIN=https://your-frontend-domain.vercel.app
```

5. Railway auto-detects Node.js and runs `npm start`.

### Frontend Deployment (Vercel)

1. Go to https://vercel.com → New Project → Import from GitHub
2. Set **Framework Preset**: Vite
3. Set **Root Directory**: `frontend`
4. Add **Environment Variables**:
```
VITE_API_URL=https://your-railway-backend-url.railway.app
VITE_SOLANA_NETWORK=mainnet-beta
```
5. Deploy!

### Alternative: Railway for Both

To deploy frontend on Railway too:
1. Create a second Railway service from the same repo
2. Set Root Directory to `frontend`
3. Add build command: `npm run build`
4. Add start command: `npx serve dist -p $PORT`

---

## 🔐 Environment Variables Reference

### Backend

| Variable | Required | Description |
|----------|----------|-------------|
| `PORT` | No | Server port (default: 3001) |
| `NODE_ENV` | No | `development` or `production` |
| `SOLANA_NETWORK` | Yes | `mainnet-beta`, `devnet`, or `testnet` |
| `SOLANA_RPC_URL` | No | Custom RPC URL (recommended for production) |
| `PLATFORM_WALLET_ADDRESS` | Yes | Your Solana wallet to receive payments |
| `CORS_ORIGIN` | Yes | Frontend URL for CORS |

### Frontend

| Variable | Required | Description |
|----------|----------|-------------|
| `VITE_API_URL` | Yes | Backend API URL |
| `VITE_SOLANA_NETWORK` | Yes | `mainnet-beta` or `devnet` |

---

## 🔒 Security Notes

- ✅ Backend **never** stores user private keys
- ✅ All wallet signing done via Phantom (client-side)
- ✅ Payment verified on-chain before token creation
- ✅ Rate limiting on all API endpoints
- ✅ Input validation on both frontend and backend
- ✅ CORS restricted to frontend domain in production

## 📡 API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/health` | Health check |
| GET | `/api/packages` | Get package info |
| GET | `/api/platform-wallet` | Get platform wallet address |
| POST | `/api/payment/initiate` | Start payment session |
| POST | `/api/payment/verify` | Verify on-chain payment |
| GET | `/api/payment/status/:id` | Check payment status |
| POST | `/api/tokens/register` | Register created token |
| GET | `/api/tokens/recent` | Get recent tokens |
| GET | `/api/logs` | Transaction logs |

## 🛠 Tech Stack

**Frontend**: React 18, Vite, @solana/web3.js, @solana/spl-token  
**Backend**: Node.js, Express, @solana/web3.js, @solana/spl-token  
**Blockchain**: Solana mainnet-beta (or devnet for testing)  
**Wallet**: Phantom

## ⚠️ Disclaimer

This tool is provided as-is for educational and technical purposes. Users are solely responsible for their token usage, compliance with applicable laws, and any financial outcomes. This is not financial or legal advice.
