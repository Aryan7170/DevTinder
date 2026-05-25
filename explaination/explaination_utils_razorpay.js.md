# Explanation: utils/razorpay.js

## Purpose

Creates and exports a configured Razorpay client instance.

## Export

- Razorpay instance (`instance`)

## Behavior

- Instantiates `new Razorpay({ key_id, key_secret })` using:
  - `process.env.RAZORPAY_KEY_ID`
  - `process.env.RAZORPAY_KEY_SECRET`

## Notes

- Requires environment variables to be present at runtime.
