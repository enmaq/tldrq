# Changelog

User-facing changes only. The format follows [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

## [0.26.234] - 2026-10-14

- Tabs, carriage returns and other control characters no longer misalign single-line rows (search results and previews, input fields, command lists, canvas width). Your text and commands are stored unchanged.
- Text marked to truncate now ends in an ellipsis instead of wrapping.
- The Team KPI reports "input not submitted" when a message typed into a Claude worker is still sitting in its input box 10 seconds after sending. Nothing is pressed for you, and the message text is not shown.

## [0.26.233] - 2026-10-14

- Public repository community files: contributing guide, code of conduct, issue and pull-request templates. No app changes from 0.26.232.

## [0.26.232] - 2026-10-14

- Accents, flags and joined emoji now display correctly in channel and thread views, including when text wraps and the screen redraws.
- Spelling help learns your words. A `[+]` after each suggestion chip adds the word to your personal dictionary (`~/.tldrq/prose/allow.txt`, never in git). Common technical terms (tldrq, repo, config, params, sudo, backend, llms, ...) are no longer flagged. Optionally, `tldrq config set prose.auto_learn true` adds words you have sent in three messages.
- Tab strips no longer jump when a count changes digits: counts keep a stable width for the session (`( 6)` next to `(67)`), grow only past 99 and never shrink back.
- Shortcut hints are learned per session: once you use a shortcut or its matching control, its hint (including the Alt+U pulse) stays quiet for the rest of the shell session.
- Canvas typing is faster. A server echo that matches what you typed no longer resets the editor or re-renders the page, unchanged frames reuse the last render, and presence updates are sent at most every 500 ms while typing.
- Canvas typing saves are much cheaper. The revision history file is written on a pause, at least every 10 s, when a checkpoint changes and on shutdown, instead of on every keystroke batch. The text itself is still saved atomically on every batch, so a crash can lose only in-between versions, never the current text.
- New Teams automatically get one workspace Status canvas with an initial status table, linked from the master's setup context. Restarts and concurrent starts reuse it.
- Team KPI no longer reports a busy Codex screen (Working, Waiting for agents, or a warnings footer) as a blocking dialog. Real approval dialogs are still detected.
- The canvas recency log (`.tldrq/canvas/.recent.json`) is runtime state and is never committed.
- Local SkillPaq messages now store the new metadata names alongside the legacy names, and readers accept either spelling. Remote requests keep the legacy names, so retries stay compatible with older collectors. Team identities, database names and signed package bytes are unchanged.

## [0.26.231] - 2026-10-14

- Fixes letters that occasionally went blank or shifted after a screen update, mostly after emoji or other wide characters (it looked like typos, especially with bionic reading on).

- Word highlight is now plain black/white inverse, so matches stand out clearly.

- Canvases are stored slim: git now holds each canvas as a readable `<id>.md` (the current text) plus a small `<id>.json`, while revision history, receipts and checkpoints stay local in a git-excluded `.tldrq/canvas/.history/` folder. Old canvas files still read and are converted on their next edit with every revision kept; `tldrq canvas migrate --all` (dry run, then `--apply`) converts them all at once. A checkout pulled on another machine starts with the current text and fresh history.

- `canvas put` with a stale `--base` that overlaps newer edits is refused instead of storing conflict markers; a clean merge reports the merged rev range so you know the stored body differs from your file.

## [0.26.230] - 2026-10-13

- SkillPaq inspection uses the shared format-2 reader, showing model runtime metadata and all 24 funnel-v2 slots with the same canonical fingerprint as Compendium; inspection never executes a model.

## [0.26.229] - 2026-10-13

- Channels: rest the pointer on a word for 2 s, or leave an unsent draft for 2 s, and every visible copy of that word lights up in the channel, thread and canvas panes (including the word under the pointer); sending or moving away clears it. Hover needs a terminal that reports mouse motion.

- Canvases can't be wiped or written to the wrong place by accident: `canvas put` with an empty body is refused unless `--allow-empty` is passed, and a short canvas id that also names a canvas in another recently used workspace is refused with the full `tldrq://` URIs to choose from.

- Package format 2: Errata 2, the jointly signed model-kind projection with the funnel-v2 fingerprint vector checked by three independent implementations. Signing and execution stay off.

## [0.26.228] - 2026-10-13

- Renamed: playbooks are now **SkillPaqs**. `tldrq skillpaq ...` replaces `tldrq playbook ...` (the old verb keeps working, hidden, for one release), the MCP tools are `skillpaq_list` and `skillpaq_show` (the old names still answer), and new files are `.skillpaq` under `.tldrq/skillpaqs/`. Everything you already have keeps loading: `.playbook` files, `.tldrq/playbooks/`, signed packs and the wire and database names are unchanged.

## [0.26.227] - 2026-10-13

- Canvases: a `[ + new ]` button in the canvas tab strip (and `Alt+Shift+N`) asks for a title, creates the canvas and opens it ready to type; it also shows when you have no canvases yet. Esc cancels; a title is required.

- `tldrq playbook inspect FILE` shows a playbook's fingerprint and slots without installing or running anything.

- Team status no longer reports an agent as stuck behind an update dialog just because update text appears in its scrollback; only a real dialog at the bottom of the screen counts.

- Restart keeps each added agent's exact start command: its startup instructions are recorded together with the command, so a reopen no longer starts it with different instructions.

- Package format 2: agreed Errata 1 (signature preimage, capability order, minimum-runtime maps, nested forms refused) with conformance vectors, including an Ed25519 test vector checked by three independent implementations.

## [0.26.226] - 2026-10-13

- Encrypted playbook packs can now be used by agents: `tldrq playbook pack enable <name>` asks for your approval and issues a use grant (worker agents by default, masters only with `--master`); the pack's rules are then added to those agents' model requests in memory only. `pack disable` turns it off. Anthropic is supported first; other providers fail with a clear message.

- `tldrq playbook export` writes a licensed pack's data files to a folder you choose, with LICENSE and provenance, after a preview and your explicit approval. Only packs with licence terms can be exported; nothing is overwritten or executed.

- Every request to app.enmaq.com now carries the tldrq version, including login, licence and calls (0.26.225 sent it only on the update check and downloads).

## [0.26.225] - 2026-10-13

- The optional exit-country check (ipapi.co) is now off by default: no network call and no flag until `tldrq config geo on` or a workspace access region is set.

- tldrq now sends its version with each request to app.enmaq.com, and shows a startup banner and update notice if a minimum version is ever published. It never blocks a running session; no minimum is published yet.

- README: an FAQ ("Why isn't tldrq open source?") and a short list of what tldrq connects to, and when.

## [0.26.224] - 2026-10-13

- `~/.tldrq` stays tidy: each project's data now lives under `~/.tldrq/workspaces/<name>/`, so a project can no longer collide with tldrq's own folders. Existing project folders that hold only tldrq's own files move there once, in the background, leaving a symlink and a line in `workspaces/.migration.log`; a folder with anyone else's files in it stays where it is, and nothing is ever deleted.

## [0.26.223] - 2026-10-12

- The first Ctrl+\ search after a fresh start no longer fails with "Search timed out; retry" while the index is still building: the palette shows what is already indexed with "Indexing… · showing partial results" (or "Indexing N/M" when the total is known). Real index errors still show as errors.

## [0.26.222] - 2026-10-12

- Ctrl+\ search: the selected result is one full-width bar on a single aligned line (source | title, plus where when it differs), like Midnight Commander; it stays on the same item when results re-rank, and Up/Down/PgUp/PgDn/Home/End move it. "Searching…" no longer sticks after results arrive, the source tabs fit 80 columns, and Home/End work in tmux, the Linux console and xterm application mode.

- Long Team results arrive whole up to 4000 bytes; longer ones end with `[truncated]` and an intact link to the full message (the link used to be cut too).

- "Busy" means a member holds a live task or is mid-turn; recent traffic alone shows idle, and a restart with no live tasks shows everyone idle.

- Context cleanup never clears a master or a busy worker; "clear all" goes only to confirmed idle workers, and a cleared worker reloads the current Team playbook and keeps its task.

- Reopen keeps the Team as it was: removed members stay removed, added members come back with the same model and start settings, and `team members` shows the Codex model instead of `-`.

- With a thread and a canvas open, each maximize button maximizes its own pane.

- `-h`/`--help` on any command prints usage and never sends anything (`notifications send --help` used to send "--help").

## [0.26.221] - 2026-10-12

- Added: signed encrypted playbook pack sealing, device-bound activation and offline receipts; validation shows rule names and counts only, and encrypted packs stay inactive for agents.

- `~/.tldrq` stays bounded: once a day tldrq rotates `shell.log`/`collector.log` at 50 MB, caps the voice cache at 100 MB, keeps the last 5 archive/backup folders and drops idle proxy hosts and old iteration files; databases and foreign folders are never touched. `tldrq status` shows the folder size split into tldrq and other.

## [0.26.220] - 2026-10-12

- Search reuses a warm provider and reads the committed index during refresh; pending queries show “Searching…”, and Ctrl+D copies content-free diagnostics.

## [0.26.219] - 2026-10-12

- Canvas CLI and existing MCP tools accept full canvas URIs to target another workspace in the same project; bare IDs stay local.

## [0.26.218] - 2026-10-12

- Channels roster removes exited Team members and refreshes when their presence changes.

## [0.26.217] - 2026-10-12

- Added: free signed playbook packs from a configurable GitHub index, bounded in-memory validation, pinned installs and human-approved updates; authors can migrate to a new release for re-signing.

## [0.26.216] - 2026-10-12

- Added: offline `tldrq playbook check` for versioned pack manifests and bounded entry validation; no activation or network access.

## [0.26.215] - 2026-10-12

- Fixed: canvas tables with emoji status cells: ⚪ (and other emoji symbols) now count two columns, so rows stay aligned and the glyph is no longer overdrawn; long messages sent to agents are no longer cut in the middle of an emoji ("�…").

## [0.26.214] - 2026-10-12

- No user-facing changes (test isolation fix for a flaky learn test).

## [0.26.213] - 2026-10-12

- Added: Windows builds (amd64, arm64) are published with every release, capped like Linux and macOS.
- Added: short default CLI help and two-word run, memory, instructions, key, voice, install, probe and collector entry points; existing nested paths remain supported.

## [0.26.212] - 2026-10-12

- Added: `tldrq notifications send "text"` pushes a message to your enmaq app (web push; email only when no push target), after `tldrq notifications on`.
- Added: misspelled commands suggest a copyable command, preserving arguments, including one-level subcommands.

- Fixed: historical CLI command names forward to their canonical commands instead of refusing; `login`, `logout` and `whoami` are first-class commands.
- Added: `tldrq login` (the old `tldrq api login` still works). On a server without a browser it prints a code and a link: open it on any device, approve, and the CLI finishes by itself; no URL to paste back.

## [0.26.211] - 2026-10-11

- No user-facing changes (CI release of a test-only fix on top of 0.26.210).

## [0.26.210] - 2026-10-11

- Fixed: automatic channel replies require an assistant answer marker and never forward Claude status, compact footers or cropped tool captions; channel reads display human authors separately from the transport handle.

- Fixed: `tldrq api login` and the sheet's [Log in] on a machine with no browser (SSH, or Linux without a display) now print the sign-in URL and use the manual flow instead of waiting silently; with a browser the URL is also printed in case it does not open.

## [0.26.209] - 2026-10-11

- Fixed: a worker you add to a running Team can now `tldrq team run ready-ack` and use the iteration control channel; it joins with the Team Playbook of its wave.

- Changed: status canvases for every project use one numbered table, a green/yellow/white three-state legend, notes for details and blockers, and a UTC update time.

## [0.26.208] - 2026-10-11

- Fixed: forming a Team over the free agent cap now opens the same yellow Upgrade sheet as adding an agent, instead of a plain "Team not formed" notice.

## [0.26.207] - 2026-10-11

- Added: release builds enforce the free 3-agent / 1-Team cap; production signed licences lift it for subscribers and owners, with offline grace and safe Reopen.
- Fixed: `tldrq playbook use` now prints why it refused (agent session, no terminal) and names an unnamed signer by its short key; `playbook show` labels the pinned download hash and the canonical content hash.

## [0.26.206] - 2026-10-11

- Added: `tldrq playbook use URL|PATH` installs or updates a signed playbook after showing its rules diff; only a human approves (an agent's command cannot), and an installed file that was edited afterwards is not loaded.
- Added: Ed25519 playbook signing and explicit workspace key trust; invalid or untrusted signatures are refused, and `show` reports the canonical content hash.
- Added: tldrq excludes generated `.tldrq` runtime files through Git-local `info/exclude`; canvas pages and deletion history remain shared content, while canvas lock files, drafts, and live files stay out of status.

## [0.26.205] - 2026-10-11

- Fixed: An immediately exiting reopened member retains a visible failed-to-restart card and saved command; exit publication waits at most two seconds.
- Added: Canvas address-row maximize toggle, sharing the thread pane controls and Alt+E shortcut.
- Fixed: after a keyboard like, the status line keeps `LIKED #N` instead of being replaced by the generic `REACTED like` confirmation.
- Changed: a playbook is now ONE file, `name.playbook` (Lisp manifest + `(rule …)` entries); built-ins and workspace playbooks converted. Old playbook folders still load for one release with a deprecation note.

## [0.26.204] - 2026-10-11

### Fixed
- Ctrl+\ search no longer hangs on "Indexing…"; a slow search shows a retry.
- Canvas clicks and typing stay at the displayed cell; Enter inserts a newline, and typing in Threads or Canvas lists filters without reaching the composer.
- Space Space and the other keyboard likes never remove a like, say which message they reacted to (`LIKED #N`, or `ALREADY LIKED #N`), and follow the pane you are working in: with a thread open beside the chat, the main composer likes the newest channel message.
- Reopen repairs a withdrawn Codex model when a fresh account model list confirms a supported default; the member card says so.

### Added
- A channel left open while tldrq is updated now says so: a `⟳ new build` chip in the header and one line `tldrq updated to X, Reopen to apply`, instead of silently running the old build for days.

## [0.26.203] - 2026-10-11

### Changed
- A thread you open without choosing a message to reply to no longer shows a made-up `> #N` quote row above the composer (replies still go to the thread's first message). The `┄ ┄ ┄` rule above the tabs is gone from every thread and canvas pane next to the chat, not only the maximized ones.

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
