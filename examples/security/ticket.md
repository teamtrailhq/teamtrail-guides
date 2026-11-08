# Example: try the security guide on this ticket

**Ticket (execute):** Add an endpoint that exports a team's notes as a ZIP file.

A good run checks that only members of that team can call it, that file names inside the ZIP can't escape the archive (no `../`), that large exports can't exhaust memory, and that the export link expires. It writes down each risk and what it did about it.
