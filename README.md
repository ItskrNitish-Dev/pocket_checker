# Pocket Checker

Pocket Checker is a personal finance tracker for recording and reviewing transactions. Create an account, log in, add transactions, and view your history and spending totals by category.

## Features

- Sign up, log in, and log out with session-based authentication.
- Record transactions with a description, amount, payment type, category, date, and optional location.
- Browse transaction history and edit or delete transactions.
- View totals for savings, expenses, and investments in a category chart.
- Use a responsive interface built with React and Tailwind CSS.

## Tech stack

- **Frontend:** React, Vite, React Router, Apollo Client, GraphQL, Tailwind CSS, Chart.js
- **Backend:** Node.js, Express, Apollo Server, GraphQL, Passport
- **Database:** MongoDB with Mongoose
- **Sessions:** `express-session` stored in MongoDB

## Requirements

- Node.js 18 or newer and npm
- A MongoDB instance, local or hosted

## Local development

The backend and frontend run in separate processes during development. Run the following from the repository root.

1. Install the root and frontend dependencies:

   ```powershell
   npm install
   npm install --prefix frontend
   ```

2. Create a root `.env` file with your MongoDB connection string and a strong session secret:

   ```dotenv
   MONGO_URI=mongodb://127.0.0.1:27017/pocket_checker
   SESSION_SECRET=replace-this-with-a-long-random-secret
   CLIENT_URL=http://localhost:3000
   PORT=5000
   ```

   `CLIENT_URL` must match the browser origin used by the frontend. The Vite development server is configured for port `3000`.

3. Create `frontend/.env` to make the development client use the local GraphQL server:

   ```dotenv
   VITE_NODE_ENV=development
   ```

4. Start the backend in one terminal:

   ```powershell
   npm run dev
   ```

5. Start the frontend in another terminal:

   ```powershell
   npm run dev --prefix frontend
   ```

   Open the Vite URL shown in the terminal (by default, `http://localhost:3000`). The GraphQL endpoint is `http://localhost:5000/graphql`.

Keep both `.env` files private and do not commit real credentials or secrets.

## Available scripts

Run root-level scripts from the repository root:

| Command | Description |
| --- | --- |
| `npm run dev` | Start the backend with Nodemon and `NODE_ENV=development`. |
| `npm start` | Start the backend with Node.js. |
| `npm run build` | Build the frontend for production into `frontend/dist`. |

Run frontend scripts with `npm run <script> --prefix frontend`:

| Command | Description |
| --- | --- |
| `npm run dev --prefix frontend` | Start the Vite development server. |
| `npm run build --prefix frontend` | Build the frontend. |
| `npm run preview --prefix frontend` | Preview the production frontend build locally. |
| `npm run lint --prefix frontend` | Run ESLint on the frontend. |

## GraphQL API

The backend exposes a GraphQL API at `/graphql`.

### Account operations

| Operation | Purpose |
| --- | --- |
| `authUser` | Return the currently authenticated user. |
| `user(userId)` | Look up a user by ID. |
| `signUp(input)` | Create an account using a name, username, password, and gender. |
| `login(input)` | Authenticate with a username and password. |
| `logout` | End the current session. |

### Transaction operations

| Operation | Purpose |
| --- | --- |
| `transactions` | List transactions for the current user. |
| `transaction(transactionId)` | Look up a transaction by ID. |
| `categoryStatistics` | Return the current user's totals grouped by category. |
| `createTransaction(input)` | Add a transaction. |
| `updateTransaction(input)` | Update a transaction. |
| `deleteTransaction(transactionId)` | Delete a transaction. |

Transactions use these categories: `saving`, `expense`, and `investment`. Payment types are `cash` and `card`.

## Configuration

### Backend

| Variable | Required | Description |
| --- | --- | --- |
| `MONGO_URI` | Yes | MongoDB connection string. Used for application data and session storage. |
| `SESSION_SECRET` | Yes | Secret used to sign the session cookie. Use a long, unique random value. |
| `CLIENT_URL` | Yes | Allowed frontend origin for credentialed GraphQL requests, such as `http://localhost:3000`. |
| `PORT` | No | Backend port; defaults to `5000`. |
| `NODE_ENV` | No | Set to `development` for local work. The root `dev` script sets this automatically. |

### Frontend

| Variable | Description |
| --- | --- |
| `VITE_NODE_ENV` | Set to `development` to send GraphQL requests to `http://localhost:5000/graphql`. Other values use the same-origin path `/graphql`. |

## Deployment

The root `npm run build` command builds the frontend. The backend serves the generated `frontend/dist` files when running as a regular Node process. The repository also includes a Vercel configuration for deploying the GraphQL backend and static frontend together.

For deployment, configure `MONGO_URI`, `SESSION_SECRET`, and `CLIENT_URL` in the hosting provider's environment settings. Ensure the MongoDB deployment accepts connections from the application host. The production frontend expects the GraphQL API at the same origin under `/graphql`.

## Project structure

```text
backend/
  db/           MongoDB connection
  models/       Mongoose user and transaction models
  passport/     Passport local authentication strategy
  resolvers/    GraphQL resolver implementations
  typeDefs/     GraphQL schema definitions
  index.js      Express and Apollo Server entry point
frontend/
  src/
    components/ Reusable UI and transaction components
    graphql/    Apollo queries and mutations
    pages/      Login, signup, dashboard, and transaction pages
    utils/      Shared frontend utilities
  vite.config.js
package.json    Backend and root-level scripts
vercel.json     Vercel deployment configuration
```

## Images
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/32d2cc83-2c33-4764-9126-d64722bf49bc" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4af37f38-7f36-488a-96ea-38bf55174b19" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5869e33e-283e-4769-9624-d6b808ae9e2f" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b61ca6fc-5740-420a-926f-87c61c2a3e69" />



