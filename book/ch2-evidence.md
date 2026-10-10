# 2. Evidence, not guesses

An agent should never start from a blank page. Before it reads a single
file, it gets one composed packet for the task:

```sh
tldrq blueprint "retry handling"
```

The packet holds ranked symbols, reverse-call impact, reachable tests,
and the exact commands to verify with. It is capped small on purpose:
enough to act, too small to drown in.

Two principles make this work:

- **Facts live in the workspace, not in the model.** Whether a symbol
  exists, where a function starts and ends, which tests are present —
  those are properties of the repo. Asking a model to guess them adds
  cost and error. Read them directly.
- **Structure first, runtime second.** Most questions ("who calls this?",
  "what breaks if I change it?", "is this reachable?") are answered by
  static analysis. Run code only for what static analysis cannot tell
  you: timing, concurrency, real values.
