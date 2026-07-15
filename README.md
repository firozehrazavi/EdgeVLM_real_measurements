# EdgeVLM Reproducibility Code

This repository contains the experimental notebooks and result files used in the revised EdgeVLM manuscript.

## Contents

- `EdgeVLM_final.ipynb`: main training and evaluation notebook
- `EdgeVLM_real_measurements.ipynb`: CPU benchmark and real-measurement notebook
- `dynamic_gating_ablation_results.csv`: fixed-versus-dynamic temporal fusion results across five random seeds
- `browser_cpu_benchmark.html`: CPU-only browser benchmark used for the Samsung Android experiment

## Dynamic Fusion Results

The dynamic temporal fusion experiment was conducted using 500 NExT-QA samples across five random seeds.

| Fusion strategy | Mean accuracy |
|---|---:|
| Fixed global α | 0.2320 |
| Dynamic α(x) | 0.2720 |

The dynamic fusion model achieved a relative improvement of 17.24%.

The paired t-test produced `p = 0.1132`. Therefore, the result is reported as an improvement trend rather than a statistically significant gain.

## CPU Benchmark

Two component-level CPU benchmarks were conducted.

| Environment | Mean latency | P95 latency | Throughput |
|---|---:|---:|---:|
| Colab CPU | 3.24 ms | 4.69 ms | 309.05 samples/s |
| Samsung Android browser | 381.57 ± 8.36 ms | 398.74 ms | 2.62 samples/s |

The Samsung benchmark was repeated across three independent runs. Each run included 10 warm-up iterations and 100 timed iterations.

The browser implementation used JavaScript CPU execution without WebGL, WebGPU, or WebAssembly acceleration.

## Important Note

The Samsung Android experiment evaluates only the temporal-fusion component.

It should not be interpreted as native end-to-end deployment of the complete EdgeVLM pipeline.

Battery consumption, sustained memory usage, thermal behavior, and full native smartphone deployment were not evaluated.

## Reproducibility

Large model weights and datasets are not included in this repository.

Some notebook cells may require downloading public models or datasets before execution.

Random seeds and experiment settings are included in the notebooks and result files.
