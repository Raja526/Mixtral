# Mixtral offloading

This project implements efficient inference of [Mixtral-8x7B models](https://mistral.ai/news/mixtral-of-experts/).

## How does it work?

In summary, we achieve efficient inference of Mixtral-8x7B models through a combination of techniques:

* **Mixed quantization with HQQ**. We apply separate quantization schemes for attention layers and experts to fit the model into the combined GPU and CPU memory.
* **MoE offloading strategy**. Each expert per layer is offloaded separately and only brought pack to GPU when needed. We store active experts in a LRU cache to reduce GPU-RAM communication when computing activations for adjacent tokens.
