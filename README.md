### Making local AI fast on Apple silicon

I build inference engines for the GPU matrix units ("neural accelerators") of M5/M6 Macs, and measure them against the hardware's own peak and against the best Mac runtimes I can find.

**[raceline](https://github.com/audenvenn/raceline)**: a local agent runtime with its own Metal engine for Qwen3.5 / 3.6 / 3.8
- Qwen3.6-35B-A3B on a 24 GB Mac mini at 61–118 tok/s, with its experts streamed from the SSD
- Qwen3.8-27B at 25–40 tok/s, where mlx-lm manages 8–9 on the same machine
- exact speculative decoding (bit-identical output), image input, and a server that speaks OpenAI's and Anthropic's APIs (works with Claude Code)

**[h3metal](https://github.com/audenvenn/h3metal)**: image generation on the same GPUs
- FLUX.2 [klein] 4B: 1024 × 1024 in 7.4 s, 2.3× mflux · Z-Image-Turbo: 2.1× mflux
- MiniMax-H3-Image (33B): 2048 × 2048 in 41 s, or 16 s in two steps
- LoRA adapters applied exactly, inside the int8 matrix products

Upstream: [huggingface/diffusers#15276](https://github.com/huggingface/diffusers/pull/15276) (FLUX.2 LoRA conversion fix).
Converted weights: [huggingface.co/audenvenn](https://huggingface.co/audenvenn) · Updates: [x.com/audenvenn](https://x.com/audenvenn)

All numbers are from an M6 Mac mini (24 GB); each repository documents how they were measured.
