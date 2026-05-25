# Explanation: routes/user.js

## Purpose

User-focused read endpoints:

- incoming connection requests
- current connections
- user feed (people you haven’t interacted with yet)

## Export

- `userRouter` (Express router)

## Shared constants

- `USER_SAFE_DATA`: projection string used in `.select(...)` / `.populate(...)` to avoid returning sensitive fields.

## Route handlers (functions)

### `GET /user/requests/received`

- Requires `userAuth`.
- Finds `ConnectionRequest` where `toUserId = loggedInUser._id` and `status = interested`.
- Populates `fromUserId` with `USER_SAFE_DATA`.
- Returns `{ message, data }`.

### `GET /user/connections`

- Requires `userAuth`.
- Finds accepted connection requests where logged-in user is either side.
- Populates both `fromUserId` and `toUserId`.
- Maps each request to “the other user” and returns `{ data }`.

### `GET /feed`

- Requires `userAuth`.
- Supports pagination via `?page=` and `?limit=` (limit capped at 50).
- Finds all connection requests involving the user.
- Builds a set of userIds to hide from feed (already interacted with).
- Queries `User` excluding hidden ids and excluding yourself.
- Returns `{ data: users }`.

## Notes / gotchas

- Error handler in `/user/requests/received` uses `req.statusCode(...)` (typo); should be `res.status(...)`.
- In `forEach`, the variable name `req` shadows Express `req` (confusing but not fatal).
