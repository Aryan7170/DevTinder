# Explanation: middlewares/auth.js

## Purpose

Defines authentication middleware that:

- Reads a JWT from cookies
- Verifies it
- Loads the current user from MongoDB
- Attaches the user document to `req.user`

## Export

- `{ userAuth }`

## Functions

### `userAuth(req, res, next)`

1. Reads `token` from `req.cookies`.
2. If missing, returns `401` (`"Please Login!"`).
3. Verifies the token: `jwt.verify(token, process.env.JWT_SECRET)`.
4. Extracts `_id` from the decoded payload.
5. Fetches user: `User.findById(_id)`.
6. If not found, throws `"User not found"`.
7. Attaches `req.user = user` and calls `next()`.

## Notes / gotchas

- Requires `cookie-parser` middleware to run before this, otherwise `req.cookies` will be undefined.
- The JWT secret here is `process.env.JWT_SECRET`. Token creation must use the same secret, or verification will fail.
