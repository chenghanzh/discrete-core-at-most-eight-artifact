# Eight-voter code-completion changelog

## Release-blocker correction pass

- Hardened `src/n8/exact_cps_fullsat_checker.cpp` so it independently rejects
  rank-deficient matrices and affine dual domains with no strictly positive
  point. Singleton/adaptive checks can no longer pass through an empty domain.
- Added the corresponding structural and exact-dual validation to both square
  `m=8` replay backends.
- Removed proposal-identity requirements. The available-data verifier, full
  verifier, and regeneration driver now use record coverage, zero failures, and
  exact replay as the mathematical acceptance rule. An audited certificate hash
  is reported but is not authoritative.
- Fixed `scripts/smoke_test_n8.sh` so its no-argument mode passes a nonexistent
  child destination to the regeneration driver.
- Replaced count-only resume reuse with SHA-256 provenance binding for key lists,
  scan chunks, `m=8` proposal chunks, and exact-replay logs. Legacy unbound
  chunks are discarded; incompatible chunk layouts are rejected.
- Added `scripts/test_n8_release_regressions.sh`, including deliberate
  rank-deficient, empty-positive-dual, mutated-key-list, and mutated-chunk cases.

## End-to-end driver

The original placeholder `scripts/regenerate_n8.sh` was replaced by a
C++/Python pipeline that:

- audits the binary ABI;
- directly enumerates `m=4` and `m=5`;
- independently obtains `m=5` by canonical augmentation;
- extends the positive-dual hierarchy through `m=8`;
- scans all residual budgets in contiguous chunks;
- merges hard records only after exact coverage and ordering checks;
- constructs and exactly replays `m=6`, `m=7`, and `m=8` certificates;
- compares signed-rational and GMP `m=8` results;
- verifies record bijection, zero failures, square-kernel structure, and expected
  census; and
- writes machine-readable summaries and a SHA-256 manifest.

## Binary safety

`src/n8/n8_binary_format.hpp` and `binary_format_selftest.cpp` define and audit
the fixed layouts. Former ABI padding is explicit zero reserved data. Readers
reject malformed headers, wrong lengths, trailing data, nonzero reserved fields,
duplicate records, and coverage mismatches.

## Compact exact data

The archive includes complete `m=4` and `m=5` lists and zero-hard-cell outputs,
plus existing `m=6` and `m=7` exact records. At `m=5`, direct and
augmentation-generated positive lists agree byte-for-byte.

## Verification entry points

- `scripts/smoke_test_n8.sh`: self-cleaning or explicit-output `m<=5` run.
- `scripts/test_n8_release_regressions.sh`: reported-blocker regressions.
- `scripts/verify_n8_available.sh`: compact `m=4,...,7` verification plus the
  exceptional `m=8` test.
- `scripts/verify_n8_adaptive_smoke.sh`: 48-record square-stage exact test.
- `scripts/verify_n8.sh`: complete deposited-data verification, including the full square stage.

## Full square-stage proof-data completion

- Regenerated the 9,105,190 canonical positive-dual `m=8` kernels and matched
  the audited SHA-256.
- Ran the complete floor-cell scan and reproduced 1,049,187 hard records with
  the audited SHA-256.
- Generated 1,049,177 fixed and 10 adaptive certificates with zero failures.
- Proved exact validity with both signed-rational and GMP checkers and required
  aggregate agreement.
- Deposited all four square-stage files, full completion summaries, logs, and a
  regenerated package manifest.

## Final data-complete release refinements

- Installed the square-stage enumerator optimization used by the production
  run: for `m=8`, the exact Cramer determinant test already proves full rank,
  so the redundant modular rank computation is skipped.  The resulting
  9,105,190-key file matches the audited hash exactly.
- Added `scripts/parallel_m8_exact_replay.py`.  The complete 64-byte
  certificate stream is partitioned into exact contiguous intervals, every
  interval is checked by both backends, and integer counters/rational minima are
  aggregated.  Dynamic scheduling uses all available cores while acceptance
  still requires complete interval coverage and identical backend aggregates.
- Added `docs/CERTIFICATE_STREAM_PORTABILITY.md` to record the exact-valid
  release certificate hash and the small, proof-neutral redistribution between
  open-floor and exact-LP subchecks.
