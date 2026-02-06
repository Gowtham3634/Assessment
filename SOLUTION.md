# Solution – Candidate Instructions

## 1. Setup & Run

This project consists of four parts that must be started in order:

1.  Local blockchain (Hardhat)
2.  Smart contract deployment
3.  Backend API
4.  Frontend dApp

------------------------------------------------------------------------

### Step 1 -- Start Local Hardhat Chain

From the `contracts` folder:

    npm install
    npx hardhat node

This starts a local Ethereum node at:

-   RPC: http://127.0.0.1:8545
-   Chain ID: 31337

Keep this terminal running.

------------------------------------------------------------------------

### Step 2 -- Deploy the Counter Contract

Open a new terminal in the `contracts` folder:

    npx hardhat run scripts/deploy.js --network localhost

You will see output like:

    Counter deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3

Copy this address.

------------------------------------------------------------------------

### Step 3 -- Configure and Run the Backend

Go to the `backend` folder:

    npm install
    cp .env.example .env

Edit `.env`:

    CONTRACT_ADDRESS=<PASTE_DEPLOYED_ADDRESS>
    CHAIN_ID=31337
    PORT=4000

Start the backend:

    npm start

Verify in browser:

-   http://localhost:4000/api/health
-   http://localhost:4000/api/config

------------------------------------------------------------------------

### Step 4 -- Configure and Run the Frontend

Go to the `frontend` folder:

    npm install
    cp .env.example .env

Edit `.env`:

    NEXT_PUBLIC_API_URL=http://localhost:4000

Start the app:

    npm run dev

Open:

    http://localhost:3000

------------------------------------------------------------------------

### Step 5 -- Connect MetaMask

1.  Add a custom network:
    -   RPC URL: http://127.0.0.1:8545
    -   Chain ID: 31337
    -   Network Name: Hardhat Local
2.  Import Account #0 private key from Hardhat output.
3.  Connect wallet to the dApp.
4.  Use Increment / Decrement buttons.

------------------------------------------------------------------------

## 2. Decisions

### Smart Contract

-   Solidity 0.8.20 used for built-in overflow/underflow protection.
-   Simple counter design with increment, decrement, and getCount.
-   Underflow protection handled by Solidity runtime checks.

### Backend

-   Built with Node.js + Express.
-   `/api/health` for service check.
-   `/api/config` supplies contract address and chain ID dynamically.
-   Uses environment variables to avoid hardcoding.

### Frontend

-   Built with Next.js + TypeScript.
-   wagmi used for wallet connection and network management.
-   Used a Minimal ABI for contract interaction.
-   `useAppConfig` fetches configuration dynamically from backend.
-   Separation of concerns:
    -   wagmi.ts → network/wallet
    -   contract.ts → ABI
    -   useAppConfig.ts → backend config

------------------------------------------------------------------------

## 3. Improvements

With more time:

-   combined tests for contract and API.
-   Improving the UI/UX and loading states.
-   Add on event listeners for real-time updates.
-   Persisting backend logs in database.
-   Get the full ABI from Hardhat artifacts.
