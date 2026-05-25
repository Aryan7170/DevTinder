# Explanation: models/payment.js

## Purpose

Persists payment/order state related to premium membership purchases.

## Export

- `mongoose.model("Payment", paymentSchema)`

## Schema fields

- `userId`: ObjectId ref `User` (required)
- `paymentId`: string (optional)
- `orderId`: string (required)
- `status`: string (required)
- `amount`: number (required)
- `currency`: string (required)
- `receipt`: string (required)
- `notes`: embedded object with optional `firstName`, `lastName`, `membershipType`
- `timestamps: true` adds `createdAt`/`updatedAt`
