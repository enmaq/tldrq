# 1. Why agents need a map

An agent dropped into a new repo faces the same problem you do on day
one: where is everything?

Grep finds text but not structure. It returns lines, not the function
around them. No callers, no tests, no sense of what breaks if you touch
it.

A code graph answers those questions directly:

```sh
tldrq graph index --quiet
tldrq graph search retryattempts
# Use the node ID returned by search:
tldrq graph inspect NODE_ID
tldrq graph impact NODE_ID
```

Search finds the symbol and its node ID. Impact shows indexed caller
relationships and dependencies. Unresolved or missing edges still need
checking before an edit. If a result belongs to another namespace, pass the
returned namespace with `--namespace`.

The rule for every change: start from the task, pull one small bounded
packet of evidence — the symbols, their callers, the tests — and only
then edit. The agent decides what to change. The evidence and the tests
decide whether it was right.
