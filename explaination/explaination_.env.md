# Explanation: .env

## Purpose

Stores environment-specific configuration (secrets and runtime settings) loaded by `dotenv`.

## Typical contents (based on code usage)

- `PORT`
- `DB_CONNECTION_SECRET` (MongoDB connection string)
- `JWT_SECRET`
- `RAZORPAY_KEY_ID`
- `RAZORPAY_KEY_SECRET`
- `RAZORPAY_WEBHOOK_SECRET`

## Notes

- `.env` should not be committed publicly.
- Do not log secret env vars in production.
