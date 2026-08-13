# Release checklist

## Mathematical proof-artifact completeness

- [x] Include `n8m8_pos.bin`, `n8m8_hard.bin`, `cps8_all.bin`, and
  `cps8_fail.bin`.
- [x] Audit all 9,105,190 square kernels for sortedness, uniqueness,
  antichainness, full rank, and positive duality.
- [x] Verify that the 1,049,187 hard records are exactly the disjoint union of
  accepted certificates and failure records.
- [x] Verify that the failure stream contains zero records.
- [x] Replay every `m=8` certificate with signed-rational arithmetic.
- [x] Replay every `m=8` certificate independently with GMP rationals.
- [x] Require agreement on all proof-relevant aggregate fields and positive
  exact minima.
- [x] Retain the hardened `m=7` dual-domain checks, proposal non-identity rule,
  fixed smoke wrapper, and hash-bound resume implementation.
- [x] Regenerate the top-level `SHA256SUMS` after adding proof data and release
  documentation.
- [x] Run the referee-scale `scripts/quick_verify.sh` on the completed data.

## Reproduction and archival metadata

- [x] Record the completion environment, wall time, peak memory, file sizes,
  hashes, and exact aggregate results.
- [x] Remove personal/contact/account metadata and normalize container-local
  paths retained in historical logs.
- [x] Keep every ordinary-Git file below GitHub's 100 MiB hard limit.
- [ ] Optional: obtain an independent clean-machine full regeneration on
  separate hardware. This release does not claim one, and it is not needed to
  replay the deposited exact proof.
- [x] License the complete artifact under Apache-2.0 and add `LICENSE`.
- [ ] Add final author metadata and `CITATION.cff`.
- [ ] Tag the immutable public release referenced by the manuscript.
