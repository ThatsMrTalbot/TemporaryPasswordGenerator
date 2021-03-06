﻿# Reasoning

There are a couple of ways to achieve a temporary password. The easiest way would be to use a database, storing generated GUIDs and expiry timestamps. However I thought it would be more interesting to algorithmically generate a password that is valid for a given period.

There exists a system like this called a Time-based One-time Password Algorithm (TOTP). This effectively slices time up into chunks, with each chunk having a unique code based of a common secret. This is used in two factor authentication.

For this system I wanted every generated password to be valid for x amount of time after generation. This differs from TOTP as a password must last x amount of time from generation, not just change every x seconds.

TOTP was a good place to start. We can calculate the offset between the current chunk and the generation time. By bundling this with the generated password we can establish an exact expiration time. This does however leave us with the issue that you could alter the the bundled expiration and expand the timeframe the password is valid. The solution to this is appending the offset to the secret used meaning a different offsets would require a different passwords.
