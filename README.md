# MicroLM

MicroLM is a small language model project focused on building compact, efficient text generation systems from scratch and experimenting with lightweight transformer designs.

## What this repo contains
- Tiny language model experiments
- Tokenization and training pipeline code
- Compact transformer architecture implementations
- Small-scale inference and text generation tests
- Research ideas around efficient language modeling

## Goal
The goal of MicroLM is to explore how much useful language capability can be achieved with a very small model and a simple training setup.

## Current focus
- Small parameter-count transformer experiments
- Efficient training on limited hardware
- Better output quality from compact models
- Architecture ideas for low-cost local inference

## Planned work
- Improve training stability
- Better dataset mixing
- Stronger tokenizer setup
- Evaluation scripts
- Inference cleanup and reproducibility

## Status
In progress.
### Experiments
#### Experiments 1
Tried to keep params small, around half million and 1 million, Kept the token params small by compressing the sentence transformer embedding
to 64 or 128 and vocab size as just 4096, got some good enough text generation but not really good, dataset was small.

#### Experiments 2
Started to increase params, tried various size for embeddings, also used frozen 384 embedding directly, and then also tried to map it to higher
dimension. Tried with different vocab size, found about the 1:20 ratio. earlier i had this parameter to token ratio as 1:576 which was very wrong. 
Tried with different head and depth by increasing token embeddings to 512 and layers also to 32 not both together since param limit was 10-20 million. 
Attempted sft for conversation as second phase once story telling / text generation was good enough with consistency, it failed but got 
idea that i need to interleave the dataset not keep each category in different shard and not train them one by one, this was the main reason
even when i reached PPL 6 for text generation, when the shard for dataset on conversation starts it ruins everything and PPL reaches 40-200
In text generation I reached Loss around 1.7 and PPL 6 as well.


## Intermediate Conclusion
After all these experiments understood the parts of llm and how they work.
I need to maintain interleave dataset, keep the embedding around 256-512.
No. of Head is fine but need more Layers. in one exp i was able to reach 7 PPL with 128 token embedding and 32 layers total of 8.5 million param.
Might increase vocab size, interleave data, and keep the llm size around 10 million for the next experiments.

## Speed
This part is interesting, code is not clean but somehow with the int8 quant , custom K-V cache and onnx I was able to reach **8000 toks/sec**.

## Vision
MicroLM is an attempt to understand language modeling deeply by building smaller systems that are easier to train, inspect, and improve.
