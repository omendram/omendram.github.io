---
layout: post
title: Multilingual Transfer in Automatic Summarization
subtitle: Using sequence-to-sequence architecture to perform summarization across multiple languages 
cover-img: 
thumbnail-img: 
share-img: /assets/img/path.jpg
tags: [deep learning, transformers, bert, aws, nlp]
---

The primary objective of this research was to evaluate a trained summarization model's performance over a multi-lingual dataset to generate summaries specifically  in other languages than English. Since the summarization training set is already an English to English mapping, it was established as a baseline to investigate the knowledge transfer across multiple languages(English, German and Dutch) during summary generation.

## Transformer Models
Recently in the field of machine translation and text reduction a neural network architecture called Transformer models are gaining popularity due to their significant advantages over the sequential neural network architectures. Transformer models are attention based models which are widely popular in Natural Language Processing field for machine translation and text generation tasks. They are designed similarly to sequence-to-sequence models, as in they are provided with a sequence and are trained to generate another sequence which could be either a translated text or generated summary. The transformer models shows that it is possible to move away from using recurrent neural networks within the encoder and decoder stacks by using attention mechanisms instead. This makes room for parallelization during translation and training processes, making these models to be considerably more efficient and capable than the RNNs / LSTMs.

Like most sequence transduction models, transformers also follow suit with having an encoder-decode type architecture. Figure below represents the transformer architecture. The transformer models consist of $N=6$  stacked identical layers of encoders and decoders The input text sequences to the encoders are turned into vector representations by using an embedding algorithm. However, since transformer models do not process inputs sequentially, there needs to be a way to contextualize the order of the words in sequences. This is solved by adding Positional Encoding to the input embeddings at the bottom of encoder and decoders each, so it is imperative for positional encoding to have the same size as the input embeddings, so they can be added before to being supplied to the encoder/decoder stack.

![Transformer](https://github.com/omendram/omendram.github.io/blob/master/assets/img/transformer.png | width=150)

## Architecture
### Input Vectors

### Cascaded System
The cascaded system is when the translation and summarization models are stacked against each other to produce multilingual summaries of text inputs.
![Transformer](https://github.com/omendram/omendram.github.io/raw/master/assets/img/cascaded.png | width=150)

### MultiTask Learning
![Transformer](https://github.com/omendram/omendram.github.io/raw/master/assets/img/multitask.png | width=150)


