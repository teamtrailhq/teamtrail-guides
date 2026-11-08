# Example: try the architect guide on this ticket

**Ticket (research):** How should we store per-user notification settings?

A good run reads the existing settings code (with real paths), compares a JSON column on the users table with a separate settings table, picks one with its trade-offs, describes the migration and rollback, and records the decision with `record_decision`.
