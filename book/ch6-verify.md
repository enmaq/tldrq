# 6. Verify before done

A change is done when the tests say so, not when the code looks right.
Every fix ships with a regression test that fails without the fix and
passes with it — written first, or the fix proves nothing.

```sh
go vet ./...
go test ./... -run TestRetryBackoff
```

Three habits make verification honest:

- **Run the project's own tests.** A throwaway script that passes is
  not evidence. The repo's test suite is the contract.
- **Test the edges, not just the path.** Empty input, missing files,
  restarts mid-operation. The happy path is where bugs hide least.
- **Check the discriminating case.** Before editing, predict one input
  whose output differs if your theory is right. Run it. If the result
  surprises you, replan — don't rationalize.
