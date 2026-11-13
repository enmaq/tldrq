# 2. Evidence, not guesses

An agent should never start from a blank page. Before it reads a single
file, it gets one composed packet for the task:

```sh
tldrq blueprint "retry handling"
```

The packet can include ranked symbols, reverse-call impact, indexed tests
and suggested verification commands. Its hints say when an index or test
coverage is missing. It is capped small on purpose: enough to act, too
small to drown in.

Two principles make this work:

- **Facts live in the workspace, not in the model.** Whether a symbol
  exists, where a function starts and ends, which tests are present —
  those are properties of the repo. Asking a model to guess them adds
  cost and error. Read them directly.
- **Structure first, runtime second.** Most questions ("who calls this?",
  "what breaks if I change it?", "is this reachable?") are answered by
  static analysis. Those links describe possible calls, not proof that a
  branch ran. Exercise code for actual paths, timing, concurrency and real
  values.
