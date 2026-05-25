# Explanation: package.json

## Purpose

Node.js project manifest: metadata, scripts, and runtime dependencies.

## Key fields

- `name`: `devtinder`
- `type`: `commonjs` (uses `require(...)` / `module.exports`)

## Scripts

- `test`: placeholder script that exits with error.

## Dependencies

- `express`: web server framework.
- `mongoose`: MongoDB ODM.
- `cookie-parser`: cookie parsing middleware.

## Notes

- Additional dependencies (bcrypt, jsonwebtoken, cors, dotenv, node-cron, date-fns, razorpay, validator, etc.) are used in code but not listed here; the runtime will fail unless they’re installed and present in dependencies.
