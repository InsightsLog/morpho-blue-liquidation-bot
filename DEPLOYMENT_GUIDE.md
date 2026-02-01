# 🚀 Beginner's Complete Guide to Deploying the Morpho Blue Liquidation Bot

Welcome! This guide will walk you through deploying your own liquidation bot step-by-step, even if you've never done anything like this before. We'll cover everything from setting up a wallet to running your bot 24/7.

## 📋 Table of Contents

1. [What is This Bot?](#what-is-this-bot)
2. [Before You Start (Prerequisites)](#before-you-start-prerequisites)
3. [Budget Breakdown ($250)](#budget-breakdown-250)
4. [Step 1: Create a Dedicated Wallet](#step-1-create-a-dedicated-wallet)
5. [Step 2: Get RPC Access (Alchemy)](#step-2-get-rpc-access-alchemy)
6. [Step 3: Choose Your Hosting (Railway Recommended)](#step-3-choose-your-hosting-railway-recommended)
7. [Step 4: Deploy the Bot](#step-4-deploy-the-bot)
8. [Step 5: Deploy the Executor Contract](#step-5-deploy-the-executor-contract)
9. [Step 6: Configure and Run](#step-6-configure-and-run)
10. [Step 7: Monitor Your Bot](#step-7-monitor-your-bot)
11. [Claiming Your Profits](#claiming-your-profits)
12. [Troubleshooting](#troubleshooting)
13. [Security Best Practices](#security-best-practices)
14. [FAQ](#faq)

---

## What is This Bot?

A **liquidation bot** monitors lending protocols (in this case, Morpho Blue) for unhealthy loan positions. When someone's collateral drops below the required threshold, the bot steps in to liquidate the position—paying off part of the debt and receiving the collateral (plus a bonus) in return.

**The profit** comes from the liquidation bonus—you get collateral worth slightly more than the debt you repay. The bot automates this entire process.

### ⚠️ Important Disclaimer

- **This is not guaranteed profit.** You can lose money through gas fees, failed transactions, or market conditions.
- **You need capital at risk.** Your wallet will need ETH/tokens to pay for gas.
- **Competition is fierce.** Many sophisticated bots are running 24/7.
- Start small and learn before scaling up.

---

## Before You Start (Prerequisites)

### What You Need

| Requirement | Description | Difficulty |
|-------------|-------------|------------|
| Basic computer skills | Copy/paste, use websites | Easy |
| A credit/debit card | To pay for hosting | Easy |
| Email address | For account signups | Easy |
| Patience | This takes 1-2 hours to set up | - |

### What You DON'T Need

- ❌ Programming knowledge
- ❌ Server administration skills
- ❌ Prior crypto/DeFi experience (helpful but not required)

---

## Budget Breakdown ($250)

Here's how your $250 budget could be allocated:

| Expense | Monthly Cost | First Month | Notes |
|---------|-------------|-------------|-------|
| **Hosting (Railway)** | $5-20 | $5-20 | Pay-as-you-go |
| **RPC Provider (Alchemy)** | $0 | $0 | Free tier sufficient |
| **Gas for Operations** | $50-150 | $100-200 | Varies by activity |
| **Executor Deployment** | One-time | $10-50 | Per chain |
| **Safety Buffer** | - | $50+ | For unexpected costs |

**Recommended starting allocation:**
- $100-150 in wallet for gas + executor deployment
- $50 for first 2-3 months of hosting
- $50-100 as reserve/safety buffer

---

## Step 1: Create a Dedicated Wallet

> ⚠️ **CRITICAL SECURITY RULE:** Never use your main wallet! Create a brand new wallet just for this bot.

### Why a Dedicated Wallet?

- If the private key is compromised, only bot funds are at risk
- Easier to track bot profits/losses
- Cleaner transaction history

### Create Your Wallet

#### Option A: MetaMask (Beginner-Friendly)

1. Go to [metamask.io](https://metamask.io)
2. Download the browser extension
3. Click "Create a new wallet"
4. **WRITE DOWN YOUR SEED PHRASE ON PAPER** (not digitally!)
5. Set a strong password
6. Click the three dots → "Account details" → "Show private key"
7. **Save this private key securely** (you'll need it later)

#### Option B: Command Line (More Secure)

If you're comfortable with terminal:

```bash
# Using cast from Foundry
cast wallet new
```

### Fund Your Wallet

Transfer ETH to your new wallet address:

| Chain | Recommended Starting Amount | Purpose |
|-------|---------------------------|---------|
| Ethereum Mainnet | 0.1-0.2 ETH (~$250-500) | Gas + deployment |
| Base | 0.01-0.05 ETH (~$25-125) | Gas + deployment |
| Arbitrum | 0.01-0.05 ETH (~$25-125) | Gas + deployment |

> **Tip for $250 budget:** Start with ONE chain (Base recommended—lower gas costs) with ~$100 in ETH.

---

## Step 2: Get RPC Access (Alchemy)

An **RPC (Remote Procedure Call)** lets your bot communicate with the blockchain. Think of it as your bot's "phone line" to Ethereum.

### Set Up Alchemy (Free Tier)

1. Go to [alchemy.com](https://www.alchemy.com)
2. Click "Sign Up" → Create account (use your email)
3. Once logged in, click "Create new app"
4. Fill in:
   - **Name:** `morpho-liquidation-bot`
   - **Chain:** Select the chain you want (e.g., "Ethereum Mainnet" or "Base")
5. Click "Create app"
6. Click on your new app → "API Key" tab
7. Copy your **HTTPS URL** - it looks like:
   ```
   https://eth-mainnet.g.alchemy.com/v2/YOUR-API-KEY-HERE
   ```

### Create Apps for Each Chain You Want

Repeat for each blockchain:

| Chain | Chain ID | Alchemy Network Name |
|-------|----------|---------------------|
| Ethereum Mainnet | 1 | Ethereum Mainnet |
| Base | 8453 | Base Mainnet |
| Arbitrum | 42161 | Arbitrum Mainnet |

> **Note:** Save each RPC URL. You'll need them formatted as `RPC_URL_1`, `RPC_URL_8453`, etc.

---

## Step 3: Choose Your Hosting (Railway Recommended)

### Option A: Railway (Recommended for Beginners)

**Why Railway?**
- ✅ One-click deployment from GitHub
- ✅ $5 free credit to start
- ✅ No server management needed
- ✅ Auto-restarts if bot crashes
- ✅ Easy environment variable management

**Cost:** ~$5-20/month depending on usage

### Option B: DigitalOcean/Vultr VPS

**Why VPS?**
- ✅ Fixed monthly cost ($5-10/month)
- ✅ More control
- ❌ Requires more technical knowledge
- ❌ Manual setup and maintenance

---

## Step 4: Deploy the Bot

### Railway Deployment (Recommended)

#### 4.1 Create Railway Account

1. Go to [railway.app](https://railway.app)
2. Click "Login" → "Login with GitHub"
3. If you don't have GitHub, create one at [github.com](https://github.com)
4. Authorize Railway to access your GitHub

#### 4.2 Fork the Repository

1. Go to the original repo: [github.com/morpho-org/morpho-blue-liquidation-bot](https://github.com/morpho-org/morpho-blue-liquidation-bot)
2. Click the "Fork" button (top right)
3. Select your account
4. Now you have your own copy at `github.com/YOUR-USERNAME/morpho-blue-liquidation-bot`

#### 4.3 Deploy to Railway

1. In Railway dashboard, click "New Project"
2. Select "Deploy from GitHub repo"
3. Find and select `morpho-blue-liquidation-bot`
4. Railway will detect the Dockerfile and start building

#### 4.4 Add PostgreSQL Database

The bot needs a database to track blockchain data:

1. In your Railway project, click "New"
2. Select "Database" → "PostgreSQL"
3. Once created, click on the PostgreSQL service
4. Go to "Variables" tab
5. Copy the `DATABASE_URL` value

#### 4.5 Configure Environment Variables

1. Click on your bot service (not the database)
2. Go to "Variables" tab
3. Click "New Variable" for each of these:

**Required Variables (for each chain):**

```
# For Ethereum Mainnet (Chain ID: 1)
RPC_URL_1 = https://eth-mainnet.g.alchemy.com/v2/YOUR-API-KEY

# For Base (Chain ID: 8453)
RPC_URL_8453 = https://base-mainnet.g.alchemy.com/v2/YOUR-API-KEY

# Your private key (same for all chains)
LIQUIDATION_PRIVATE_KEY = 0xYOUR_PRIVATE_KEY_HERE

# Database URL (copy from PostgreSQL service)
POSTGRES_DATABASE_URL = postgresql://postgres:xxxx@xxx.railway.app:5432/railway
```

> ⚠️ **Never share your private key!** Railway keeps variables encrypted.

### Alternative: VPS Deployment

<details>
<summary>Click to expand VPS instructions</summary>

#### Requirements
- Ubuntu 22.04 VPS ($5-10/month from DigitalOcean, Vultr, or Hetzner)
- SSH access

#### Setup Steps

```bash
# 1. Connect to your VPS
ssh root@YOUR_VPS_IP

# 2. Update system
apt update && apt upgrade -y

# 3. Install Node.js 20+
curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
apt install -y nodejs

# 4. Install pnpm
npm install -g pnpm

# 5. Install Docker (for PostgreSQL)
curl -fsSL https://get.docker.com | sh

# 6. Clone the repository
git clone https://github.com/morpho-org/morpho-blue-liquidation-bot.git
cd morpho-blue-liquidation-bot

# 7. Install dependencies
pnpm install

# 8. Start PostgreSQL
docker-compose up -d

# 9. Create .env file
cp .env.example .env
nano .env  # Edit with your values

# 10. Run the bot (use screen or pm2 for persistence)
pnpm liquidate
```

**Keep bot running with PM2:**
```bash
npm install -g pm2
pm2 start "pnpm liquidate" --name liquidation-bot
pm2 save
pm2 startup  # Follow the instructions it gives
```

</details>

---

## Step 5: Deploy the Executor Contract

The bot uses a special "executor" contract to perform liquidations. You need to deploy one per chain.

### Option A: Using the Web Interface (Easiest)

1. Go to [rubilmax.github.io/executooor](https://rubilmax.github.io/executooor/)
2. Connect your bot wallet (the one with the private key you're using)
3. Select the network (Ethereum, Base, etc.)
4. Click "Deploy"
5. Confirm the transaction in your wallet
6. **Save the deployed contract address!**

### Option B: Using the Bot's Built-in Command

If you have the bot running locally:

```bash
# Make sure .env has RPC_URL and LIQUIDATION_PRIVATE_KEY set
pnpm deploy:executor
```

This deploys to ALL chains configured in your .env file and prints the addresses.

### Add Executor Addresses to Railway

After deploying, add these to your Railway variables:

```
# Replace with your actual deployed addresses
EXECUTOR_ADDRESS_1 = 0xYOUR_MAINNET_EXECUTOR_ADDRESS
EXECUTOR_ADDRESS_8453 = 0xYOUR_BASE_EXECUTOR_ADDRESS
```

---

## Step 6: Configure and Run

### Verify All Variables Are Set

Your Railway (or .env) should have these for each chain:

| Variable | Example | Description |
|----------|---------|-------------|
| `RPC_URL_<chainId>` | `https://eth-mainnet.g.alchemy.com/v2/xxx` | Blockchain connection |
| `LIQUIDATION_PRIVATE_KEY` | `0xabc123...` | Your bot wallet's private key |
| `EXECUTOR_ADDRESS_<chainId>` | `0xdef456...` | Your deployed executor contract |
| `POSTGRES_DATABASE_URL` | `postgresql://...` | Database connection |

### Start the Bot

**Railway:** The bot auto-starts after adding variables. Check the "Logs" tab to see output.

**VPS:** Run `pnpm liquidate`

### What to Expect

1. **Indexing Phase:** Bot downloads blockchain history (can take 10-60 minutes per chain)
2. **Monitoring Phase:** Bot watches for liquidatable positions
3. **Execution Phase:** When opportunities arise, bot executes liquidations

You'll see logs like:
```
[INFO] Starting liquidation bot...
[INFO] Indexing chain 8453 (Base)... 45% complete
[INFO] Chain 8453 fully indexed. Watching for opportunities...
[INFO] Found liquidatable position: 0x... (potential profit: $X.XX)
```

---

## Step 7: Monitor Your Bot

### Railway Dashboard

1. Go to your Railway project
2. Click on the bot service
3. View "Logs" for real-time activity
4. Check "Metrics" for CPU/memory usage

### Health Checks

The bot exposes a health endpoint. You can set up monitoring with:

- [UptimeRobot](https://uptimerobot.com) (free)
- [Better Uptime](https://betteruptime.com)

### Alerts

Set up notifications for:
- Bot going offline
- Successful liquidations (check logs)
- Error patterns

---

## Claiming Your Profits

Profits accumulate in your Executor contract. To withdraw:

```bash
# On your local machine or VPS with the bot installed
pnpm skim --chainId 8453 --token 0xTOKEN_ADDRESS --recipient 0xYOUR_WALLET
```

Or transfer tokens manually by interacting with your executor contract.

**Common tokens to claim:**
- WETH: `0x4200000000000000000000000000000000000006` (Base)
- USDC: `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` (Base)

---

## Troubleshooting

### Bot won't start

| Issue | Solution |
|-------|----------|
| "RPC_URL not found" | Check environment variable names match chain IDs |
| "Invalid private key" | Ensure key starts with `0x` and is 64 characters |
| "Executor not deployed" | Deploy executor contract first |

### Indexing takes forever

- This is normal for first run
- Ethereum mainnet can take 30-60+ minutes
- Use `PONDER_SERVICE_URL` if available for faster sync

### Transaction failures

| Error | Cause | Fix |
|-------|-------|-----|
| "Insufficient funds" | Not enough ETH for gas | Add more ETH to wallet |
| "Nonce too low" | Transaction stuck | Wait or increase gas |
| "Execution reverted" | Someone else liquidated first | This is normal, keep running |

### Database errors

```bash
# Railway: Delete and recreate PostgreSQL service
# VPS: Reset with
docker-compose down -v
docker-compose up -d
```

---

## Security Best Practices

### DO ✅

- Use a dedicated wallet with only necessary funds
- Keep private keys in environment variables (never in code)
- Use Railway's encrypted variables feature
- Regularly withdraw profits to a secure wallet
- Start with small amounts to test

### DON'T ❌

- Never use your main wallet
- Never commit private keys to GitHub
- Don't share your RPC URLs publicly
- Don't run on untrusted servers

### Recommended Security Setup

```
Main Wallet ──► Bot Wallet ──► Executor Contract ──► Profits
     │              │                                    │
     │         (limited funds)                           │
     │                                                   │
     └────────────── Withdraw when accumulated ◄────────┘
```

---

## FAQ

### How much can I make?

There's no guaranteed income. Profits depend on:
- Market volatility
- Competition from other bots
- Gas costs
- Which chains you run on

Some bots make nothing, others make significant profits. Start small!

### Which chain should I start with?

**For $250 budget:** Start with **Base** because:
- Lower gas costs (~10x cheaper than Ethereum)
- Active Morpho Blue markets
- Good RPC support

### Do I need to keep my computer running?

No! That's why we use Railway or a VPS—they run 24/7 in the cloud.

### Can I run on multiple chains?

Yes! Add more `RPC_URL_<chainId>` and `EXECUTOR_ADDRESS_<chainId>` variables. But start with one chain first.

### How do I update the bot?

**Railway:** Push to your GitHub fork, Railway auto-deploys

**VPS:**
```bash
cd morpho-blue-liquidation-bot
git pull
pnpm install
pm2 restart liquidation-bot
```

### What if I lose money?

- Gas fees are a cost even if liquidations fail
- Start with small amounts you can afford to lose
- Monitor closely in the first weeks

---

## Next Steps

1. ✅ Deploy on one chain (Base recommended)
2. ✅ Monitor for a week
3. ✅ Add more chains if profitable
4. ✅ Consider running your own Ponder service for speed
5. ✅ Join the [Morpho Discord](https://discord.morpho.org) for community support

---

## Need Help?

- **Morpho Documentation:** [docs.morpho.org](https://docs.morpho.org)
- **Morpho Discord:** [discord.morpho.org](https://discord.morpho.org)
- **GitHub Issues:** [Report bugs here](https://github.com/morpho-org/morpho-blue-liquidation-bot/issues)

---

*Good luck with your liquidation bot! Remember: start small, learn the ropes, and scale up gradually.* 🚀
