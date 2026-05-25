# Explanation: routes/request.js

## Purpose

Implements “connection request” actions:

- send a request (interested/ignored)
- review a request (accept/reject)

## Export

- `requestRouter` (Express router)

## Route handlers (functions)

### `POST /request/send/:status/:toUserId`

- Requires `userAuth`.
- Reads:
  - `fromUserId` from `req.user._id`
  - `toUserId` from params
  - `status` from params
- Validates `status` in `["ignored", "interested"]`.
- Ensures `toUserId` exists (`User.findById`).
- Prevents duplicate requests in either direction using `$or`.
- Creates and saves a `ConnectionRequest`.
- Responds with a message and saved request data.

### `POST /request/review/:status/:requestId`

- Requires `userAuth`.
- Validates `status` in `["accepted", "rejected"]`.
- Loads a pending request where:
  - `_id = requestId`
  - `toUserId = loggedInUser._id`
  - `status = interested`
- Updates the request `status` and saves.
- Responds with `{ message, data }`.
