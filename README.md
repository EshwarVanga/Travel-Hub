# TravelHub (Vite + React + TypeScript)

 A demo travel booking frontend with a lightweight Express/Mongo backend. Includes OTP demo flows, local-storage fallbacks for offline demos, and example payment UI.

 ---

 ## Quickstart (development)

 Prerequisites:
- Node.js (LTS recommended)
- npm
- MongoDB running locally or a connection string

 1. Install dependencies (root and backend):

 ```powershell
 # from project root
 npm install
 # start backend in a separate terminal
 cd backend
 npm install
 npm run dev
 ```

 2. Start frontend dev server (project root):

 ```powershell
 npm run dev
 ```

 Frontend runs via Vite (default port 5173; Vite will pick another port if occupied).

 3. Open the app in your browser (Vite prints the exact URL, e.g. http://localhost:5173/)

 ---

 ## Build / Preview (production)

 ```powershell
 npm run build
 npm run preview
 ```

 If you want the backend to serve the built frontend in production, copy the `dist` folder into `backend/` or adjust the backend static path (server already attempts to serve from `../dist`).

 ---

 ## Environment variables

 Create a `.env` in `backend/` to set values used by the server. Example variables used by the project:

 ```env
 MONGO_URI=mongodb://127.0.0.1:27017/travelhub
 PORT=5000
 FRONTEND_URL=http://localhost:5173
 JWT_ACCESS_SECRET=your_access_secret
 JWT_REFRESH_SECRET=your_refresh_secret
 JWT_EXPIRES_IN=15m
 REFRESH_EXPIRES_IN=30d
 ```

 For the frontend, Vite env vars use the `VITE_` prefix if needed (e.g. `VITE_API_URL` to change API base URL).

 ---

 ## Notable implementation details

- The login/signup UI uses a demo OTP flow (OTP is shown in an alert for easy testing). In production you would replace this with a proper SMS/email 2FA provider.
- Local fallback: the frontend includes a `src/lib/storage.ts` helper that stores demo users/bookings/reviews in `localStorage` for offline/demo purposes.
- Backend routes are located in `backend/routes/` and use MongoDB for persistence. User signup endpoint: `POST /api/auth/signup` and login: `POST /api/auth/login`.
- We added password visibility toggles to the login/signup password field and CVV field in the payment modal.

 ---

 ## TypeScript

 Run a typecheck locally:

 ```powershell
 npm run typecheck
 ```

 The repo allows importing some existing `.js` files (see `tsconfig.app.json` `allowJs`), which reduces friction during migration.

 ---

 ## Troubleshooting

- Port conflicts: Vite will try the next available port if `5173` is occupied — check the console for the URL.
- If signup seems to succeed locally but login fails, ensure the backend is running and that signup POSTs to `/api/auth/signup` (the frontend was updated to use `/signup`).
- If the backend cannot connect to MongoDB, check `MONGO_URI` and that MongoDB is running.

 ---

 ## Development notes

- To add compatibility, you can create a small dev-only endpoint on the backend to list users for debugging.
- To secure CVV/password visibility toggles in production, conditionally enable them only for development builds.

 ---

 If you want, I can:
- add a `dev` endpoint to list users (development only),
- add a CONTRIBUTING.md or tests for the auth flow, or
- lock the password/CVV toggles to non-production builds.

 License: MIT (project demo)