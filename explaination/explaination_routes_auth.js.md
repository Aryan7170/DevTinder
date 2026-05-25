# Explanation: routes/auth.js

## Purpose

Defines authentication routes: signup, login, logout.

## Export

- `authRouter` (Express router)

## Route handlers (functions)

### `POST /signup`

- Calls `validateSignUpData(req)` to validate request body.
- Extracts `{ firstName, lastName, emailId, password }`.
- Hashes password: `bcrypt.hash(password, 10)`.
- Creates `new User({ ... , password: passwordHash })` and saves.
- Creates JWT via `savedUser.getJWT()`.
- Sets `token` cookie (expires in ~8 hours).
- Responds with `{ message, data: savedUser }`.

### `POST /login`

- Reads `{ emailId, password }`.
- Looks up user: `User.findOne({ emailId })`.
- Validates password via `user.validatePassword(password)`.
- If valid:
  - Creates token via `user.getJWT()`
  - Sets cookie and responds with the user document
- Else throws `"Invalid credentials"`.

### `POST /logout`

- Clears the cookie by setting `token` to `null` and expiring immediately.
- Responds with a success message.

## Notes / gotchas

- This router depends on helper functions in `utils` (sign-up validation).
- Consider returning a “safe” user object (without password hash) on login.
