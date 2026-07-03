# EdgeVLM

Code and measurements for EdgeVLM, a lightweight vision-language model built for deployment on edge and mobile hardware. This repo contains the notebook used to run the real components of the pipeline and collect the numbers reported in the paper.

Paper: EdgeVLM, ICWR 2026 (IEEE Xplore ID: 11513320), co-authored with Leila Safari (University of Zanjan).

## What's actually in here

The pipeline has three parts:

- **Vision encoder** — MobileViTv2, pretrained, loaded through `timm`.
- **Language model** — TinyLLaMA-1.1B-Chat as the student model.
- **Fusion adapter** — a small bottleneck adapter (down-projection → GELU → up-projection) that maps vision features into the LLM's hidden space. This is the actual contribution of the paper; everything else is off-the-shelf.

The notebook (`EdgeVLM_real_measurements.ipynb`) runs all of this end to end on a Colab GPU (T4 is enough) and measures:

- FP16 model size (vision + student + adapter)
- End-to-end latency (vision encode → fusion → one LM forward pass), averaged over 30 runs
- VQA accuracy on a small labelled subset (100 samples from VQAv2, using BLIP-VQA as the reference model)
- INT4 quantized size of the student model (via bitsandbytes / nf4)
- A short training run of the adapter on CIFAR-10 to get real loss/accuracy curves, and a size-reduction chart across compression stages (base → QLoRA → distillation → QAT)

All numbers are measured directly, not simulated — the notebook prints them at the end in a summary block so they can be copied straight into the tables.

## Running it

Open the notebook in Colab (GPU runtime), then run the cells top to bottom:

```
pip install torch torchvision transformers timm pillow datasets accelerate bitsandbytes
```

A free T4 instance is enough for the sizes used here. The VQA and training cells will download a small dataset slice on first run.

## Notes

- The latency numbers are GPU dev-time measurements, not on-device mobile numbers — this is noted in the notebook itself.
- The VQA accuracy uses BLIP-VQA as a reference model on a 100-sample subset, not the trained EdgeVLM head; swap in your own head once trained if you want pipeline-specific accuracy.
- Figures are saved at 300–600 dpi as JPGs, ready to drop into the paper.

## Citation

```
@inproceedings{razavi2026edgevlm,
  title={EdgeVLM},
  author={Razavi, Firouzeh and Safari, Leila},
  booktitle={ICWR 2026},
  year={2026}
}
```
