# Explanation: models/user.js

## Purpose

Defines the `User` Mongoose schema/model and adds helper methods for JWT creation and password verification.

## Export

- `mongoose.model("User", userSchema)`

## Schema fields (high level)

- `firstName` (required, 4–50 chars)
- `lastName` (optional)
- `emailId` (required, unique, trimmed, lowercased, validated as email)
- `password` (required, validated as “strong password”)
- `age` (min 18)
- `gender` (enum: `male|female|other`)
- `isPremium` (default false)
- `membershipType` (optional)
- `photoUrl` (default URL, validated as URL)
- `about` (default string)
- `skills` (array of strings)
- `timestamps: true` adds `createdAt`/`updatedAt`

## Validation functions

- `emailId.validate(value)`: throws if `!validator.isEmail(value)`.
- `password.validate(value)`: throws if `!validator.isStrongPassword(value)`.
- `photoUrl.validate(value)`: throws if `!validator.isURL(value)`.

## Instance methods

### `user.getJWT()`

- Creates a JWT containing `{ _id: user._id }`.
- Sets expiration to 7 days.
- Returns the token string.

### `user.validatePassword(passwordInputByUser)`

- Compares plaintext input with the stored hash (`user.password`) using `bcrypt.compare`.
- Returns `true/false`.

## Notes / gotchas

- Token signing secret must match the secret used in auth verification middleware.
- Password validation runs on the stored value; if you store a bcrypt hash, this validator is checking the hash, not the raw password.
