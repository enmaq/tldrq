# Changelog

User-facing changes only. The format follows [Keep a Changelog](https://keepachangelog.com/).

## [0.26.181] - 2026-10-10

### Added
- Install without an account: the one-line installer works anonymously and you sign in later with `tldrq api login`.
- When new unread messages arrive, the Alt+U hint lights up together with the unread indicator.
- The hint row shows "SPACE SPACE like" while the composer is empty.
- `tldrq channel reply --topic "3-6 words"` names a thread; the option now appears in the help.

## [0.26.180] - 2026-10-10

### Fixed
- Search now finds an exact phrase inside a thread reply, not just the thread's first message, and jumps straight to that reply.
- Double-space-to-like now likes the newest message from anyone else, including a reply from your own session's handle.
- The one-line installer now checks your system's glibc before downloading, and refuses with one plain line on an old Linux instead of a cryptic error after the download.

### Added
- Threads carry a short, updatable topic instead of always showing the first message's text.
- The canvas list is grouped by age (Last hour / Today / Yesterday / Last 7 days / Older), with a "delete all" per group.

## [0.26.178] - 2026-10-09

### Added
- Alt+C opens and focuses a canvas, focuses it again, then hides it — a full keyboard path, no mouse required.
- `TLDRQ_AUTO_ACK=0` turns off the automatic "Got it" acknowledgement.

## [0.26.177] and earlier

### Added
- Live canvas editing with a visible caret and source view, MDGL animations playable in a canvas, a hover bar under the mouse, `#N` message links, and anti-aliased banner text.

### Fixed
- Proxy memory and CPU use under load, restart/identity handling, and raw-byte leakage from canvases into the terminal.

See the GitHub Releases page for exact download links.
