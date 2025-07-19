

# 🚀 Blockchain-Based Online Voting System

## Project Overview

This project, developed as a final thesis, aims to address the challenges of traditional voting systems, such as lack of transparency, susceptibility to fraud, complexity, and high costs. By leveraging **blockchain technology**, this system provides a secure, transparent, and efficient online voting platform suitable for communities, organizations, and various competitions.

The system adopts a client-server architecture, with the Frontend developed using **React.js** and the Backend powered by **Node.js** in conjunction with **MongoDB**. All votes are meticulously recorded and secured on the **Ethereum Sepolia testnet** via **Smart Contracts written in Solidity**.

It supports two primary voting methods: direct participation on the website and voting via **QR codes**, enhancing user accessibility. For user authentication and authorization, the system integrates **Firebase Authentication** with **JWT (JSON Web Token)**.

## ✨ Key Features

*   **Secure User Management:**
    *   User registration, login, and logout.
    *   Personal profile updates (name, email, avatar).
    *   Password change functionality.
    *   Admin panel for user management (blocking/unblocking accounts).
*   **Flexible Poll Creation:**
    *   Create new voting polls with title, description, start/end dates.
    *   Option to upload cover images or use image links.
    *   Choose between public or private (password-protected) polls.
*   **Comprehensive Candidate Management:**
    *   Add candidates manually or import from an Excel file.
    *   View and update candidate information.
*   **Diverse Voting Methods:**
    *   Direct voting from the poll's detail page.
    *   Quick voting via unique QR codes generated for each candidate.
*   **Transparent Results & History:**
    *   View detailed poll information, including real-time vote counts and results.
    *   Retrieve personal voting history and updates via QR code scans.
*   **Admin Dashboard:**
    *   Overview of system statistics (total users, total polls).
    *   Manage all active polls in the system.
*   **Real-time Updates:** Integration with Socket.IO (implied by directory structure) for live vote count updates.

## 🛠 Technology Stack

This project is built on a robust set of modern technologies:

*   **Frontend:**
    *   **React.js (with TypeScript):** For building dynamic and interactive user interfaces.
    *   **Material-UI / BLK Design System React:** (Implied by extensive asset/component structure) For a clean and responsive design.
    *   **Axios:** For making HTTP requests to the backend API.
    *   **React Chart.js 2:** For visualizing voting results.
    *   **QR Code React:** For generating QR codes.
    *   **Socket.io-client:** For real-time communication.
*   **Backend:**
    *   **Node.js (with TypeScript):** Runtime environment.
    *   **Express.js:** Web application framework for building RESTful APIs.
    *   **MongoDB & Mongoose:** NoSQL database for flexible data storage and ODM for schema definition.
    *   **JWT (JSON Web Token):** For secure user authentication and authorization.
    *   **Bcrypt.js:** For password hashing.
    *   **Cookie-parser:** For handling HTTP cookies.
    *   **Socket.io:** For real-time communication with the frontend.
*   **Blockchain & Smart Contracts:**
    *   **Ethereum Sepolia Testnet:** The blockchain network where Smart Contracts are deployed.
    *   **Solidity:** Programming language for Smart Contracts.
    *   **Hardhat:** Ethereum development environment for compiling, deploying, and testing contracts.
    *   **Ethers.js:** JavaScript library for interacting with Ethereum blockchain.
    *   **Alchemy SDK:** Enhanced JavaScript SDK for robust blockchain interaction and data fetching.
*   **Authentication Service:**
    *   **Firebase Authentication:** For robust and scalable user authentication (email/password).
    *   **Firebase Storage:** For storing user avatars and poll cover images.

## 🏗 Architecture

The system follows a standard **Client-Server architecture** with deep blockchain integration:

