### Local AI on Apple silicon, measured honestly

I build and benchmark local inference on Macs: GPU kernels where they help, and end-to-end measurements of what actually gets work done.

**[solvetime](https://github.com/audenvenn/solvetime)**: how long a Mac takes to finish real coding tasks with a local model. Each engine is scored on tasks solved and time to solution, not tokens per second, and every trajectory is published.
- First result: on a 24 GB Mac, the Qwen3.6-35B builds that fit are ~2-bit, and they drop the opening `<tool_call>` tag. We reported it, and kapitsa fixed its parser the same day (19/32 → 28/32 tasks solved).

**[h3metal](https://github.com/audenvenn/h3metal)**: image generation on the M5/M6 GPU matrix units
- about 2.3x faster than Draw Things' CLI per denoising step (FLUX.2 [klein] 4B, Z-Image-Turbo, same Mac)
- MiniMax-H3-Image (33B): 2048 × 2048 in 16 s with two steps on a 24 GB Mac mini

**[raceline](https://github.com/audenvenn/raceline)** (research, maintenance mode): a local agent runtime with its own Metal engine. Its findings feed solvetime: MTP drafting, experts streamed from the SSD, and a GPU that slows down while it waits for the CPU.

Upstream: [diffusers#15276](https://github.com/huggingface/diffusers/pull/15276) (FLUX.2 LoRA fix) · [kapitsa#1277](https://github.com/nace-ai/kapitsa/issues/1277) (fixed in #1279) · [MTPLX#695](https://github.com/youssofal/MTPLX/issues/695)

Converted weights: [huggingface.co/audenvenn](https://huggingface.co/audenvenn) · Updates: [x.com/audenvenn](https://x.com/audenvenn) · [bsky.app/profile/audenvenn.bsky.social](https://bsky.app/profile/audenvenn.bsky.social)

All numbers come from one M6 Mac mini (24 GB) unless stated; each repository documents how they were measured.
