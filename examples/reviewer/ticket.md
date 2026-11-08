# Example: try the reviewer guide on this review ticket

**Review ticket:** Review #12 "Rate-limit the login endpoint". Checks passed; the diff adds a middleware and a config value.

A good review reads the whole diff, checks the limit applies per account and per IP as the ticket asks, runs the tests, and answers FAIL with a finding like `src/auth/limit.ts:42: the counter never resets after a successful login` when something is wrong.