1.  **Client (Frontend):**
    *   Developed with React.js, responsible for rendering the UI, capturing user input, and displaying real-time data.
    *   Communicates with the Backend API via HTTP requests.
    *   Directly interacts with MetaMask for specific blockchain operations (if user's own wallet is used, though the thesis describes backend-signed transactions).
2.  **Server (Backend):**
    *   Built with Node.js and Express.js, acts as the central hub.
    *   Manages user data, poll information, and candidates in **MongoDB**.
    *   **Crucially, it acts as the bridge to the blockchain.** It sends requests to the deployed Smart Contract on Sepolia to record votes and fetch blockchain-verified results using **Ethers.js** and **Alchemy SDK**.
    *   Handles user authentication and authorization via JWT after Firebase authentication.
    *   Manages real-time updates using Socket.IO.
3.  **Database (MongoDB):**
    *   Stores all off-chain data: user profiles, voting poll details (title, description, dates), candidate information (name, description, image URL), and participation records for private polls.
    *   This provides flexibility and scalability for application data.
4.  **Blockchain (Ethereum Sepolia Testnet):**
    *   **Smart Contracts (Solidity):** Deployed on Sepolia, these contracts are responsible for immutably recording votes and vote updates. Each vote or update is a transaction on the blockchain, ensuring transparency and tamper-proof records.
    *   A single MetaMask wallet (managed by the backend) is used to sign transactions to the Smart Contract, simplifying the user experience as users don't need their own ETH for gas fees for basic voting actions.

## 📂 Project Structure

```
Voting-system/
├── backend/                  # Node.js/Express.js server
│   ├── src/
│   │   ├── controllers/      # Business logic handlers
│   │   ├── db/               # MongoDB connection
│   │   ├── middleware/       # Auth/Admin protection
│   │   ├── models/           # Mongoose schemas for MongoDB
│   │   ├── routes/           # API endpoints
│   │   ├── smartcontract/    # Logic for interacting with deployed Smart Contracts
│   │   ├── socket/           # Socket.IO setup for real-time updates
│   │   └── utils/            # Utility functions (e.g., JWT generation)
│   │   └── server.ts         # Main backend application file
│   ├── .env                  # Backend environment variables
│   ├── package.json          # Backend dependencies
│   └── tsconfig.json         # TypeScript configuration
├── frontend/                 # React.js UI application
│   ├── public/               # Static assets
│   ├── src/
│   │   ├── api-url.ts        # API endpoint configuration
│   │   ├── App.tsx           # Main React component
│   │   ├── firebase.ts       # Firebase configuration
│   │   ├── contract/         # Smart Contract ABI (TransactionManager.json)
│   │   ├── assets/           # CSS, fonts, SCSS (BLK Design System React)
│   │   ├── components/       # Reusable UI components (admin, polls, charts, etc.)
│   │   ├── context/          # React Context API for global state
│   │   ├── examples/         # Complex UI component examples
│   │   ├── layouts/          # Page layouts (authentication, dashboard, etc.)
│   │   ├── redux/            # Redux store, actions, reducers (if Redux is used)
│   │   ├── variables/        # Global variables (e.g., chart data configs)
│   │   └── views/            # Main application screens/pages
│   ├── .env                  # Frontend environment variables
│   ├── package.json          # Frontend dependencies
│   ├── tsconfig.json         # TypeScript configuration
│   └── webpack.config.js     # Webpack configuration
├── smart-contracts/          # Solidity Smart Contracts and Hardhat project
│   ├── contracts/            # Solidity source files (e.g., VotingContract.sol)
│   ├── scripts/              # Deployment scripts (TypeScript)
│   ├── test/                 # Smart Contract test files (TypeScript)
│   ├── hardhat.config.ts     # Hardhat configuration for networks, compiler
│   ├── .env                  # Smart contract environment variables (RPC URL, Private Key)
│   ├── package.json          # Hardhat dependencies
│   └── tsconfig.json         # TypeScript configuration
└── .gitignore                # Global Git ignore file
```

## 🚀 Installation & Setup

To get this project up and running locally, follow these general steps:

### Prerequisites

*   **Node.js & npm/yarn:** Ensure you have Node.js (LTS version) and npm/yarn installed.
*   **Git:** For cloning the repository.
*   **MongoDB:** Install MongoDB Community Server locally or use a cloud service like MongoDB Atlas.
*   **MetaMask:** Install the browser extension and set up a wallet.
*   **Alchemy/Infura Account:** Sign up for a free account to get Sepolia RPC URL.
*   **Firebase Project:** Create a project in Firebase Console for Authentication and Storage.

### Steps

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/Voting-system.git # Replace with your actual repo
    cd Voting-system
    ```

2.  **Setup Smart Contracts:**
    ```bash
    cd smart-contracts
    npm install # or yarn
    npx hardhat compile
    # Create a .env file (copy .env.example) and fill in SEPOLIA_RPC_URL, PRIVATE_KEY, ETHERSCAN_API_KEY
    # Deploy your contract to Sepolia
    npx hardhat run scripts/deploy.ts --network sepolia
    # IMPORTANT: Note down the deployed contract address and copy the ABI from artifacts/contracts/VotingContract.sol/VotingContract.json
    cd ..
    ```

3.  **Setup Backend:**
    ```bash
    cd backend
    npm install # or yarn
    # Create a .env file (copy .env.example) and fill in MONGO_URI, JWT_SECRET, ETHEREUM_RPC_URL (from Alchemy/Infura), PRIVATE_KEY (for backend-signed transactions), CONTRACT_ADDRESS (from step 2)
    # Configure package.json scripts and tsconfig.json as per detailed instructions.
    cd ..
    ```

4.  **Setup Frontend:**
    ```bash
    cd frontend
    npm install # or yarn
    # Create a .env file (copy .env.env.example) and fill in REACT_APP_BACKEND_URL, REACT_APP_CONTRACT_ADDRESS (from step 2), and Firebase config variables.
    # Copy the Smart Contract ABI (Voting-system/smart-contracts/artifacts/contracts/VotingContract.sol/VotingContract.json) to frontend/src/contract/TransactionManager.json
    # Ensure your src/ folder structure matches the project's design (e.g., if using a UI template, copy its assets/components).
    cd ..
    ```

### Running the Application

1.  **Start MongoDB:** Ensure your MongoDB server is running.
2.  **Start Backend:**
    ```bash
    cd backend
    npm run dev # or yarn dev
    ```
3.  **Start Frontend:**
    ```bash
    cd frontend
    npm start # or yarn start
    ```

The frontend application should open in your browser at `http://localhost:3000`.

## 💡 Usage

*   **Register** a new user account via the `Sign Up` page.
*   **Login** to access the main features.
*   **Create a new poll** from the dashboard, add details, image, and set privacy.
*   **Add candidates** to your newly created poll, either manually or via Excel import.
*   **Participate in public polls** or join private polls using their ID and password.
*   **Vote** for your favorite candidates directly or by scanning the generated **QR codes**.
*   **Admins** can log in to manage users and polls from the dedicated dashboard.

## Roadmap & Future Enhancements

*   **Mainnet Deployment:** Transition the Smart Contracts and application to the Ethereum Mainnet for real-world usage.
*   **Performance Optimization:** Implement further optimizations to handle high transaction loads and improve response times on the blockchain.
*   **Monetization & Scalability:** Integrate payment features for large-scale, paid voting events to create revenue opportunities.
*   **Advanced Features:** Explore adding more complex voting mechanisms, decentralized identity solutions, or enhanced analytics.
