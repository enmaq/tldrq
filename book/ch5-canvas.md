# 5. Canvas: the current picture

Some things are easier drawn than said. A canvas is a live picture of
the current state — a diagram, a plan, a sketch — that everyone in the
team can see and edit:

```sh
tldrq canvas new "retry flow"
tldrq canvas put 3 --text "client -> backoff -> server"
tldrq canvas show 3
```

A canvas is not a document. In a document you append; in a canvas you
**rewrite in place**. When the state changes, replace the part that
changed on the latest revision. Old sections are deleted, not
accumulated — otherwise the picture lies.

And when the picture unfolds over time — a flow, a pipeline, a state
change — animate it instead of drawing it static. Steps revealed in
sequence, tokens moving along arrows, carry meaning a still diagram
cannot.
