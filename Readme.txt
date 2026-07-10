# EdgeVLM Reproducibility Code

This repository contains the reproducibility notebook and result files for the revised EdgeVLM manuscript.

## Contents

- `EdgeVLM_final_v2_with_baselines_and_gguf.ipynb`: main experimental notebook
- `dynamic_gating_ablation_results_FINAL_REG_REBUILT.csv`: final fixed-versus-dynamic gating ablation results
- `browser_cpu_benchmark.html`: CPU-only browser benchmark used for the Samsung Android prototype test

## Main Results

The final dynamic fusion ablation uses five random seeds and 500 NExT-QA samples.

| Fusion Strategy | Accuracy |
|---|---:|
| Fixed global alpha | 0.2320 |
| Regularized dynamic alpha(x) | 0.2720 |

The paired t-test gives p = 0.1132, so the improvement is reported as an improvement trend rather than a statistically significant gain.

## Important Note

The browser-based Samsung Android benchmark is a CPU-side prototype workload. It uses JavaScript CPU execution only and does not use WebGL, WebGPU, or WASM acceleration. This benchmark should not be interpreted as full native smartphone deployment of the complete EdgeVLM pipeline.

## Reproducibility

Large model weights and datasets are not included in this repository. Some notebook cells are optional and may require downloading public models or datasets.