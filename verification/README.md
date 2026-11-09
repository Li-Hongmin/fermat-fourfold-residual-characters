# Supplement S1: Residual Characters of Odd-Degree Fermat Fourfolds

This supplement contains the source and complete finite data cited in the
unpublished manuscript dated 4 November 2026. It requires Python 3.9 or
later, a C compiler and the Python standard library. The replay of the census
through degree 105 uses one CPU and only small tables; it usually takes a
few seconds. No repository, external data service or remote account is
needed. `CONTENTS.sha256` records each enclosed file's SHA-256.

## Exhaustive finite census through degree 105: Proposition 4.1

From the extracted archive root, run:

```sh
python3 -I calculations/bundles/xcheck-hodge-r5-2026-11-02/replay_base.py \
    scratch/finite-base-replay
```

The output directory must be new. `CC` and `CFLAGS` select the compiler
and flags; the default is `cc -O2`. On macOS, if the local SDK requires it,
set `CFLAGS='-O2 -isysroot /path/to/MacOSX.sdk'` before the command.

The driver compiles two independent enumerators and runs both for all 52
odd degrees 3,...,105, without using a conductor cutoff to skip any degree.
The divisor-normalized direct enumerator prints every Hodge candidate;
Python checks each at every unit, rejects inverse pairs and classifies
the canonical orbits with all ten surface splits and all admissible
5-standard multisets. The three-plus-three C implementation uses its own
enumeration, canonicalization and predicates. Every canonical pair-free
orbit and its category must agree, in addition to the category counts and
residual sets. The seed list is compared only after enumeration.

Expected totals: 57 pair-free orbits, partitioned into 15 exact-standard,
35 other surface contractions and seven residuals. Six residuals are
primitive, in degrees 33,39,39,45,105,105; the seventh is the inflation at
99 of the degree-33 seed. The complete retained run is
`calculations/bundles/xcheck-hodge-r5-2026-11-02/results/r8-20261102/`.
It includes all 69,548 direct candidate rows, all three-plus-three orbit
rows, compiler diagnostics, environment and per-degree classifications.
A compiler/enumerator failure, missing summary or comparison failure exits
nonzero. Neither compiled executable nor an archived answer is needed.

The direct `enum6.c` and `classify.py` are the unchanged independent review
implementation supplied with the project. `hs_enum3.c` is the separately
written three-plus-three review implementation; R8 adds only optional
orbit output. `replay_base.py` joins their independent results. These
implementations are not taken from Jumagulov's code. The seed algebraicity
presentations remain credited to Jumagulov in the manuscript.

## Other finite checks

The following commands check the retained arithmetic and proof calibrations;
they do not rerun the larger exhaustive censuses:

```sh
python3 calculations/bundles/odd-fourfolds-le599-checked-closure/verify_closure.py
python3 calculations/bundles/odd-fourfolds-le599-checked-closure/verify_short_semiprime_classification.py
python3 calculations/bundles/odd-fourfolds-le599-checked-closure/verify_two_prime_depth.py
python3 -I calculations/bundles/odd-fourfolds-le599-checked-closure/verify_depth_extensions.py
python3 calculations/bundles/odd-fourfolds-le599-checked-closure/verify_positive_finite_reduction.py
python3 calculations/bundles/xcheck-hodge-thm720-2026-10-29/block_E0.py 35
python3 calculations/bundles/xcheck-hodge-thm720-2026-10-29/verify_r4_census.py
```

The first bundle contains the original 140-degree primitive census through
599, its complete `primitive-census.txt`, calibration scripts and outputs.
The second review bundle additionally retains the original census through 105 and
the two individual calibrations at 3465 and 3675. They do not extend a
continuous census beyond 2001. The explicit contraction check gives 190
quadruple blocks, 190 sextuple blocks and four invariant blocks at N=13;
these are potential counts, not orbit counts.

The extension bundle `quota-queue-r3-independent-enum-2026-10-29` contains
the complete original and extension outputs, C source and direct checker.
To check its retained extension output without rerunning enumeration:

```sh
cd calculations/bundles/quota-queue-r3-independent-enum-2026-10-29
python3 - <<'PY'
from pathlib import Path
import extend_residual_census as extension
import run_independent_census as checker
extra = [m for m in range(601, 2002, 2) if m % 3 == 0
         and (extension.prime_support(m) == [3, 5]
              or len(extension.prime_support(m)) >= 3)]
checker.DEGREES = sorted(set(checker.DEGREES + extra))
checker.verify(Path('extension-output.txt').read_text())
PY
```

Expected extension totals are 156 degrees, 966 nonpair orbits and 90
residuals, including 103 selected degrees above 599. To re-enumerate that
larger calculation, run `python3 extend_residual_census.py` in the same
directory on a suitable compute host. The original <=599 C census can
likewise be rebuilt from `primitive_residual.c`; the manuscript Appendix
specifies its degrees and command. These longer runs are supplemental
observations. Theorem 7.20 and Theorem A use neither these runs nor the
exhaustive census through 105.

## Mathematical scope

The scripts verify exact finite arithmetic. The analytic proofs in Section 7
provide the unrestricted conductor reduction. Classical geometric inputs
remain cited in the manuscript, and no script proves those theorems or the
general Hodge conjecture. The supplement contains no proof-assistant
formalization and makes no assertion of public deposition or journal acceptance.

## Independent large-degree check (observations, not premises)

`calculations/bundles/r9-large-degree-mitm-2026-11-04/` holds a third,
separately written enumerator (`mitm6.c`, `classify_r9.py`), its local
replay of the 52-degree census through 105, and the complete raw output of a batch run
at m = 1155, 1365, 1785, 1995, 2145, 2415, 2625, 2835, 3003, 3315.
Its `README.md` gives the commands; `compare_prior.py` compares the
results with copies of two earlier runs kept in `prior-runs/`. Degrees
above about 1500 need minutes and several GB of memory each.

## Census at the eight degrees of Proposition 7.21 (checks, not premises)

`calculations/bundles/r10-minimal-base-2026-11-04/` holds `naive6.c`, which
loops over every sorted sextuple with sum 3m at m = 3, 5, 15, 21, 33, 39, 45,
105 without orbit or divisor normalization, its classifier and the raw
output of one batch run (`README.md`, `SHA256SUMS.txt`).

`calculations/bundles/xc-uniform-check-2026-11-04/xc_uniform_check.py` is a
separately written Python check (`python3 -I xc_uniform_check.py`, about two
minutes; reference output `xc_uniform_check.out.json`). It reproduces the 28
pair-free orbits at these eight degrees and lists the finite configurations
named in the case analysis of Sections 7.1, 7.5 and 7.8. Theorem A does not
use either bundle.

Note: the 431 calculation files (seven bundles) are packed in calculations-bundles.zip (unzip to restore calculations/bundles/); its SHA-256 is appended to CONTENTS.sha256.

`CONTENTS.sha256` is authoritative for every file in this supplement. The historical manifest `calculations/bundles/xcheck-hodge-thm720-2026-10-29/results/r4-20261030/SHA256SUMS.txt` is retained unchanged from the R4 run: it also lists two launcher logs that are not included, and its `../../hs_enum3.c` entry predates the R8 optional-output line described in the manuscript Appendix.
