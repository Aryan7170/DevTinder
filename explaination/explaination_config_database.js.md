# Explanation: config/database.js

## Purpose

Provides a single helper function to connect Mongoose to MongoDB using a connection string from environment variables.

## Export

- `connectDB` (async function)

## Functions

### `connectDB()`

- Reads `process.env.DB_CONNECTION_SECRET`.
- Connects to MongoDB via `mongoose.connect(...)`.
- Returns a promise (because it’s `async`).

## Notes / gotchas

- The current code logs `process.env.DB_CONNECTION_SECRET` to the console. That value is typically a secret connection string; logging it is risky in production.
- `mongoose.connect(...)` will throw if the connection string is missing/invalid.
