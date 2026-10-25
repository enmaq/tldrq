# Changelog

User-facing changes only. The format follows [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

## [0.26.362] - 2026-10-25

- `tldrq shell --profile sample`: Run is no longer blocked on small trial machines (capacity is a hint, as in the normal picker), and Advanced opens the normal picker instead of ending the session.

## [0.26.361] - 2026-10-25

- A fresh Tandem team answers the first human ask right away: no work round is opened until there is real work, and an agent refused by team-run calls is told to reply in the channel instead of retrying.

## [0.26.360] - 2026-10-25

- Bottom bar: the same buttons in the same order at every UI level: `[ W Workers ] [ C Channels ] [ B Browser ]` on the left; `[⌕ Search ] [Prx •] [ UI-Level N ] [ help ]`, the clock with idle time in brackets (`20:36 Oct25 (1m)`) and power on the right. Below 160 columns both sides go compact, 160-199 keeps the right side in words, 200+ shows words everywhere. UI-Level never moves as idle or traffic changes; clicks hit the same cells in the terminal and the browser view.
- "X is thinking…" above the composer now scrolls what each busy agent is doing, side by side (blue), using the same running-text component as the channel header (yellow), which now shows at every UI level.
- SkillPaqs are protected: built-in and installed packs are stored compressed in the binary; `skillpaq show`/`preview`, MCP, the catalog and the Skills pane show a plain summary (what it does, who it applies to, whether it's active) and the rule graph only with `--graph`, never rule text. Claude gets protected rules only through the local proxy; Codex and Muse keep free built-in rules in plain text; paid packs say "not available here; works in Claude" instead of falling back.
- The proxy no longer skips licensed rules when a message contains the public marker text, and refuses WebSocket requests in a licensed session with a clear reason.
- `tldrq shell --profile sample` starts a trial sample with one "Run sample" confirmation (Advanced opens the usual picker); a second Run resumes.
- Unanswered-message nudges and badges: an answer by any Team master clears the message, and a reply to the latest message of a burst answers the whole burst.
- Any Team master can react to a human message (reactions were refused for co-masters).
- `tldrq channel rules CH --json` only reads; writing needs `--set TEXT` (it used to save "--json" as the rules).
- MCP `channel_reply` can open a new thread (`new_thread`, `topic`); `channel reply --help` lists `--new-thread` and `--topic`, and the thread-topic rule tells agents to check help before saying something is unsupported.

## [0.26.359] - 2026-10-25

- A model's short rate limit (or "provider down") no longer sends a push notification; it stays on the member card. Pushes about model health are sent only when credentials are rejected and you need to act.

## [0.26.358] - 2026-10-25

- A shell started before you log in now joins the web sessions list once you log in (the relay retries every 30 seconds instead of switching off for good), and the shell log says once why the relay is off (not logged in, certificate trust failure, ...), never with tokens or URLs.
- Browser view (TUI2WUI): the first page fills the whole window without switching the scale (it re-fits when the view attaches, after fonts load and on every resize), and the text cursor is black or white against its cell in both themes.
- Bottom bar: the team button reads [ W Workers ] and the browser button [ B Browser ] next to [ C Channels ] on wide terminals (compact [W] [C] [B] below about 160 columns).
- The humans-rituals-and-psychology SkillPaq is now mostly Lisp: a `shapes` part maps each measured signal (repeat, burst, gap, long absence, stress) to a one-line reply shape that the wake line carries, and a `meaning` part lists twelve one-line answers for what the agent reads in a message (thanks, stepping away, a light moment...). The pack text is 25% shorter; the basis of each entry lives in scripts/humans-study/README.md.
- Human signals no longer match fixed word lists ("tea", "чай", "eta"…): the wake tag carries only language-free measurements (bursts, gaps, repeated asks, ?! and capitals), and the agent reads what a message means in any language. A first message after silence is skipped when the person's last message says they stepped away.
- The SkillPaq pane uses the same header as the Threads and Canvas panes: "All SkillPaqs (20 · 2 proposed)", open packs as tabs and a close button, without the extra [ Processes ] [ Threads ] [ Canvas ] [ SkillPaq ] row.

## [0.26.356] - 2026-10-25

- The bottom-bar traffic button reads [ Σ 12B · 2.2M/h ] (total, then the last hour), and UI-Level now sits before the idle time, in the same place whether idle shows 1m or 59m.
- When several masters are mentioned on a human's request and the leading master answers, the advisors no longer get an "unanswered" nudge, KPI hit or badge. A request nobody answers still nudges its owner once.

## [0.26.355] - 2026-10-25

- After you rename a workspace, the web relay rows, the "Welcome back" title and the command palette show the new name (the stable id still routes everything underneath).

## [0.26.354] - 2026-10-25

- Clearing a Codex worker handles Codex's "Where should the new conversation run?" question: tldrq picks "Use current Git worktree" (never a new worktree), waits for the fresh prompt and then sends the setup once; no stray keys are left in the composer. An unconfirmed setup submission or a pasted setup left unsent is reported instead of retried blindly.

## [0.26.353] - 2026-10-25

- A new tldrq release now counts as a reason for the master's "Worth opening?" opener after a long silence, if that channel has not been told about it yet. The release comes from the signed server list, never from the installed binary; each channel starts silently from the release current when it is first checked.
- `tldrq channel send|say|reply --release-version VERSION` (and MCP release_version) records which release a post announced; the operating-model release sub-skill tells masters to use it.

## [0.26.352] - 2026-10-25

- `./test.sh quick` also runs the -short tests of every package that imports a changed package, and the named slow PTY tests a changed file owns (third column in scripts/quick-tests.map); it prints the selection first. Its change list `.quick-changed` is git-ignored and deleted after use.

## [0.26.351] - 2026-10-25

- After a person has been quiet across the whole workspace longer than the Initiative dial allows (low 8 h, normal 3 h, high 1 h; default low), the Team's master gets one "Worth opening?" wake when there is a recorded reason: an unanswered question or blocker, or a result that person asked for. Never at night (00-07 in the person's own zone), never when they said they stepped away, at most once per quiet period; the master decides whether to write. Set the zone with `tldrq person --for NAME timezone Europe/Moscow` (unknown zone: no opener); change the dial with "initiative off|low|normal|high".

## [0.26.350] - 2026-10-25

- When an agent is woken by a person's channel message and answers only in its terminal, it gets one private nudge right away to post its reply; if it still does not, its master gets a KPI line and the message is marked "unanswered" until an answer arrives. A reply or reaction to that exact message, or `tldrq channel receipt <channel> <seq> --outcome handoff|defer`, counts as answered. Terminal text is never copied into the channel any more: masters that relied on auto-forward now get nudged to post.

## [0.26.349] - 2026-10-25

- The web relay gets one session per tldrq shell a person started: only the Team's primary master dials; further master sessions in the same window no longer show up as extra rows.

## [0.26.348] - 2026-10-25

- tldrq reads simple signals from a person's messages, with no model: a burst of quick messages, a long gap, an ask repeated after no answer, stress words, stepping away. When one fires, the agent gets one short line (at most 120 bytes), for example "human: burst 4 · stress high · repeat of #5541 · humor 0 now"; nothing is added for normal messages. Thresholds and cue words come from the humans-rituals-and-psychology SkillPaq, so a workspace can tune them.

## [0.26.347] - 2026-10-25

- The [ ASK!ME ] button is gone from the bar. Say "grill me", "ask me about X" or "interview me" and the master runs the same decision interview through the new built-in enmaq/ask-me (the `tldrq askme` commands stay).

## [0.26.346] - 2026-10-25

- New built-in enmaq/operating-model: one SkillPaq that explains end to end how work runs (request, ticket, one owner, workers and teams, who knows what, status, release), with every permission kept; nine overlapping packs are merged into it. Its short overview is in every primer, the sub-skills are read on demand.
- enmaq/human-rituals becomes enmaq/humans-rituals-and-psychology, learned from a week of real messages: answer a repeated ask first, keep ETAs, step-away and light moments, message gaps and stress signals; rules marked by evidence (one person, two people, general knowledge); dials for humor, honesty and initiative and a signals part as data.
- scripts/humans-study: a repeatable, read-only study tool (prepare, model pass, merge with quote checks).
- In the browser view: paste an image or drop files anywhere; they attach to the open thread or channel composer as a reference you send (4 MB cap, same as the terminal).
- In the browser view, your messages show as a tinted card, agent messages stay plain, and existing buttons render as flat buttons.

## [0.26.345] - 2026-10-25

- The built-in quick-status status format now leads with what is needed from the owner, gives evidence and what is not verified in every note, lists every release with its Pacific time from the release record, and ends with Facts and Corrections lines; customer-neutral wording.
- Masters always get the status format and the link to the status canvas that is actually kept, refreshed on every wake, not only at start.
- No more "started / finished: work item" lines in the human channel. In the Verbose style, work steps go only into the thread the request came from, only for named work between a Team's own master and worker.
- Humor dial: type "humor 50" (0, 25, 50, 75, 100; default 25) and agents allow a light touch in relaxed moments, never on failures, decisions or late work. Honesty is fixed at 100 %.
- Esc closes an open completion popup first (your text stays), then clears the composer with Ctrl-Z to undo, and only an empty composer closes the thread. A [ clear ] button sits next to [A+] while there is text.

## [0.26.344] - 2026-10-24

- "↓ N new" now counts the messages that arrived since you last read the channel or thread (not your own), and a thin "new" line marks the first unread message.
- A message sent to a name that matches no Team member is refused with that name and close matches (for example eng2-madeline) instead of being reported as delivered; members who are offline still get it later.
- In the Verbose style, an agent's saved canvas shows as one step with the canvas link.
- Skill candidates read plainly in the master's review: your own sentence, who reviews it and how old it is, no JSON; an unreviewed candidate is re-sent once after 2 hours and marked overdue after 24; declining or proposing removes it.
- Every SkillPaq rule now needs its "How this rule works" (when / do / if not run): proposing, editing or approving a rule without one is refused, and a workspace pack missing it is named once at load. The skill-formation summary asks for rules any team could use.
- In the browser view, the cursor is a filled block in reversed colours that blinks, hollow and still when the page is not focused, steady while you type and for people who turn animations off, so you can see which field has focus.
- New built-in pack enmaq/work-principles: tickets of about 20 minutes, all started at once on separate workers on a fixed base, one combined test and one fix round, with the human looking at the screens during the test.
- New `./test.sh quick` pre-seal check: the tests owned by the changed files, vet, and the release-target check, in about a minute.

## [0.26.343] - 2026-10-24

- Channel header is simpler: one [ Team ] button opens People and Settings (Config Team and Members are inside it); the "TEAM ·" label and the INSIGHTS button are gone (type "insights" to open that view); Steer and Complete are gone from the header (use the chat words "steer:", "complete", "stop"), so each member's activity words line up under that member again.
- During a run one plain line says "Working on 1 task · 3 done [ Show tasks ]"; the budget appears only past 80%.
- Your own messages sit on a light block so they stand out from agent messages, in light and dark themes.
- At beginner UI levels, member chips show plain role words, and a click shows role, model and effort with a one-line explanation.
- "Typing…" and "thinking…" show inside the thread where they happen, not only in the channel.
- Light theme: agent text and headers are fully readable (some words used to be faint).
- New built-in pack enmaq/batch-release: when a person tests a batch, it ships as one release, tested once.
- New built-in pack enmaq/one-ticket-never-blocks: a ticket that fails the full test is rolled back and the rest of the batch ships; changes to shared screen parts run that part's tests and a compile for every shipped platform before sealing.
- The built-in enmaq/todo-tickets pack is generic: it no longer names our own project folders and ticket prefixes; each project's ticket folder sets its own.
- While your last request is scrolled out of view, a one-line bar at the top of the channel or thread shows it; click to jump back. A "↓ N new" button jumps to the end.
- Long messages fold under "Show more" (yours after 3 lines, agents' after 6); the two newest agent answers in each chat or thread always stay open.
- Each delegated task shows "<worker> started: <item>" and "<worker> finished: <item>" in the channel (Natural, Structured and Verbose styles; not in Succinct).
- Agents post one plain sentence when they finish a step of their plan (Natural and Verbose), and a new built-in pack explains each Team role in plain words.

## [0.26.341] - 2026-10-24

- While an agent works on a message from a channel, that channel shows "doyle is thinking…" until it answers.
- In the Natural style, agents confirm a like or a quick ask that starts work in one plain sentence ("On it, indexing backend and frontend now"); Succinct and Structured keep it to one line or a reaction.
- New communication style Verbose: dispatches, worker results and canvas edits by the Team's masters appear in the channel as generated step lines, folded into one "doyle: 6 steps" row that opens on click. No extra model text.
- Search inside a shell no longer comes back empty under heavy CPU load: a catch-up refresh cut short by its deadline keeps an already-complete index complete.
- A like on an agent's question or proposal, on the whole message or on that one line, now tells the agent it means yes: it answers "On it: ..." in the thread and does it. A like on a status message still needs no reply.

## [0.26.339] - 2026-10-24

- The background collector no longer inherits a shell's private tldrq proxy, so machine presence (the web "Online" state), notifications and usage reports keep reaching the server after a collector is started from a shell. A failed presence report is logged once per change, with its reason.

## [0.26.337] - 2026-10-24

- Only shells a person drives (the Team cockpit and its masters) connect to the web relay; worker shells spawned by a master no longer appear in the web session list or use relay links.

## [0.26.336] - 2026-10-24

- The web relay logs why a connection is refused: "auth refused 403, paused", "update required 404", or the handshake status code before a retry, once per change instead of a generic failure on every retry.

## [0.26.334] - 2026-10-24

- Clicks in the Team form, Help and the resource and traffic popups are counted too. The external login flow is not part of the app and is not counted.
- Text in tldrq messages and skills keeps every backslash and quote exactly, also for text built by tldrq itself.
- Idle Codex workers can be cleared: the clear no longer mistakes Codex's empty prompt placeholder for a busy worker.

## [0.26.333] - 2026-10-24

- Clicks in the member picker, settings, Team menu and confirmation dialogs are now counted too (fixed paths only, no text or names). Dialogs not yet counted are marked so they are never reported as unused.
- A master can clear its own context: `tldrq team control clear --reason "<status canvas; tickets>" self`. The clear waits until the master is idle and is refused while it still waits for answers, has unsent messages or runs a Team iteration; the reason comes back as the first message after the clear.
- A shell logged in to one server no longer shows Guest when an unrelated server rejects a request.
- Model health push notifications carry the model name (claude, codex), so the notification can say which model is down instead of "Platform".

## [0.26.332] - 2026-10-24

- A logged-in tldrq shell keeps a connection out to your account, so you can open your own running sessions from web tldrq. It reconnects on its own after a server restart.
- Team menu Clear now really clears Codex workers (/new) as well as Claude workers (/clear). It shows one plain line per worker: cleared, kept (still has work queued, or masters clear themselves), or no answer in 15 s.
- Fixed: since 0.26.325 a message containing a double quote reached agents cut off at that quote, so an agent could see an empty message and not answer. Messages now arrive whole, and a thread label can no longer break them.
- Invite an agent from another Team into one channel: `tldrq channel invite <channel> <agent> --human`. The guest can read and chat only in that channel, and can be removed again at any time.

## [0.26.331] - 2026-10-24

- With "Share usage" on, the hourly SkillPaq usage report also counts button clicks per screen path and UI level (no labels, names or message text), so buttons nobody clicks can be found and removed. Dialog and settings buttons are not counted yet.
- Joining a Team from the cockpit or through MCP registers the shell first, or says exactly what is missing, the same as the shell start path already did.
- New built-in skills: enmaq/canvas-debates (agents debate on one canvas per question, with sources and a skeptic, and the master writes the decision at the top) and enmaq/clear-workers (masters clear a worker's context when its ticket is released and at the end of a wave, with the right command for Claude or Codex).

## [0.26.330] - 2026-10-24

- A team chat whose wake delivery fails is retried (5 s, 30 s, 2 min, then every 10 min) instead of going silent, and tldrq status shows "chat wake late: <chat> since <time>" when a chat has waited more than 5 minutes.

## [0.26.329] - 2026-10-23

- At detail levels 1 and 2 on narrower screens (37-99 columns) the top bar keeps "no finish time yet" visible while a run is active (it used to disappear).

## [0.26.328] - 2026-10-23

- Shells register themselves with the tldrq gateway before joining their team, so the "gateway registration failed (400)" warning every team showed since 19 Oct is gone and other machines can see the team again.

## [0.26.327] - 2026-10-23

- A message an agent receives from inside a thread now starts with that thread ([in thread #N "topic"]), so agents stop answering in the wrong thread.
- Chat words for runs: the master runs steer:, stop, complete, pause and resume when you type them; pause and resume are new master-only commands.
- Below level 5 the run status block no longer appears and no longer pushes the chat down when a run starts; the steer hint shows once.

## [0.26.326] - 2026-10-23

- The UI level is kept when the same project is opened through a symlinked path (it used to start again at level 1). Each new shell now logs which repo, workspace and level it loaded.

## [0.26.325] - 2026-10-23

- A chat message ending in a backslash could stop a whole team chat from waking its masters: every later message stayed undelivered (seen in the tldrq-cloud chat since 16:26 UTC). The reader now handles escaped backslashes, and one message that still cannot be read is skipped with a log line while the rest are delivered.

## [0.26.324] - 2026-10-23

- The token total in the bottom bar survives restarts again (a new proxy could not load the saved totals while an old one held a lock).
- Run buttons: none below level 5; at level 5 only Steer and Complete while work runs. Steer works now (it did nothing before): it opens the message box in steer mode and Enter sends the steer to the running work.
- Workers who joined before a run started can be given work.
- Everything you can click keeps its [ ] at every level; the level control reads [ UI-Level n ] (short [ UI n ] when space is tight, never a bare digit). Buttons keep the same place at every level.
- One close rule for Threads, Canvas, Processes and SkillPaq: the top-right [×] closes the pane and keeps its tabs; a tab's × closes that tab; closing the last tab closes the pane.
- New built-in skill todo-tickets: one ticket per piece of work, kept in step with the domain's TODO.md.

## [0.26.323] - 2026-10-23

- Plain words at detail levels 1 and 2, written so a 5th grader (level 1) or a 9th grader (level 2) can use them: "Simple 1" / "Simple 2" for the level control, "Send · Shift+Enter: new line", "Enter sends · Alt+? shortcuts", "active 2 min ago", "open for 2 min" / "no finish time yet", "Urgent 1", "Style N · Urgency 2", "Guest", "Help", "Big text", and the side tabs written out (Threads at level 1; Threads, Canvas, Skills, Processes at level 2). Narrow screens drop whole optional words instead of shortening them. Levels 3 to 5 keep today's labels.
- The Iterate, Status and machine-resources buttons are gone from the bottom bar. Their jobs stay: say "iterate", "status" or "resources" in chat, the health and resource warnings colour the ▗ logo, and clicking the token stats (or the battery) shows machine resources under the traffic numbers.
- "New build, close and reopen" is now a small [⟳] next to the idle time, in a slot that is always reserved so nothing moves; click it for the message.
- Chat words start what the hidden buttons did: "ask!me" or "grill me" starts the decision interview (new `tldrq askme start`), "status", "iterate", and "resources" (new `tldrq system resources`). A built-in skill lists them.
- Phones and narrow terminals: every message shows its time and a Thread button again (the name is shortened with … instead).

## [0.26.322] - 2026-10-23

- Messages no longer jump when you hover them: at every detail level each part of a message is either shown or hidden, never shown only on hover. Levels 1 to 3 show the full name, time, text, attachments, long-message fold, reactions and threads; the model tag from 3; reply, delete and receipts from 4; routing and quotes at 5. Level 5 is unchanged.
- SkillPaq usage: the first report goes out 5 minutes after tldrq starts, then hourly, so a fresh start reports soon instead of after an hour.
- New built-in skill owner-decisions: when you decide how something must look or behave, agents keep your words in one checklist and check every line before saying done.

## [0.26.321] - 2026-10-22

- Threads on tall or narrow terminals (phones, portrait screens, under 132 columns) open full screen instead of in a half pane; typing goes straight into the thread. Wide screens keep the split.
- The dotted separator row no longer disappears when a thread opens.
- Browser view: the zoom dropdown is replaced by in-page − ×n + buttons, which also work where the browser blocks its own menus (cars, kiosks). Saved zoom, the 40-column limit and Alt+Shift+Z still work.
- Busy machines: many agents polling at once no longer get "collector busy". Empty polls no longer take the database write lock, and the last-seen time is saved at most every 10 seconds.
- Four new built-in skills from this week's work: ship-safely, ui-no-surprises, verify-before-claiming and ask-before-building.
- SkillPaq usage: tldrq counts which skills were loaded and applied each day and sends the counts hourly, so we can see which skills help. No names, text or personal data: built-in skills by name, your own skills only as a one-way fingerprint. On by default; turn off with `tldrq skillpaq usage off` or Settings, Share usage.

## [0.26.320] - 2026-10-22

- Fixed: at level 5 the bottom bar again shows everything it showed before 0.26.319 (token stats, battery, search, idle, clock). The new [UI n] control had taken their space; now it only uses free space, then shortens to [5] (or a single digit on narrow screens), and never removes another part. Token stats show at levels 4 and 5.
- Detail levels, slice 2: both bars follow the level. Bottom bar: level 1 keeps the logo, workspace, your name, update notice, tabs, [T], idle, [UI n], [?] and power; style and urgency come at 2, the tool buttons and clock at 3, search and proxy at 4, the token stats at 4 and 5. Channel top bar: level 1 shows the chat name and what is known about the team; buttons and details return level by level. Hover shows the hidden parts; nothing moves when data arrives. Reactions and threads show at every level; the ASK button from level 2.
- Pasted screen text no longer changes urgency: a copied bar containing "[ U: P1 HIGH ]" set urgency to P1 by mistake.

## [0.26.319] - 2026-10-22

- Detail levels, first slice: a `[UI n]` control in the bottom bar (before the traffic meter) sets how much each message row shows, from 1 (sender and text) to 5 (everything, exactly as before). Click to cycle; the screen updates at once and keeps your draft and cursor; the level is saved per workspace. In between, hidden parts appear when you hover or select a row, and the time shows from level 2 (on hover at level 1). New users start at 1, existing users at 5. Other screens follow.
- tldrq reports each of your machines to the platform (a random machine id, host name, version and workspace names, at start and every 5 minutes), so the TLDRQ page can list your machines. Logged-out machines send nothing; failures are silent.

## [0.26.318] - 2026-10-21

- Typed letters show instantly (predicted) in dialog fields such as the Open workspace search, as they already do in the C1 composer. Before, those fields drew their own cursor, so the browser view never predicted there.

## [0.26.317] - 2026-10-21

- In the browser view, keys typed before the connection is fully ready are kept and sent in order as soon as it is, instead of being dropped with "not sent". A failed send keeps the keys and retries; the warning clears once input flows again. Only a very full queue (512 waiting inputs) refuses new input, visibly. The first key after the link is ready still goes out at once.

## [0.26.316] - 2026-10-21

- `tldrq vv` calls no longer get stuck in "checking" when the first connection candidates arrive before the other side's offer or answer: candidates wait until the description is set, and connection errors are logged instead of dropped.

## [0.26.315] - 2026-10-21

- The name box at the start of the bar has a fixed width, so C1, M1 and the other tabs never shift when a worker with a longer name joins. Before, a click aimed at C1 right after start could land on the gap. Longer names end with "…"; the full name is in [?] and copy.
- The SkillPaq view explains each rule under "How this rule works": WHEN, DO and IF NOT RUN, with a short preview on P that stops on any key, click or resize. All built-in SkillPaqs have it; agents' instructions are unchanged. An empty "RULE 1" heading no longer shows.
- An urgency confirmation always goes to the collector that started it, even if the collector changes while it is being sent.

## [0.26.314] - 2026-10-21

- An agent shows as blocked by quota only when its tool says the limit is actually reached. A "less than 25% of your weekly limit left" warning, or chat that merely talks about quotas and resets, no longer marks agents (or their master) as blocked in the Team list and status line.

## [0.26.313] - 2026-10-21

- No code changes; changelog wording only (same program as 0.26.312).

## [0.26.312] - 2026-10-21

- The power button asks with the CLOSE dialog for a saved master even when its Team configuration is missing or names no owner. Before, such a master was shut down at once, without the dialog or the animation.

## [0.26.311] - 2026-10-21

- The Team pass also renews after you reopen an existing workspace. In 0.26.310 a reopened shell could reconnect after a collector restart without renewing, so SkillPaq proposals still failed with "stale Team token". It now renews once on the first successful reconnect; a failed renewal waits for the normal reconnect delay instead of retrying in a loop.
- Closing tldrq plays the animation and hands the terminal back reliably. About one close in three still lost the animation, once with a 24 s wait: when CLOSE stopped a worker, the worker's cleanup also removed the master's session before it could restore the screen. Each session now cleans up only its own record.
- The Team menu stays open while channel history finishes loading after start. Before, the loaded history could paint over the menu and make it vanish; history now updates underneath and shows when the menu closes.
- The real-path release check now starts from a copy of an existing team (Welcome back, REOPEN, no Form team), the way a normal day starts.

## [0.26.310] - 2026-10-21

- The old web UI is gone. The browser shows the same screen as the terminal (Exact view) for the Teams menu, Form team, channels and canvases; the old HTML pages, `/console`, `/ws` and their REST endpoints are removed (they return 404). Not in the browser yet: file upload, image paste and inline attachment previews.
- `tldrq channel read` and `reply` accept `C1`-style names, and a failing `tldrq` command always prints its error, even in shells that log diagnostics to a file. Before, `channel read C1` failed silently there.
- An agent's Team pass is renewed automatically when its shell reconnects after a collector restart, so actions such as proposing a SkillPaq keep working. Before, a pass signed by an earlier collector was refused with the misleading "active Team member only"; if renewal ever fails, the error now says "stale Team token" and to restart that agent's tab.
- The real-path release check reads the expected version from the build, so it needs no manual update per release.

## [0.26.309] - 2026-10-21

- Urgency follows what you say: an explicit P0 to P3 wins (P0 is capped at High), and calm words such as "no rush" or "take your time" lower it. "Out for the night" on its own changes nothing. Only human messages count; quoted text and talk about levels never do. When the level changes, C1 gets one line saying so. The words live in the built-in urgency SkillPaq, so a workspace can override them; a broken override changes nothing and shows the error.
- `tldrq code search --body none` (and `body_mode=none` for agents) returns only file, line and column, never source text. Before, it still printed the matched line and nearby lines, which could expose secrets in a repo. The default compact output keeps plain function and method names but no source text.
- New pre-release check of the real daily path (startup, channel history, one send, SkillPaq list, a canvas, closing tldrq) runs before every release (`./test.sh your-path`).

## [0.26.308] - 2026-10-21

- Closing tldrq (power button or Ctrl+C, then CLOSE) plays the shutdown animation and hands your terminal back without a key press in the normal supervised mode too. Before, tldrq stopped itself with a kill signal in that mode, so it quit with no animation and the screen could stay stale. Stopping a session from outside with `tldrq stop` is unchanged.
- The shared tldrq collector belongs to the home folder that started it. A leftover test shell with a different HOME could restart it under that HOME, after which human-only actions (such as listing SkillPaqs) failed with "human approval only" and the SkillPaq list looked empty. A shell with a different HOME now never adopts, restarts or replaces a running collector; it stops with an error naming the home-folder mismatch. The SkillPaq pane shows Loading or the full error instead of an empty list. Test collectors on their own port keep their own HOME.
- Clicking the tldrq logo flashes again while the collector is unreachable; the outage paint used to cover the flash.

## [0.26.307] - 2026-10-21

- Channel views use far less CPU in busy teams: when agents flip between busy and idle, tldrq no longer re-wraps the whole channel history (that change is invisible on screen), and thread counts no longer touch every message. Measured on a 20,000-message channel with frequent events: from 79% of a CPU core to 4.4%. Takes effect when a shell restarts on this version.
- Team sends retry the same message id for up to 10 s when the local collector times out, without redelivering a message already consumed. If the reply is still missing, the tool reports delivery unknown with the message id instead of an error that invites a duplicate resend. Cross-host sends through the gateway are not yet send-once.

## [0.26.306] - 2026-10-21

- SkillPaq review works like email: the list is grouped Proposed, In use, Built-in, then Rejected at the bottom. In a proposed SkillPaq, Enter approves and Esc rejects, and you land on the next proposed one each time, so Enter, Enter, Enter walks the whole queue. In the Rejected group, Esc deletes that proposal for good (no confirm; a "Deleted …" line confirms). Esc on approved or built-in SkillPaqs, or on the list, still closes as before. Switched-off workspace SkillPaqs show dimmed at the end of In use.

## [0.26.305] - 2026-10-20

- Sending in channels uses a queue: Enter saves the message locally and empties the composer at once (a few ms, without waiting for a disk flush), the message waits in a one-line queue above the composer, and tldrq keeps retrying (1 s up to 30 s) with the same message id until it is delivered, also after a tldrq restart, in order per channel and never twice. A rejected message shows `Failed · Retry / Edit` and holds back only its own channel. Typing more while a message is sending can no longer merge two messages. Replies and threads use the queue too; attachments follow later. Known: queued messages survive a tldrq crash or kill, but a power loss or OS crash can lose the last few; a crash within milliseconds of pressing Enter can bring the draft text back.
- Closing tldrq: the power button keeps a fixed spot at the right edge of the bar even when the bar is crowded (the clock gives way first), so clicking where it was no longer opens the clock screen. After CLOSE, a "Closing N agents" line appears at once and counts down while agents stop (up to the existing 3 s grace), then the animation plays and tldrq exits by itself; the final session save no longer holds the exit for more than 0.5 s.
- Dialogs no longer vanish while still open: a terminal resize (window change, tab switch, wake) used to redraw the screen over an open dialog such as Close, leaving it invisible but still taking keys, so the screen looked frozen until a key was pressed. The redraw now leaves every open dialog visible.
- Proxy memory: shells now ask each proxy only for the last 15 minutes of events when showing model activity, instead of the whole event log every 5 s; long-running proxies no longer grow to gigabytes. Restart existing proxies (or the shell) to pick it up.

## [0.26.304] - 2026-10-20

- SkillPaq review: after Approve, Reject or Unapprove you land back on All SkillPaqs with a one-line receipt ("Approved enmaq/x v2"), and that SkillPaq's tab closes. Errors and blocked approvals stay on the detail as before.

## [0.26.303] - 2026-10-20

- Processes: two different repositories with the same folder name (for example two checkouts called `app`) no longer share one Processes history; the same repository opened through a symlink keeps one. Existing history is moved once into the matching repository, only for commands that ran inside it; the old file is left untouched.
- Built-in canvas rule v3: agents retire a stale canvas to one line pointing at the status canvas, and never compress away an uncertainty, a correction or what a decision waits on.

## [0.26.302] - 2026-10-20

- Sending in channels no longer freezes typing: the message shows SENDING at once and you can keep typing. When the collector is slow (for example right after a restart) the send retries quietly for up to 10 s with the same message id, so it lands once; "collector unreachable" now appears only when it is really down. Known: if you edit the text while it is sending and the send then fails, the original is kept only in input history (Up) for this session.
- Canvas tabs work like browser tabs: the top-right [ x ] and the ✕ on the open tab hide it and open the next tab (right, else left), then All canvases when none are left. Hiding another tab keeps your canvas. Deleting from the list returns to the list and says the canvas was deleted (restore still works). No x ever deletes.
- SkillPaq view: what the skill teaches comes first, sections are separated by thin titled lines, only WHEN / DO / IF are highlighted, and the structure is folded; Space or a click opens it as a tree instead of LISP text.
- `tldrq skillpaq check FILE` accepts single-file SkillPaqs exactly as the loader does, instead of failing with "invalid pack id".

## [0.26.301] - 2026-10-20

- SkillPaq pane: channel search (F4), help (Alt+?) and switching to other panes work while it is open, and Esc closes it even after you clicked into the chat.
- Numbered lists keep numbering when the list starts below other text or a blank line ("Steps:" then "1. …" now continues with "2. "). A line starting with "1. " under prose now starts a list on Enter.
- SkillPaq skill detector: the same message sent twice (or with only spacing or punctuation changed) no longer counts as a repeated correction; reworded corrections still do.
- Built-in canvas rule: agents check for an existing canvas on the topic before making a new one, and drop decided options and stale parts when rewriting.

## [0.26.300] - 2026-10-20

- Likes (Space Space): when a like takes more than 150 ms to show its green flash, one line in the shell log records where the time went (each step, channel size, open thread, incoming messages), so a slow like can be traced. Fast likes write nothing; behaviour is unchanged. Measured on a 4,777-message channel the flash shows in 35-80 ms, even when the server answers 2 s late.

## [0.26.299] - 2026-10-20

- Browser Exact TUI: at x1 the page no longer flickers scrollbars on and off twice a second. The view never overflows the window; anything wider is clipped like in a terminal. The x1-x4 sizes are unchanged.
- Reach another team by name: `@enmaq/tldrq-cloud/tom`, `@tldrq-cloud/tom` or just `@tom`, using the workspace's current name or any earlier name, no Team code needed. The `##` and `@` popups list other teams' masters too, matching loosely (`@enmaq--cclouddd` still finds tldrq-cloud), with recently used names first and each row showing workspace and idle time. A name that matches two teams is refused with both addresses listed, never guessed. Known: recent-use ranking resets on restart, and other teams can take up to 10 s to appear after a shell starts.

## [0.26.298] - 2026-10-20

- SkillPaq: each skill version now records how often it was created, reviewed and loaded into an agent's context, with sizes, so whether a skill saves tokens can be measured instead of assumed. Token counts are recorded only when known (never estimated); loading a skill counts as "used", never as "applied". Covers agent onboarding, resumed and reaction wake-ups; shell start-up and context-clear loads are not counted yet.

## [0.26.297] - 2026-10-19

- Browser Exact TUI: bold text sits exactly in its cells again, so words that mix bold and regular letters no longer show gaps or offset boxes (in every theme and scale; this was off since 0.26.278).
- SkillPaq: skills are never deleted or switched off automatically. "Stop doing X" (English or Russian) asks the lead master to retire that skill; a skill unused for 30 days, declined twice, or corrected twice after use is marked dormant for a person to review. Agents report when they actually applied a skill (loading it does not count), and only a person can restore a retired skill.

## [0.26.296] - 2026-10-19

- Browser Exact TUI: Light theme by default (Dark one click or Alt+Shift+T away, remembered per browser); all terminal colours are mapped so text stays readable on light. Scale the cells x1, x1.5, x2, x3 or x4 (header control or Alt+Shift+Z, remembered); bigger cells mean fewer columns, never page overflow. Scales that would leave fewer than 40 columns are greyed out with the reason, and a too-large remembered scale steps down on a small window and comes back when it grows.
- SkillPaq: the first time a person corrects a rule of an approved skill, the lead master is asked once to propose an updated version (linking the correction, never copying it); skills are never edited silently.

## [0.26.295] - 2026-10-19

- Forming a team with several Masters retries with a new name when a Master's name gets taken while the team is starting, instead of failing. If it still cannot start a Master, the message says which one, why, and what to do, in plain words.
- SkillPaq: a formed-skill candidate states its scope and conditions, links to the evidence instead of copying the person's text (so exceptions are never cut off), and personal details are removed before it reaches the master.

## [0.26.294] - 2026-10-19

- New workspace names accept any text: spaces and punctuation become `-`, accents and Cyrillic are written in Latin letters, and the result (max 40) shows live under the field; what you typed stays as the display name. A name already in use gets `-2`, `-3`. `--workspace` on the command line uses the same rule but always picks the existing workspace.
- Ctrl+C and deleting a workspace show the shutdown animation again (each frame is drawn on its own instead of one held-back block), and the browser Exact view redraws even if a program leaves a synchronized-output block open.

## [0.26.293] - 2026-10-19

- Starting a team with more than one Master no longer fails with "team worker role is already in use" when the chosen Master name is already used by another team: names are checked against every live agent in the project, and a taken name just moves on to the next one.

## [0.26.292] - 2026-10-19

- Form team is back to the three-column layout of 0.26.289 (the one-column form from 0.26.290 is removed); a single Enter forms the Tandem team again.

## [0.26.291] - 2026-10-19

- Agents whose git goes through the tldrq proxy can push and fetch again: the proxy now asks for credentials with a proper 407 answer (and closes that connection so git reconnects), and wrapped agents get `GIT_SSL_CAINFO` pointing at the proxy's trust bundle, so git accepts the proxy certificate. TLS checks and the proxy stay on; a `GIT_SSL_CAINFO` you set yourself is kept.

## [0.26.290] - 2026-10-19

- When the enmaq servers are unreachable (outage, refused connection, timeout), the shell stays calm: the tldrq logo turns red with a small ⚠ next to it, with no change in width. Clicking either, or Alt+? then O, shows the host, status, since when and the next retry; it returns to normal by itself when the server answers. Nothing is printed over the shell any more: tldrq's own startup and background messages go to `~/.tldrq/shell.log`, and the owner link and token file stay in help.
- `tldrq login` and the shell ask you to log in again only when the server really says you are signed out; an outage or an expired token while offline never does.
- SkillPaq: tldrq notices when a skill has formed (a person says always, never, from now on or remember; the same correction comes twice; the same steps succeed three times) and asks the team's lead master once to propose it or decline with a reason. It uses no AI model, wakes at most once an hour and three times a day, and its rules live in the built-in enmaq/skill-formation pack, which a team can change like any skill.
- SkillPaq tab shows `(20) · N proposed` when proposals wait for you; every proposal attempt is logged.
- Form team is one column: tools, one line per role with ‹ N › counts, a single "fits" line (details behind ?), and small Create/Cancel. Fits an 80x24 terminal and a phone.

## [0.26.289] - 2026-10-19

- The status bar keeps the Team button at every width: on a narrow terminal or a phone the workspace name and the date go first, so [T] and the urgency control stay and clicking [T] opens the Team menu.
- Browser Exact TUI: the channel members list has real buttons. Clicking a member toggles it exactly as Space does, and Save/Cancel work like Enter/Esc; the picture stays identical. Watch-only navigators cannot change anything.

## [0.26.280] - 2026-10-18

- The shell browser now opens straight into the Exact TUI. Its legacy Web UI toolbar, dialogs, scripts, and view switch are removed from the page.

## [0.26.279] - 2026-10-18

- Hovering a message line shows the reaction bar on that same line, at its right end, in the channel and in threads alike (one rule, one code path). It uses the empty space after the text and covers the end of the text only when the line is too full; the text comes back when you move away. Fixes the bar appearing only sometimes in threads.
- Browser Exact TUI: the terminal now takes the size of your browser window (a phone gets a narrow terminal, a large window a wide one), and resizing the window resizes it. With a real terminal attached too, whichever you typed in last sets the size; your next key in the other one takes it back and redraws.
- Browser Exact TUI: Ctrl+V and Ctrl+Shift+V paste your clipboard (multi-line and any language) instead of sending a control character.
- Browser Exact TUI on a phone: a sideways pan stays where you put it, and taps land on the cell you touched. Known gap: at phone width the status bar has no room for the Team button yet; that comes in the next release.
- Groundwork for browser buttons on the channel members list; nothing visible yet.

## [0.26.278] - 2026-10-18

- Browser access is now protected: [W Browser] opens you as the owner with a one-time key that becomes a private session cookie (the key itself is never stored in the browser); opening the shell's address without it is refused. The owner key sits in a file only you can read, and its path and the owner link are printed when the shell starts.
- Navigators: the owner can create a watch-only link to the Exact TUI view; every key, click or resize from it is refused on the server. The owner can end any session, which also closes its connections.
- Browser: the Exact TUI view draws long runs of text as one piece instead of one element per cell, so large screens open much faster and use far less memory (a 105×310 tldrq screen: 1,793 elements instead of 97,752).

## [0.26.277] - 2026-10-18

- Browser: rows are exactly one character tall, so coloured backgrounds have no stripes between rows and box-drawing lines join, in both the Web UI and the Exact TUI view.
- Browser: reversed colours (highlighted title bars in nano, top, less) now show in the Exact TUI view and the Web UI.
- Browser Web UI: accented letters keep their accents, and every wide emoji takes two columns. One width table, generated from the same rules the terminal uses, now drives tldrq's layout, the terminal output and the browser.
- Browser: the Exact TUI view works on a phone: the screen shrinks to fit (down to 12 px text) and pans sideways beyond that, a tap opens the keyboard, and the cursor row stays visible while it is open.

## [0.26.276] - 2026-10-18

- Browser: a new Exact TUI view shows the whole `tldrq shell` screen exactly as the terminal does (dialogs included), switchable with the existing Web UI. Only changed rows are sent and redrawn; typing, mouse, paste and resize go back to the terminal numbered and confirmed, so a reconnect never loses or repeats a key, and keys sent before a shell restart are shown as not sent instead of replayed.
- Browser: Alt+Shift+L in the Exact TUI view shows how fast keys appear (last, median, slowest 5%) with lost and pending key counts; a summary is written to `~/.tldrq/shell.log`.
- Wide characters (Chinese, Japanese, emoji) take exactly two columns in the browser and in programs shown inside tldrq, so rows no longer shift; accented letters stay intact.
- Browser: a thread's address line no longer overlaps its messages.

## [0.26.275] - 2026-10-18

- Hovering a message line pops up the reaction bar on the line just below the pointer again, never on the line you are hovering (it broke in 0.26.261). A one-line message whose header has scrolled off now gets the bar on the blank line under it.
- Browser: a plain click on a channel attachment opens a preview (images, text, PDF) or downloads it, so files work in a browser-only session. Ctrl/Cmd-click still reveals the file on the host.
- Browser: terminal text in the light theme has readable contrast.
- `tldrq shell --browser --team …` starts straight in the browser, without the terminal "Choose workspace mode" dialog. The browser still asks how to start when no team is given.
- Groundwork for showing the exact terminal screen in the browser; nothing visible yet.

## [0.26.274] - 2026-10-18

- Processes and SkillPaq now use the same pane design as Canvas: one header with item tabs (× hides a tab, nothing is deleted), an `[ All … (N) ]` list and an address line, with the large action buttons kept. Every tab shows a plain `Name (N)` count (`…` while loading). Terminal and browser.
- Presence: a chat or canvas header shows coloured initials of who has it open now (they fade after 2 minutes). In a canvas, another person's cursor is marked in their colour without hiding your text, and a chat shows "Alice is typing…" above the composer. Each person keeps one colour everywhere; agents show a seen dot and typing only.
- The team menu no longer goes empty after a collector restart: running shells re-register on their next heartbeat. Shells started before this version need one reopen.

## [0.26.273] - 2026-10-18

- Canvas: after 1 s without typing, a large `Finished editing? Press Esc` button appears at the bottom. Esc (or a click) leaves editing and, once your edits are saved, sends agents one "finished editing canvas N" note with the diff right away. Any other key hides the button and is typed normally; Enter stays a new line. Terminal and browser.
- Canvas is an endless page: Down, Ctrl+N and Right at the end of a line keep moving past the last line; blank lines and spaces are added only when you type there.
- Hovering any line of a message always shows the reaction bar: on its header when visible, otherwise on the first visible line of that message, never covering the line under the pointer.
- Groundwork for presence (who is in a chat or canvas); nothing visible yet.

## [0.26.272] - 2026-10-18

- Threads, Canvas, SkillPaq and Processes all take 50% of the screen and show two panes at a time. With a thread open, Canvas, SkillPaq or Processes opens on the left and the thread stays on the right; with no thread, the channel stays on the left. Esc closes the top pane and brings back the one it covered, as it was. Terminal and browser.
- The help screen (`Alt+?`) is easier to read: keys in the accent colour, bold section headings, aligned columns, and a larger window that fits the screen (fewer pages, nothing cut off).
- `Ctrl+Alt+T` opens Threads, like `Alt+T` (matching `Ctrl+Alt+C/S/P`).
- Processes: on the Rerun confirmation, Enter now reruns the command and Esc cancels (Enter used to cancel).

## [0.26.271] - 2026-10-17

- An empty Processes tab says "No commands yet. Run !command in the composer." once, across the whole pane, instead of twice in two columns. The filter hint is shorter ("filter commands") so it fits at 80 columns; a filter with no match says "No matching commands."

## [0.26.270] - 2026-10-17

- The SkillPaq and Processes button bar no longer draws a white band across the bottom: the bar sits on the pane's dark background and only the buttons are filled.

## [0.26.269] - 2026-10-17

- The long shortcut line under the composer is gone. An empty composer shows one muted hint instead, chosen by context (unread messages, a running command, a selected message, an open thread or canvas) and ending with `· Alt+? all keys`. It changes when you send or refocus, never on a timer, and disappears as you type. The browser composer shows the same hints, with `Shift+Enter newline` for a new line.
- The Processes tab shows running/total, e.g. `[ Processes (0/50) ]`, in grey; Threads stay blue, Canvas purple, SkillPaq orange. At narrow widths all four tabs stay visible with short labels.
- Fixed the blue background spilling to the left of the tabs.

## [0.26.268] - 2026-10-17

- New `[ Processes (N running) ]` tab, first in the tab strip (`Alt+P`), in the terminal and the browser. It lists commands run from the command tray (`!command`): running ones first, then finished ones with ✓ exit 0, ✗ exit N or ⊘ stopped and their duration. Selecting one shows who ran it, when it started and the end of its output.
- Actions: `Stop` a running command (only its own processes), `Copy output → composer` (never sends), `Rerun` a finished one after a confirmation that defaults to Cancel, `Delete` a finished entry. The last 50 finished commands are kept across restarts, per workspace, outside the repo.

## [0.26.267] - 2026-10-17

- SkillPaq review uses one row of large buttons, in the terminal and the browser: a proposal shows `Approve · Enter` (default), Reject, Edit, Visibility and `Close · Esc`. While the safe-to-share check has findings, Approve shows as `Blocked` and Enter does nothing. Built-in skills show only Close; Back appears only in a nested narrow view.
- `Unapprove` on an approved skill undoes an accidental approval: the skill returns to proposed, the revocation is recorded next to the approval receipt and nothing is deleted, so it can be approved again.
- `Ctrl+Alt+S` no longer opens a blank page when skills cannot be loaded; the status and the error stay visible.

## [0.26.266] - 2026-10-17

- The collector log names who started each collector (parent process, command, handle) and why (no pid file, stale pid, health check failed), so an unexpected restart can be traced to its source.

## [0.26.265] - 2026-10-17

- Pressing `Alt+T`, `Alt+C` or `Alt+S` again cycles through threads, canvases or skills with activity in the last 8 hours, newest first, and wraps around. The item header shows the position ("3/5 in last 8 h", or "latest available" when nothing is that recent). `Esc` closes; `Alt+Shift+T` / `Alt+Shift+C` still open the full lists.
- The SkillPaq view shows the skill in plain language on top and its LISP below in grey, indented and highlighted. Safe-to-share findings stay marked in the source, the detail scrolls while the review buttons stay visible, and the skill list is 20% wider.

## [0.26.264] - 2026-10-17

- `Alt+S` (or `Ctrl+Alt+S`) opens the SkillPaq tab, like `Alt+T` for Threads and `Alt+C` for Canvas; workspace settings moved to `Alt+O`. `Alt+Shift+S` still sends.
- Canvas links in channel and thread messages, including `[label](tldrq://…/canvas/N)` links, open canvases from other workspaces in the same project as read-only views, keeping their workspace and link visible. A link to a different project says it is unavailable instead of doing nothing.
- The SkillPaq catalog records when each skill last changed (built-in skills have no date).

## [0.26.263] - 2026-10-17

- Agent control keys can dismiss a blocking dialog immediately instead of waiting behind queued messages; normal messages remain held until the prompt returns.

## [0.26.262] - 2026-10-16

- The SkillPaq tab label is orange in the terminal and the browser, so skills stand apart from Threads and Canvas; its count shows without a padded space ("SkillPaq (4)").

## [0.26.261] - 2026-10-16

- SkillPaq tab beside Threads and Canvas (terminal and browser): one list of every skill (proposed, approved, workspace, built-in) with search over names and rule text, the total on the tab, and the selected skill's LISP with the review controls. Approval still binds the exact reviewed hash.
- Channel hover controls stay on the message header and never cover the text under the pointer; when the header is off screen they are hidden.
- Fixed a race that could misplace channel text: terminal output and the status bar's cursor restore no longer interleave.

## [0.26.260] - 2026-10-16

- Skills (local, first slice): agents can propose a SkillPaq with `skillpaq_propose` and list open proposals with `skillpaq_drafts`. A proposal is a canonical `(skillpaq ...)` LISP document, never Markdown. A proposal close to an existing pack becomes a versioned update of that pack instead of a new one, unless the agent justifies a new pack.
- New Skills panel (Team menu `[S] Skills`, browser toolbar `[Skills]`) with Proposals, My skills and Review tabs. Review shows the exact LISP source, its hash, the parent pack and a diff. You approve, reject or edit there. Agents cannot approve.
- Safe-to-share check before approval: secrets, tokens and private facts from your profile are flagged and block approval until the source is edited and re-scanned. Approval binds the exact reviewed hash. Approved packs are pinned on this device and marked "approved on this device (local)". Account signing, sync and other visibility levels come later.

## [0.26.259] - 2026-10-16

- Your sent message appears as soon as the collector accepts it; the full channel reload runs in the background instead of delaying it. Messages from others sent at the same moment are kept exactly once, and a failed send restores your draft.
- A new message in another thread no longer clears the open thread's rendered rows.
- Slow channel-send log lines include the process and channel, and split message reads from acknowledgement waits.

## [0.26.258] - 2026-10-16

- Removing a worker (by hand or by Auto-optimize) now closes its tab and ends its agent: the master shell compares its tabs with the Team roster on its existing refresh and closes tabs of removed members after a short grace. Paused workers keep their tabs. A worker running in its own terminal ends itself when removed.

## [0.26.257] - 2026-10-16

- The channel no longer waits for a running file-path search when it counts completion candidates; the count is published as soon as the path list changes.

## [0.26.256] - 2026-10-16

- Auto-optimize removes idle workers on its own again: a restart no longer makes every worker look new, acknowledged-but-unanswered asks expire after 24 h, and an abandoned iteration (no moves, all items stale) no longer blocks it.
- Removing a member from a closed work round no longer fails the cleanup; an open round left without a turn order is marked blocked for the master to re-plan.
- Collector: saving an agent's status no longer holds the global lock during the database write, so one slow write cannot stall every other request.
- Slow channel sends log where the time goes (handoff, editor, receipts, updates, canvas, transcript, panes), only while a send is pending.

## [0.26.255] - 2026-10-16

- Canvas: clicking into a plain paragraph edits just that paragraph in place; headings, tables, animations and other paragraphs stay rendered and do not move. A source longer than the paragraph's rows scrolls inside it. Lists, tables and animation blocks still use the existing editor.
- Masters keep a private communication profile for the person they work with (`tldrq person --for <id> me|note`), taught once by the first-contact cue; communication traits only, 2 KB, stored outside the repo.

## [0.26.254] - 2026-10-15

- Channel redraws no longer re-read the memory file for every human message: a thread with 80 human messages took about 50 ms and 89 MB per frame, and the name lookup is now cached until the file changes. This is a likely main cause of slow typing in busy channels.
- The web Channel shows each person's name instead of "human" (falls back to "human" when the name is unknown).
- `tldrq person me` shows your private communication profile, and `--forget` deletes it. It is stored only on your machine, never in the repo; agents record observations with `tldrq person note`.
- A worker that leaves retries its leave call for up to ~18 s when the collector is overloaded, instead of lingering in the roster for 5 minutes; a final failure is logged once.

## [0.26.253] - 2026-10-15

- Vision claim checks require an artifact reference for VERIFIED and reject invalid supersession. Missing state/caveat and stale claims are flagged only when read; unresolved blockers and history remain. Message bodies are unchanged, and an artifact reference is not independent proof. Cached views refresh expiry flags only on a new revision or an explicit read.

## [0.26.252] - 2026-10-15

- Workers added from the Team UI only get names that survive a restart; previously a 9-letter generated name was silently dropped on Reopen. A member skipped on restore is now reported with its name and reason.
- UI diagnostics record key-to-screen latency buckets and redraw causes alongside SIGUSR2 profiles, without recording typed text.
- German, Spanish and French spelling lists gain the common word forms that were missing (German had about half of them missing).

## [0.26.251] - 2026-10-15

- Reacting to a message flashes it (or the hovered row) in the reaction's color for a third of a second, starting on the keypress; a reaction that fails to land flashes red with the error.
- Team members picker gains Clear and Set model; each worker's own result is shown as returned, never a made-up "changed".
- Russian spelling: about 1,000 common word forms added (было, идеально, неплохо, исправляются), ё and е match, and "не плохо" becomes "неплохо".
- Wide thread panes reuse unchanged rows on redraw, cutting allocations while typing.
- Clear results show only the worker's reply text, not the internal message envelope.
- Human rituals: outside-world claims need a source someone opened, and every debate names a rotating skeptic who checks claims before the summary reaches the human.

## [0.26.249] - 2026-10-15

- Channel views stop the fast redraw loop for hidden or stale worker status text; visible status text still scrolls.
- After a restart, a worker shows busy only when it has assigned work or a visible spinner, not because it printed startup output.
- Reopen keeps removed workers removed; a worker added on purpose comes back with its model and start settings; look-alike names stay distinct.
- Masters can clear workers through `team_control` (action `clear`); each worker's own reply comes back as the result: cleared and primed, refused with a reason, or failed.
- Slow Team sends (over 1 s) log their phase timings and shared database waits; fast sends stay quiet.

## [0.26.248] - 2026-10-15

- Canvas: clicking in text below an animation block or inside a wrapped table puts the cursor where you clicked; typing no longer starts at the left edge.
- Canvas: text uses the full canvas width and wraps the same way in view and edit mode, so nothing jumps when you start editing.

## [0.26.247] - 2026-10-15

- Auto-optimize now finds idle workers: Channel broadcasts and old unanswered asks no longer count as activity.
- Auto-optimize and Clear context show which workers are eligible and why before anything is applied; the dialogs wrap long text instead of cutting it off.
- Clear context skips workers that are busy right now, re-sends the bootstrap once if the worker did not take it, and reports per worker: cleared, primed or failed.
- The bootstrap after a clear is built in one place from the worker's SkillPaqs and its roster role.
- Masters can set a worker's role or model and add workers through `team_control` (actions `set` and `add`); a model change is sent to Claude Code and Codex workers and refused with a reason for others.

## [0.26.246] - 2026-10-15

- Rebuild for a SkillPaq module update; no tldrq changes.

## [0.26.245] - 2026-10-14

- Word highlight (hover and unsent draft) is now black text on yellow in every theme, so matches are easy to see.

## [0.26.244] - 2026-10-14

- Channel views use less CPU on a busy Team: repeated readiness check-ins no longer reload the iteration view (about 3.7x cheaper per poll); real budget changes, lease deadlines and roster or profile edits still refresh it.

## [0.26.243] - 2026-10-14

- README demo videos re-recorded on the current UI (main tour, threads, canvas). No app changes.

## [0.26.242] - 2026-10-14

- One voice in the human channel: a plain message from you wakes only the leading master instead of mentioning every Team member; an explicit @name still reaches that agent.
- Less clutter from agents: built-in rules now ask for one line plus an artifact path instead of evidence walls, the first failing test line instead of full output, and a reaction or silence instead of "noted" posts.
- Channel views reuse unchanged iteration data instead of reloading it for every row (lookup about 7x faster), refreshing within a second when anything changes.
- Only the elected leading master of a real Team creates the workspace Status canvas; test and scratch accounts no longer leave canvases in the repo.

## [0.26.241] - 2026-10-14

- Spelling: two swapped letters in a short word are fixed too (elft → left, lfet → left); a word that is already known, or has two possible swaps, is left alone.
- Naming people: when someone new writes, the master asks "Call you <name>?" with a guess from git user.name, git user.email, the OS account's full name or the login email, the same on Windows, macOS and Linux. Nothing is saved until confirmed, and the computer name is never used.

## [0.26.240] - 2026-10-14

- Privacy: agents keep only a person's display name in shared workspace memory. Language, pronouns, tone, working hours and other preferences go to private per-developer memory (`--scope personal`), which is never in git.

## [0.26.239] - 2026-10-14

- Agents follow everyday communication norms: a new built-in `enmaq/human-rituals` SkillPaq (18 one-line goals such as: close the loop in the thread where you were asked, answer first and short, an ETA is a promise, stay calm with anger, remember names and preferences). A short essence of it is in every agent's setup; `quick-status` defers to it.
- Humans are named instead of "human": a message you send carries your tldrq login, and channel and thread views show your saved name. Unknown people and guests look exactly as before. The master asks a new person's name once per workspace.

## [0.26.238] - 2026-10-14

- The collector no longer slows down under many open channel views: the channel list is read with a few bulk queries instead of several per channel (about 6x faster at 100 channels), so channel replies and sends stop timing out.
- A channel send that times out and is retried no longer posts twice. An unchanged resend reuses the same message id; an edited one gets a new id.
- The workspace token total (⇅) no longer resets with a new build. It lives in one shared, locked `workspace-usage.json`, and the old per-build files are imported once. New usage is counted exactly; imported history is a measured sum of the stored files.
- An open canvas fills the pane down to the last row; the channel composer no longer shows beneath it, and typing goes to the visible thread draft.
- Canvas and thread headers read like a browser: the title on the first row with its controls, the full address on the second.
- The new-canvas title prompt stays in place while you type. A deleted canvas can be restored for 24 hours, then it is removed for good (its number is never reused).
- The left channel pane no longer jumps when a refresh times out.
- Spelling: German and French word lists added, Russian grows to 55k forms and Spanish to 45k (machine-generated; lists under 100k words make only safe fixes).
- The Team KPI recognises Claude Code's background-agents panel as busy instead of reporting a blocking dialog.
- (0.26.237 also shows a fixed 🇺🇸 next to tldrq instead of `??`.)

## [0.26.237] - 2026-10-14

- Spelling help now checks Russian and Spanish, with German and French to follow. Words in any script are checked, Cyrillic and accented letters included. Missing accents are restored (francais → français), and `prose.languages` picks the languages (default en, ru, es, de, fr). The new word lists are machine-generated (Russian 38k forms, Spanish 25k), so while a list is under 100k words only safe fixes are made: accents, a doubled letter, two swapped letters. A correct word that is missing from the list is never changed, and `[+]` adds it to your dictionary.
- Channel views no longer reload all presence and Team data on every worker heartbeat, and the channel list reads the roster once instead of once per row, cutting idle CPU.
- The workspace picker lists recently opened workspaces first and shows when each was last opened. New workspace stays at the top.
- The bottom tab strip uses a single dot between every tab again (`·C1·M1·M2·W1·`).

## [0.26.236] - 2026-10-14

- Animated canvases are cheaper again: unchanged text and table rows keep their trimmed, padded form between frames (bounded per page), so a frame now takes about 1.3 ms and 3 MB instead of 3.5 ms and 13 MB.

## [0.26.235] - 2026-10-14

- Canvases with an MDGL animation no longer burn CPU: text, tables and page geometry are laid out once and reused while the animation plays, instead of on every frame (about 3x less work per frame, and none once the animation has settled).
- On Linux, a hung collector now recovers by itself. When a shell auto-starts the collector and finds a verified tldrq collector that has failed its health checks for 15 seconds, it saves a SIGQUIT goroutine dump in `collector.log` and takes over. Processes it cannot verify, or that do not exit, are left alone with an error and never force-killed.

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

- An open canvas next to a thread fills the pane to the last row; the channel composer underneath is gone, and typing after leaving canvas edit lands in the visible thread draft.
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
