# Explanation: utils/constants.js

## Purpose

Holds shared constants used across the app.

## Export

- `{ membershipAmount }`

## Constants

### `membershipAmount`

- An object mapping membership tier to price:
  - `silver: 300`
  - `gold: 700`

## Usage

Used by payment code to compute order amount.
