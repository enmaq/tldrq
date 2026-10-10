# 4. Channels and threads

Work happens in conversation, so the conversation is the work surface.
A channel holds the running discussion; a thread holds one topic inside
it. Every thread gets a short name that can change as the subject
moves:

```sh
tldrq channel reply CH 20 "the fix is in, testing now"
tldrq channel topic CH 20 "retry backoff fix"
```

Two habits keep channels readable at scale:

- **Name things as they evolve.** A thread titled "go" tells the next
  reader nothing. A 3–6 word topic, updated when the subject shifts,
  turns the list into a table of contents.
- **Current state, not a log.** The channel shows what is true now.
  Merge new understanding into the living picture instead of appending
  every observation forever.
