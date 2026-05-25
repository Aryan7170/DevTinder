# Explanation: src/app.js

## Purpose

Bootstraps the Express server, wires up middleware + routes, initializes Socket.IO (or a socket layer), connects to MongoDB, and starts listening on `process.env.PORT`.

## Key imports

- `express`: HTTP server framework.
- `../config/database`: `connectDB()` Mongo connection helper.
- `cookie-parser`: reads cookies into `req.cookies`.
- `cors`: enables cross-origin requests for the frontend.
- `http`: creates an HTTP server wrapper around Express (needed for sockets).
- `dotenv/config`: loads environment variables from `.env` into `process.env`.
- `./utils/cronjob`: expected to register scheduled jobs on startup.
- Routers: `./routes/auth`, `./routes/profile`, `./routes/request`, `./routes/user`, `./routes/payment`, `./routes/chat`.
- `./utils/socket`: expected to export `initializeSocket(server)`.

## Runtime flow (top to bottom)

1. Loads env vars: `require("dotenv").config()`.
2. Starts cron jobs by requiring the cron module (side-effect import).
3. Applies middleware:
   - `cors({ origin: "http://localhost:5173", credentials: true })`
   - `express.json()`
   - `cookieParser()`
4. Mounts routers at `/`.
5. Creates `server = http.createServer(app)` and calls `initializeSocket(server)`.
6. Calls `connectDB()`:
   - On success: `server.listen(process.env.PORT, ...)`
   - On failure: logs DB connection error.

## Exports

- No exports. This is the application entrypoint.

## Notes / gotchas

- The require path `./utils/cronjob` must match the actual file name.
- `initializeSocket` must be a function export; otherwise `initializeSocket(server)` will throw.
- The log message says port `7777...`, but it actually listens on `process.env.PORT`.
