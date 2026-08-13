# Artifact status

## Release status

The artifact is **data-complete and proof-replayable**. All source-level release
issues have been corrected, all four square-stage files are present, and the
full 9,105,190-kernel `m=8` computation passed kernel audit, hard-record coverage,
zero-failure checking, and independent exact replay.

| Component | Status |
|---|---|
| six-voter predecessor | complete |
| seven-voter predecessor | complete |
| eight voters, `m=4` | complete; zero hard cells |
| eight voters, `m=5` | complete; zero hard cells |
| eight voters, `m=6` | complete; 163 fixed and 5 adaptive certificates |
| eight voters, `m=7` | complete; 36,119 fixed and 9 adaptive certificates |
| eight voters, `m=8` kernels | complete; 9,105,190, independently audited |
| eight voters, `m=8` hard cells | complete; 1,049,187 |
| eight voters, `m=8` certificates | complete; 1,049,177 fixed and 10 adaptive |
| eight voters, `m=8` failures | zero records; canonical eight-byte header |
| signed-rational/GMP replay | PASS; proof-relevant aggregates agree |

The authoritative `m=8` kernel and hard-cell hashes match their audited values.
The accepted certificate stream differs bytewise from the audited proposal, but
complete coverage and both exact replays pass. Exact minima are `1/1008` for
the singleton/adaptive-sum margin and `1/11` for the price margin. The precise
hash/counter alignment is recorded in `CERTIFICATE_STREAM_PORTABILITY.md`.

## Release-review corrections retained

1. The `m=7` exact checker independently rejects rank-deficient kernels and
   affine dual domains without a strictly positive point.
2. Floating-point proposal identity is not trusted; exact validity and complete
   record coverage determine acceptance.
3. The no-argument smoke wrapper obeys the new-destination contract.
4. Resume artifacts are SHA-256-bound to tools, inputs, parameters, and outputs.
5. Both square exact backends validate the unique positive dual and structural
   metadata before margin checks.

Historical release-blocker logs remain under `logs/n8/` as an audit trail. The
completion evidence is in `logs/n8/full_m8_regeneration_console.log` and
`summaries/n8/m8_full_completion.json`.
