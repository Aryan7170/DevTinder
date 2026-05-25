# Explanation: routes/profile.js

## Purpose

Provides profile endpoints for viewing and editing the currently authenticated user.

## Export

- `profileRouter` (Express router)

## Route handlers (functions)

### `GET /profile/view`

- Requires `userAuth` middleware.
- Returns `req.user` (the authenticated user document).

### `PATCH /profile/edit`

- Requires `userAuth` middleware.
- Calls `validateEditProfileData(req)`; throws if invalid.
- Copies all keys from `req.body` onto `loggedInUser`.
- Saves the updated user document.
- Responds with a confirmation message and updated user.

## Notes / gotchas

- `Object.keys(req.body)` allows editing any field provided by the client; typically you would whitelist editable fields.
