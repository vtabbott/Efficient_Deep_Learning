# Efficient Deep Learning
We make a distinction between *functionality* and *efficiency*. Functionality research manipulates the mathematical functions models implement (mappings from input to output), and hence the functionality they provide. Efficiency focuses on implementing the same (or very similar) function but using less resources.

We provide a spoiler for each linked paper summarising the *results* of the efficiency gains. Details regarding *how* this is achieved are left for the relevant papers.

---
## Transformers

### Optimized Kernels
<details> 
  <summary><a href="https://arxiv.org/abs/2205.14135">FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness</a></summary>
   "FlashAttention trains Transformers faster than existing baselines: 15% end-to-end wall-clock speedup on BERT-large (seq. length 512) compared to the MLPerf 1.1 training speed record, 3× speedup on GPT-2 (seq. length 1K), and 2.4× speedup on long-range arena (seq. length 1K-4K)."
</details>
<details> 
  <summary><a href="https://arxiv.org/abs/2307.08691">FlashAttention-2: Faster Attention with Better Parallelism and Work Partitioning</a></summary>
   "These yield around 2× speedup compared to FlashAttention, reaching 50-73\% of the theoretical maximum FLOPs/s on A100 and getting close to the efficiency of GEMM operations. We empirically validate that when used end-to-end to train GPT-style models, FlashAttention-2 reaches training speed of up to 225 TFLOPs/s per A100 GPU (72\% model FLOPs utilization)."
</details>
<details> 
  <summary><a href="https://arxiv.org/abs/2407.08608">FlashAttention-3: Fast and Accurate Attention with Asynchrony and Low-precision</a></summary>
   "FlashAttention-2 [achieves] only 35% utilization on the H100 GPU. [...] FlashAttention-3, achieves speedup on H100 GPUs by 1.5-2.0× with FP16 reaching up to 740 TFLOPs/s (75% utilization), and with FP8 reaching close to 1.2 PFLOPs/s. We validate that FP8 FlashAttention-3 achieves 2.6× lower numerical error than a baseline FP8 attention."
</details>

### PEFT Methods
<details> 
  <summary><a href="https://arxiv.org/abs/2106.09685">LoRA: Low-Rank Adaptation of Large Language Models</a></summary>

   * Freeze most model parameters, utilize low-rank decomposed matrices for adapters

   * Around 2x fast than full-parameter training

   * Memory efficient due to saving in Adam's first/second moments

   * Save disk space for storing model weights, particularly good for customization scenarios
</details>
<details> 
  <summary><a href="https://arxiv.org/abs/2305.14314">QLoRA: Efficient Finetuning of Quantized LLMs</a></summary>

   * Quantize the model weights during training, further save memory consumption
</details>
<details> 
  <summary><a href="https://arxiv.org/abs/2403.17919">LISA: Layerwise Importance Sampling for Memory-Efficient Large Language Model Fine-Tuning</a></summary>

   * Sample activated layers during training

   * Around 1.5x faster than LoRA

   * Even better than full-parameter training in instruction following tasks
</details>


### Model Architecture Modifications
<details> 
  <summary><a href="https://arxiv.org/abs/2305.13245">GQA: Training Generalized Multi-Query Transformer Models from Multi-Head Checkpoints</a></summary>

   * We reduce the number of heads for K and V by a factor of $g$, repeating them to match the number of query/output heads, $h$.

   * With $g = 8$, we get strong performance and minimal inference loss. This reduces K, V parameter count and generation compute cost by a factor of 8.

</details>
