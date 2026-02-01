# 🚀 Beginner's Guide: Run the Morpho Blue Liquidation Bot on YOUR Computer

This guide shows you how to run the liquidation bot **locally on your own computer** (Windows, Mac, or Linux). No cloud services needed—just your machine.

> ⚠️ **Important:** Your computer must stay ON and connected to the internet for the bot to work. If you close your laptop or lose internet, the bot stops.

---

## 📋 Table of Contents

1. [What is This Bot?](#what-is-this-bot)
2. [What You'll Need](#what-youll-need)
3. [Budget Breakdown ($250)](#budget-breakdown-250)
4. [Step 1: Install Docker Desktop](#step-1-install-docker-desktop)
5. [Step 2: Create a Dedicated Wallet](#step-2-create-a-dedicated-wallet)
6. [Step 3: Get a Free RPC URL](#step-3-get-a-free-rpc-url)
7. [Step 4: Deploy Your Executor Contract](#step-4-deploy-your-executor-contract)
8. [Step 5: Download and Configure the Bot](#step-5-download-and-configure-the-bot)
9. [Step 6: Start the Bot](#step-6-start-the-bot)
10. [Step 7: Monitor and Claim Profits](#step-7-monitor-and-claim-profits)
11. [Stopping and Restarting](#stopping-and-restarting)
12. [Troubleshooting](#troubleshooting)
13. [FAQ](#faq)

---

## What is This Bot?

A **liquidation bot** watches for unhealthy loans on Morpho Blue. When someone's collateral drops too low, your bot can liquidate it and earn a bonus. The bot automates finding and executing these opportunities.

### ⚠️ Important Disclaimer

- **No guaranteed profit.** You can lose money on gas fees and failed transactions.
- **Your wallet needs ETH** to pay for gas.
- **Competition is real.** Other bots are running too.
- Start small and learn!

---

## What You'll Need

| Item | Where to Get It | Cost |
|------|-----------------|------|
| A computer (Windows/Mac/Linux) | You probably have one! | $0 |
| Docker Desktop | Free download | $0 |
| MetaMask browser extension | metamask.io | $0 |
| Alchemy account | alchemy.com | $0 (free tier) |
| ETH in your wallet | Buy on Coinbase, etc. | ~$100-200 |

**Total software cost: $0**

---

## Budget Breakdown ($250)

Since you're running locally, you save on hosting! Here's how to use your $250:

| Expense | Cost | Notes |
|---------|------|-------|
| **Hosting** | $0 | Your computer! |
| **RPC Provider** | $0 | Alchemy free tier |
| **Executor Deployment** | $10-50 | One-time per chain |
| **Gas for Operations** | $150-200 | Main expense |
| **Safety Buffer** | $50+ | For unexpected costs |

**Recommended:** Start with **Base** chain (~$50-100 in ETH) for lower gas costs.

---

## Step 1: Install Docker Desktop

Docker lets you run the bot in a container—no complicated setup needed.

### Windows

1. Go to [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)
2. Click **"Download for Windows"**
3. Run the installer (`Docker Desktop Installer.exe`)
4. Follow the prompts (use defaults)
5. **Restart your computer** when asked
6. Open Docker Desktop from your Start menu
7. Wait for it to say "Docker Desktop is running"

### Mac

1. Go to [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)
2. Click **"Download for Mac"** (choose Intel or Apple Chip based on your Mac)
3. Open the `.dmg` file
4. Drag Docker to your Applications folder
5. Open Docker from Applications
6. Click "Open" if you see a security warning
7. Wait for it to say "Docker Desktop is running"

### Linux (Ubuntu/Debian)

Open a terminal and run:

```bash
# Install Docker
curl -fsSL https://get.docker.com | sh

# Add yourself to docker group (so you don't need sudo)
sudo usermod -aG docker $USER

# Log out and back in, then verify:
docker --version
```

### ✅ Verify Docker is Working

Open a terminal (or PowerShell on Windows) and run:

```bash
docker --version
```

You should see something like: `Docker version 24.0.x`

---

## Step 2: Create a Dedicated Wallet

> ⚠️ **NEVER use your main wallet!** Create a new one just for this bot.

### Create a New MetaMask Wallet

1. Install MetaMask: [metamask.io](https://metamask.io)
2. Click the MetaMask icon → Click your account icon → **"Add account or hardware wallet"**
3. Choose **"Add a new account"**
4. Name it "Liquidation Bot"
5. Click on the account → Three dots → **"Account details"**
6. Click **"Show private key"**
7. Enter your password
8. **COPY AND SAVE THE PRIVATE KEY SOMEWHERE SAFE** (you'll need it soon!)

The private key looks like: `0x1234abcd...` (64 characters after 0x)

### Fund Your Wallet

Send ETH to your new wallet address. For **Base** chain (recommended for beginners):

1. Get your wallet address from MetaMask
2. Send **0.02-0.05 ETH** (~$50-125) to that address on Base
3. You can bridge from Ethereum using [bridge.base.org](https://bridge.base.org)

---

## Step 3: Get a Free RPC URL

An RPC URL lets your bot talk to the blockchain.

### Set Up Alchemy (Free)

1. Go to [alchemy.com](https://www.alchemy.com)
2. Click **"Sign Up"** and create an account
3. Once logged in, click **"Create new app"**
4. Fill in:
   - **Name:** `morpho-bot`
   - **Chain:** Choose your chain (e.g., "Base Mainnet")
5. Click **"Create app"**
6. Click on your app → **"API Key"** tab
7. Copy the **HTTPS** URL

It looks like: `https://base-mainnet.g.alchemy.com/v2/YOUR-KEY-HERE`

**Save this URL!** You'll need it in Step 5.

### Chain IDs Reference

| Chain | Chain ID | Alchemy Name |
|-------|----------|--------------|
| Ethereum | 1 | Ethereum Mainnet |
| Base | 8453 | Base Mainnet |
| Arbitrum | 42161 | Arbitrum Mainnet |

---

## Step 4: Deploy Your Executor Contract

The bot needs a special contract to execute liquidations. You only do this **once per chain**.

### Easiest Method: Web Interface

1. Go to [rubilmax.github.io/executooor](https://rubilmax.github.io/executooor/)
2. Click **"Connect Wallet"** and connect your bot wallet (from Step 2)
3. Switch to your desired network (Base, Ethereum, etc.)
4. Click **"Deploy"**
5. Confirm the transaction in MetaMask
6. **COPY THE DEPLOYED CONTRACT ADDRESS!**

The address looks like: `0xAbCd1234...`

**Save this address!** You'll need it in Step 5.

---

## Step 5: Download and Configure the Bot

### 5.1 Download the Bot

**Option A: Download ZIP (Easiest)**

1. Go to [github.com/morpho-org/morpho-blue-liquidation-bot](https://github.com/morpho-org/morpho-blue-liquidation-bot)
2. Click the green **"Code"** button
3. Click **"Download ZIP"**
4. Extract the ZIP to a folder (e.g., `C:\liquidation-bot` on Windows or `~/liquidation-bot` on Mac/Linux)

**Option B: Using Git**

```bash
git clone https://github.com/morpho-org/morpho-blue-liquidation-bot.git
cd morpho-blue-liquidation-bot
```

### 5.2 Create Your Configuration File

1. Open the bot folder
2. Find the file called `.env.example`
3. **Make a copy** and rename it to `.env` (just `.env`, no `.example`)

### 5.3 Edit the .env File

Open `.env` in a text editor (Notepad on Windows, TextEdit on Mac) and fill in your values:

**For Base chain (recommended):**

```bash
# Your Alchemy RPC URL (from Step 3)
RPC_URL_8453=https://base-mainnet.g.alchemy.com/v2/YOUR-KEY-HERE

# Your executor contract address (from Step 4)
EXECUTOR_ADDRESS_8453=0xYOUR_EXECUTOR_ADDRESS_HERE

# Your wallet's private key (from Step 2)
# IMPORTANT: Include the 0x at the start!
LIQUIDATION_PRIVATE_KEY_8453=0xYOUR_PRIVATE_KEY_HERE
```

**For Ethereum mainnet (higher gas costs):**

```bash
RPC_URL_1=https://eth-mainnet.g.alchemy.com/v2/YOUR-KEY-HERE
EXECUTOR_ADDRESS_1=0xYOUR_EXECUTOR_ADDRESS_HERE
LIQUIDATION_PRIVATE_KEY_1=0xYOUR_PRIVATE_KEY_HERE
```

**Example completed .env for Base:**

```bash
RPC_URL_8453=https://base-mainnet.g.alchemy.com/v2/abc123xyz789
EXECUTOR_ADDRESS_8453=0x742d35Cc6634C0532925a3b844Bc9e7595f2bD12
LIQUIDATION_PRIVATE_KEY_8453=0x4c0883a69102937d6231471b5dbb6204fe5129617082790abe5d523bd2c246a3
```

> ⚠️ **Never share your .env file or private key with anyone!**

---

## Step 6: Start the Bot

### 6.1 Open a Terminal

**Windows:** Press `Win + R`, type `cmd`, press Enter. Then navigate to your bot folder:
```bash
cd C:\path\to\morpho-blue-liquidation-bot
```

**Mac/Linux:** Open Terminal and navigate:
```bash
cd ~/liquidation-bot/morpho-blue-liquidation-bot
```

### 6.2 Start the Database

The bot needs a database. Docker makes this easy:

```bash
docker-compose up -d
```

You should see:
```
Creating morpho_blue_liquidation_bot_postgres ... done
```

### 6.3 Install Dependencies and Run

**First time only—install Node.js and pnpm:**

**Windows:**
1. Download Node.js from [nodejs.org](https://nodejs.org) (LTS version)
2. Run the installer
3. Open a NEW terminal window

**Mac:**
```bash
brew install node
```

**Linux:**
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo bash -
sudo apt install -y nodejs
```

**Install pnpm (all platforms):**
```bash
npm install -g pnpm
```

**Install bot dependencies:**
```bash
pnpm install
```

**Start the bot:**
```bash
pnpm liquidate
```

### 6.4 What You'll See

```
Starting liquidation bot...
Indexing chain 8453 (Base)...
Progress: 10%... 25%... 50%... 75%... 100%
Chain fully indexed. Watching for liquidatable positions...
```

The first run takes **10-60 minutes** to index the blockchain. After that, it watches for opportunities!

> 💡 **Keep this terminal window open!** Closing it stops the bot.

---

## Step 7: Monitor and Claim Profits

### Watching the Logs

Keep an eye on your terminal. You'll see messages like:

```
[INFO] Checking positions...
[INFO] Found liquidatable position! Evaluating profitability...
[INFO] Executing liquidation: 0x...
[SUCCESS] Liquidation completed! Profit: $X.XX
```

### Claiming Your Profits

Profits accumulate in your Executor contract. To withdraw:

```bash
# Replace with your values
pnpm skim --chainId 8453 --token 0xTOKEN_ADDRESS --recipient 0xYOUR_WALLET_ADDRESS
```

**Common tokens on Base:**
- WETH: `0x4200000000000000000000000000000000000006`
- USDC: `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`

---

## Stopping and Restarting

### Stop the Bot

Press `Ctrl + C` in the terminal where the bot is running.

### Stop the Database

```bash
docker-compose down
```

### Restart Everything

```bash
# Start database
docker-compose up -d

# Start bot
pnpm liquidate
```

### Keep Bot Running When You Close Terminal (Advanced)

**Windows:** Use a tool like [NSSM](https://nssm.cc/) to run as a service.

**Mac/Linux:** Use `screen` or `pm2`:

```bash
# Install pm2
npm install -g pm2

# Start bot with pm2
pm2 start "pnpm liquidate" --name liquidation-bot

# View logs
pm2 logs liquidation-bot

# Stop
pm2 stop liquidation-bot

# Auto-start on reboot
pm2 startup
pm2 save
```

---

## Troubleshooting

### "Docker is not running"

Make sure Docker Desktop is open. Look for the whale icon in your system tray.

### "pnpm: command not found"

Run `npm install -g pnpm` again, then open a NEW terminal window.

### "Cannot connect to database"

```bash
# Restart the database
docker-compose down
docker-compose up -d
```

### "Invalid private key"

Make sure your private key:
- Starts with `0x`
- Has 66 characters total (0x + 64 hex characters)
- Has no spaces or extra characters

### Bot crashes immediately

Check your `.env` file for typos. Each line should be:
```
VARIABLE_NAME=value
```
No spaces around the `=` sign!

### Indexing stuck or very slow

- First run takes 10-60 minutes per chain
- Ethereum mainnet takes longest
- If stuck for hours, try resetting:

```bash
docker-compose down -v
docker-compose up -d
pnpm liquidate
```

### "Insufficient funds"

Add more ETH to your bot wallet for gas fees.

---

## FAQ

### Can I close my computer?

No—the bot stops when your computer sleeps or shuts down. For 24/7 operation, consider:
- A dedicated cheap computer (old laptop)
- A Raspberry Pi
- A cloud VPS (~$5/month)

### Which chain should I start with?

**Base** is recommended for beginners:
- Lower gas costs
- Active markets
- Good liquidity

### How much can I make?

Honestly? It varies wildly. Some bots make nothing, others make good profit. Factors:
- Market volatility
- Competition
- Gas prices
- Your chain choice

**Start small and learn!**

### Can I run multiple chains?

Yes! Add more entries to your `.env`:

```bash
# Base
RPC_URL_8453=...
EXECUTOR_ADDRESS_8453=...
LIQUIDATION_PRIVATE_KEY_8453=...

# Ethereum
RPC_URL_1=...
EXECUTOR_ADDRESS_1=...
LIQUIDATION_PRIVATE_KEY_1=...
```

### How do I update the bot?

```bash
# If you used git:
git pull
pnpm install

# If you downloaded ZIP:
# Download new ZIP, replace files (keep your .env!)
pnpm install
```

### Is this safe?

As safe as you make it:
- ✅ Use a dedicated wallet with limited funds
- ✅ Never share your private key
- ✅ Don't run on public computers
- ✅ Keep your `.env` file private

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────┐
│  MORPHO LIQUIDATION BOT - QUICK COMMANDS                │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  START DATABASE:     docker-compose up -d               │
│  START BOT:          pnpm liquidate                     │
│  STOP BOT:           Ctrl + C                           │
│  STOP DATABASE:      docker-compose down                │
│                                                         │
│  CLAIM PROFITS:                                         │
│  pnpm skim --chainId 8453 --token 0x... --recipient 0x..│
│                                                         │
│  RESET DATABASE:     docker-compose down -v             │
│                      docker-compose up -d               │
│                                                         │
│  VIEW LOGS (pm2):    pm2 logs liquidation-bot           │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Need Help?

- **Morpho Discord:** [discord.morpho.org](https://discord.morpho.org)
- **Morpho Docs:** [docs.morpho.org](https://docs.morpho.org)
- **GitHub Issues:** [Report bugs](https://github.com/morpho-org/morpho-blue-liquidation-bot/issues)

---

*Good luck! Start small, learn the process, and scale up when you're comfortable.* 🚀
