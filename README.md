# InnovaHub — local setup

## Requirements
- Node.js 18.18+ (Node.js 20 LTS recommended)
- npm
- A MongoDB database (MongoDB Atlas or local MongoDB)

## 1. Configure the backend
Open a terminal in `backend`:

```bash
npm install
```

Copy `.env.example` to `.env` and replace the placeholders with your real MongoDB connection string and a private JWT secret.

Windows PowerShell:
```powershell
Copy-Item .env.example .env
```

Configure your MongoDB Atlas database user/password and Network Access IP allow-list. Do not commit `.env` or share its contents.

Start the backend:
```bash
npm run dev
```

It should print `MongoDB connected successfully` and `Server running on http://localhost:5000`.
Check `http://localhost:5000/api/health`.

## 2. Start the frontend
Open a second terminal in `frontend`:

```bash
npm install
npm run dev
```

Open the local URL printed by Vite (normally `http://localhost:5173`).

## Registration notes
- Supported roles are `student`, `innovator`, `mentor`, and `organization` (plus `admin` internally).
- Email addresses are normalized to lowercase before registration/login.
- If an email already exists, use the login page for that email.

## Common errors
- `MongoDB connection failed`: check `backend/.env`, Atlas username/password, cluster hostname, and Atlas Network Access allow-list.
- `Network Error` / `ERR_CONNECTION_REFUSED`: backend is not running or is not listening on port 5000.
- `An account with this email already exists`: log in instead of registering again.
- `Registration failed`: check the backend terminal for the detailed validation/database error.


## Registration and login troubleshooting

- Each account must use a distinct email address. Registering an email already stored in MongoDB is intentionally rejected.
- The email is trimmed and converted to lowercase before registration and login.
- The login and registration pages now distinguish an HTTP/API response from a backend connection failure.
- The backend logs unexpected login errors in its terminal. Never share passwords, database connection strings, or JWT tokens.
- If a *different* email still reports a duplicate, check the backend terminal for `Duplicate registration field`. If it names a field other than `email`, share that field name and the HTTP response status.
- For a login failure, inspect the backend terminal and browser Developer Tools > Network > `login` > Response. Share only the status and message, never credentials or tokens.
