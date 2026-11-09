# Residual Characters of Odd-Degree Fermat Fourfolds

[![verify](https://github.com/Li-Hongmin/fermat-fourfold-residual-characters/actions/workflows/verify.yml/badge.svg)](https://github.com/Li-Hongmin/fermat-fourfold-residual-characters/actions/workflows/verify.yml) [![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.24054302-blue)](https://doi.org/10.5281/zenodo.24054302)

**Hongmin Li** (Institute of Science Tokyo; The University of Tokyo) · ORCID [0000-0003-0228-0600](https://orcid.org/0000-0003-0228-0600)

Main result of the manuscript: for odd-degree Fermat fourfolds, the residual Hodge characters (those not covered by surface contractions or Aoki's exact 5-standard tuples) are at every odd degree exactly the inflations of six explicit seeds in degrees 33, 39, 45 and 105; the proof is uniform in the degree, and the finite computations here are independent checks. The earlier Lean certificates cited in the paper are at [Li-Hongmin/hodge-odd-fermat-fourfolds](https://github.com/Li-Hongmin/hodge-odd-fermat-fourfolds/tree/649a3ce).

- Manuscript on rStation: <https://rstation.ai/problems/hodge_conjecture/papers/104/v4> (version 4)
- Archived on Zenodo: concept DOI [10.5281/zenodo.24054302](https://doi.org/10.5281/zenodo.24054302) (all versions); this repository mirrors version 4, DOI [10.5281/zenodo.24054303](https://doi.org/10.5281/zenodo.24054303)

## Contents

- `paper/paper.md`, `paper/fermat-fourfold-residual-characters.pdf` — the manuscript (version 4).
- `verification/` — the supplement of that version, unpacked unchanged; its own README describes each file.
- `.github/workflows/verify.yml` — reruns every check below on each push.

## What the programs check

| Check | Command (run inside `verification/`) |
|---|---|
| Proposition 4.1: exhaustive census through degree 105 (two independent enumerators) | `python -I calculations/bundles/xcheck-hodge-r5-2026-11-02/replay_base.py scratch/finite-base-replay` |
| Closure check | `python calculations/bundles/odd-fourfolds-le599-checked-closure/verify_closure.py` |
| Short semiprime classification | `python calculations/bundles/odd-fourfolds-le599-checked-closure/verify_short_semiprime_classification.py` |
| Two-prime depth | `python calculations/bundles/odd-fourfolds-le599-checked-closure/verify_two_prime_depth.py` |
| Depth extensions | `python -I calculations/bundles/odd-fourfolds-le599-checked-closure/verify_depth_extensions.py` |
| Positive finite reduction | `python calculations/bundles/odd-fourfolds-le599-checked-closure/verify_positive_finite_reduction.py` |
| Contraction block count at N=35 | `python calculations/bundles/xcheck-hodge-thm720-2026-10-29/block_E0.py 35` |
| R4 census check | `python calculations/bundles/xcheck-hodge-thm720-2026-10-29/verify_r4_census.py` |
| Uniform check at the eight degrees of Proposition 7.21 | `cd calculations/bundles/xc-uniform-check-2026-11-04 && python -I xc_uniform_check.py` |

The programs check the finite and exact computations used in the manuscript; the mathematical arguments are those written in the paper.

## Reproducing

```sh
cd verification
unzip -q calculations-bundles.zip
sha256sum -c CONTENTS.sha256      # or: shasum -a 256 -c CONTENTS.sha256
python -I calculations/bundles/xcheck-hodge-r5-2026-11-02/replay_base.py scratch/finite-base-replay
python calculations/bundles/odd-fourfolds-le599-checked-closure/verify_closure.py
python calculations/bundles/odd-fourfolds-le599-checked-closure/verify_short_semiprime_classification.py
python calculations/bundles/odd-fourfolds-le599-checked-closure/verify_two_prime_depth.py
python -I calculations/bundles/odd-fourfolds-le599-checked-closure/verify_depth_extensions.py
python calculations/bundles/odd-fourfolds-le599-checked-closure/verify_positive_finite_reduction.py
python calculations/bundles/xcheck-hodge-thm720-2026-10-29/block_E0.py 35
python calculations/bundles/xcheck-hodge-thm720-2026-10-29/verify_r4_census.py
cd calculations/bundles/xc-uniform-check-2026-11-04 && python -I xc_uniform_check.py
```

Requirements: Python 3.9+; the census replay needs a C compiler. Run the commands from a copy if you want to keep the recorded outputs untouched.

## Cite

```bibtex
@misc{li2026fermatfourfoldresidualch,
  author    = {Li, Hongmin},
  title     = {Residual Characters of Odd-Degree Fermat Fourfolds},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.24054302},
  url       = {https://doi.org/10.5281/zenodo.24054302}
}
```

## License

Manuscript and data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Code: MIT (see `LICENSE`).
