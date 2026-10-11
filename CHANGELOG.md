# Changelog

User-facing changes only. The format follows [Keep a Changelog](https://keepachangelog.com/).

## [0.26.199] - 2026-10-11

### Changed
- The channel **Iterate** and **Status** buttons now come from playbooks (`enmaq/quick-iterate`, `enmaq/quick-status`), so a team can rewrite them. Status always reports onto the workspace's one canvas whose topic is `Status`, rewritten in place, never a new canvas each time.

## [0.26.198] - 2026-10-11

### Changed
- Threads and canvases show `#N · topic · address` on one row; the topic updates live and renames in place on click. Tabs show the first few plus `+N`.

## [0.26.197] - 2026-10-11

### Added
- fzf-style `@` path completion in the composer: typos and deep paths match, fast on million-file repos, no git needed.

## [0.26.193] - 2026-10-11

### Changed
- `tldrq playbook list` and `show` print readable tables; `!` commands get a dark-blue composer and a taller output tray; canvas and urgency cues go to the leading master only.

## [0.26.192] - 2026-10-11

### Added
- **Playbooks:** a team's way of working as packages in `.tldrq/playbooks/<org>/<name>/` (a Lisp manifest plus plain-prose rules). tldrq ships its own practices as built-in playbooks; a team adds, overrides or disables them. `tldrq playbook list | show | enable | disable | new | preview`.

## [0.26.191] - 2026-10-11

### Changed
- Canvas editing is calm and predictable: a click in the canvas never starts editing (it follows links and sorts tables); press `[edit]`, double-click or `e` to edit, Esc to leave. Your place stays put when switching, and the whole block under the caret shows as source, so nothing jumps while you type.

## [0.26.190] - 2026-10-11

### Fixed
- Under heavy load, the proxy could hand an agent a cut-off model response with no error. It never truncates now.

## [0.26.189] - 2026-10-10

### Added
- A filter bar at the top of the Threads and Canvas lists: type to narrow by topic, number or author.
- Canvases have an updatable topic, like threads (`tldrq canvas topic N "words"`).

### Fixed
- Search no longer gets stuck on "Indexing…"; it always shows what it has and why.

## [0.26.188] - 2026-10-10

### Added
- Canvas tables sort like channel tables: click a header.

### Fixed
- Typing after moving up or down onto a shorter line lands where the caret is.
- Coloured canvas text renders as colour again.

## [0.26.187] - 2026-10-10

### Fixed
- Text tldrq sends to agents no longer shows up in the roster tiles; hint rows never cut a word in half.

## [0.26.186] - 2026-10-10

### Changed
- `tldrq api logout` also revokes the device's key on the server.

## [0.26.185] - 2026-10-10

### Fixed
- In a canvas, text typed into empty space stays exactly where you typed it.

## [0.26.183] - 2026-10-10

### Added
- A clear upgrade dialog when a plan limit is reached, and a guard that keeps diagrams and big tables out of chat (they belong on a canvas).

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

Install or update with the one-line installer in the [README](README.md#install); `tldrq update` keeps you current.
