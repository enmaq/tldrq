# Security

The installer checks the SHA-256 of the downloaded binary against the value the
download server sends, and refuses to install on a mismatch. The built-in updater
verifies a signature on every update before it replaces the binary, so a tampered
update is refused rather than installed.

## Reporting a vulnerability

Email **contact@enmaq.com** with what you found and how to reproduce it, and put
"security" in the subject. We read every report. Please do not open a public
GitHub issue for a security problem until we've had a chance to respond; give us a
reasonable window to fix it first.

## Scope

This repository holds documentation, videos and the book; it carries no source.
tldrq binaries are downloaded by the installer from app.enmaq.com, the same
artifacts our own team runs.
