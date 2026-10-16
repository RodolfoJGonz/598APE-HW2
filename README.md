# Checking performance changes

Build and run the benchmark from a checkout with:

```bash
make -j
./genetic_benchmark diabetes
```

The benchmark prints an end-to-end runtime. Evolution is randomized, so run each version a few times and compare the median. Keep the machine, thread count, dataset, and build flags the same.

## Paper section commits

| Section | Commit |
| --- | --- |
| Baseline | `12cd475` |
| Compiler flags | `8a8011f` |
| Parallelism | `85e3edf` |
| Data structures | `b23d381` |
| Evaluation loop order and prediction-buffer reuse | `622b28b` |
| MSE work reduction | `0db46a9` |

## Compare the performance commits

For each feature, check out its commit, rebuild from scratch, and run each benchmark below. Repeat runs a few times and compare the median runtime. `git checkout -f` discards uncommitted changes, so save anything you need first.

```bash
## Baseline
git checkout -f 12cd475
make clean
make -j

## Compiler flags
git checkout -f 8a8011f
make clean
make -j

## Parallelism
git checkout -f 85e3edf
make clean
make -j

## Data structures
git checkout -f b23d381
make clean
make -j

## Evaluation loop order and prediction-buffer reuse
git checkout -f 622b28b
make clean
make -j

## MSE work reduction
git checkout -f 0db46a9
make clean
make -j
```

After each build, run the benchmark workloads:

```bash
./genetic_benchmark diabetes
./genetic_benchmark cancer
./genetic_benchmark housing
./genetic_benchmark silk-wave
./genetic_benchmark square-wave
```
