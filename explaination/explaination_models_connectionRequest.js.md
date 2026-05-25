# Explanation: models/connectionRequest.js

## Purpose

Stores a “connection request” (like friend request) between two users with a status lifecycle.

## Export

- `ConnectionRequest` Mongoose model (named `ConnectionRequestModel` in the file).

## Schema fields

- `fromUserId`: ObjectId ref to `User`, required.
- `toUserId`: ObjectId ref to `User`, required.
- `status`: required string enum: `ignored | interested | accepted | rejected`.
- `timestamps: true` adds `createdAt`/`updatedAt`.

## Indexes

- Compound index `{ fromUserId: 1, toUserId: 1 }` for faster lookups of request pairs.

## Hooks / functions

### `connectionRequestSchema.pre("save", function (next) { ... })`

- Runs before saving a connection request.
- Throws if `fromUserId` equals `toUserId` (prevents sending a request to yourself).
- Calls `next()` to continue saving.
