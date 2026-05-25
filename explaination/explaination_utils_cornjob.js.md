# Explanation: utils/cornjob.js

## Purpose

Registers a scheduled background job (cron) that emails users about pending connection requests from the previous day.

## Exports

- None. Requiring this module registers the cron schedule (side-effect module).

## Scheduled function

### `cron.schedule("0 8 * * *", async () => { ... })`

- Runs every day at 08:00.
- Computes “yesterday” time window using `date-fns`:
  - `yesterdayStart = startOfDay(yesterday)`
  - `yesterdayEnd = endOfDay(yesterday)`
- Queries pending requests created yesterday:
  - `status: "interested"`
  - `createdAt: { $gte: yesterdayStart, $lt: yesterdayEnd }`
- Populates `fromUserId` and `toUserId`.
- Builds a deduped email list from `toUserId.emailId`.
- Loops emails and calls `sendEmail.run(subject, body)`.

## Notes / gotchas

- This file name is `cornjob.js` (spelling). Any `require("./utils/cronjob")` won’t match unless renamed.
- `sendEmail.run` must exist; currently the `utils/sendEmail.js` file is empty.
