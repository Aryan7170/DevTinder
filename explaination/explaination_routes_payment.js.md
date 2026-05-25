# Explanation: routes/payment.js

## Purpose

Creates Razorpay orders for memberships and processes Razorpay webhooks to mark users as premium.

## Export

- `paymentRouter` (Express router)

## Dependencies

- `razorpayInstance`: configured Razorpay SDK client.
- `Payment`: payment model.
- `User`: user model.
- `membershipAmount`: maps membership type to price.
- `validateWebhookSignature`: verifies webhook signatures.

## Route handlers (functions)

### `POST /payment/create`

- Requires `userAuth`.
- Reads `membershipType` from body.
- Creates Razorpay order with amount `membershipAmount[membershipType] * 100`.
- Saves an internal `Payment` document using returned order details.
- Responds with payment JSON + `keyId` for frontend checkout.

### `POST /payment/webhook`

- Reads webhook signature header `X-Razorpay-Signature`.
- Verifies signature using `process.env.RAZORPAY_WEBHOOK_SECRET`.
- If invalid: responds `400`.
- If valid:
  - Extracts `paymentDetails` from payload.
  - Finds internal `Payment` by `orderId` and updates `status`.
  - Finds `User` by `payment.userId`, sets `isPremium = true`, sets `membershipType`.
  - Saves both documents.
- Responds `200`.

### `GET /premium/verify`

- Requires `userAuth`.
- Returns the current user JSON (premium or not).

## Notes / gotchas

- Webhook handler assumes the payload shape `req.body.payload.payment.entity`.
- Be sure Express is configured to parse webhook body exactly as Razorpay expects (signature verification is sensitive to body formatting).
