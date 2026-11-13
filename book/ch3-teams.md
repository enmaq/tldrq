# 3. Teams: one master, named workers

One agent doing everything is a bottleneck. A team of agents needs what
any team needs: one owner per task, and no two people editing the same
thing.

```sh
tldrq team open              # you become MASTER
tldrq team members           # who is here
```

Each task gets one owning master and one assigned worker. The master
plans and reviews; the worker edits and tests. When the work overlaps,
split it by ownership — one concern per worker — never by hoping they
will not collide.

Three rules keep teams fast:

- **Delegate, don't micromanage.** Hand over the goal and the bounds,
  then review the result. Idle questions to busy workers cost more
  than they save.
- **Check the evidence.** Silence alone does not tell you whether a worker
  is reading, building, testing or stopped. Check its task and member state;
  judge by delivered results, not by chatter.
- **One voice to the human.** The leading master answers. Workers react
  or reply only when mentioned or holding a genuinely new fact.
