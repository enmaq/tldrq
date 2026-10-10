# 7. Release discipline

Ship small, ship green, ship often. Each release is one concern, fully
tested, tagged, and announced — never a bundle of half-finished work.

The cadence:

1. Run the full gate: unit tests, integration, build, vet.
2. Commit and push only the release's files.
3. Tag it, confirm the tag, announce what changed.
4. Restart to pick it up.

Two rules protect the rhythm:

- **Freeze before the gate.** No new edits land while the release is
  being verified. Anything unfinished waits for the next train.
- **Never break the tree.** The shared code compiles and passes vet at
  all times. A red tree blocks everyone, so fix it before anything
  else.
