# Byte Pair Encoding (BPE) Tokenizer — From Scratch (GPT-2 Style)

This repository contains a **from-scratch Python implementation of Byte Pair Encoding (BPE)** inspired by the GPT-2 tokenizer.
 It is designed for learning and educational purposes, with an emphasis on clarity, correctness, and extensibility.



## Features

The BPE tokenizer:

- operates at the **byte / character level**
- uses **subword merges**
- follows the **GPT-2 convention** of marking word boundaries with `Ġ`
- guarantees **no out-of-vocabulary (OOV) tokens**



## Why Byte Pair Encoding?

Word-level tokenization suffers from:

- exploding vocabulary size
- frequent out-of-vocabulary tokens
- poor generalization to rare or unseen words

Character-level tokenization avoids OOV issues but produces **very long sequences**.

BPE strikes a balance:

- common words become single tokens
- rare words decompose into known subwords
- vocabulary size stays manageable

This is why **all modern LLMs (GPT, LLaMA, Mistral, Qwen)** rely on BPE-style tokenizers.



## Quick Start

### Installation

```shell
git clone https://github.com/fudonglin/blog_code_repository.git
cd blog_code_repository/bpe
```



### Train the Tokenizer

```python
from bpe.byte_pair_encoding import BPETokenizer

corpus = "merchant merchandise commerce"

bpe = BPETokenizer()
bpe.train(
    text=corpus,
    vocab_size=300,
    allowed_special={"<eos>"}
)
```



### In-Vacabulary Example

```python
iv_test = "merchant merchandise commerce"
iv_tokens = bpe.encode(iv_test, allowed_special={"<eos>"})

print("")
print("========== In-Vocabulary Example ==========")
print("Input:", iv_test)
print("In Vocabulary Tokens:", iv_tokens)
print("In Vocabulary Decoded (skip <eos>):", bpe.decode(iv_tokens, skip_special={"<eos>"}))
```



### Out-of-Vacabulary Example

```python
oov_test = "mercurial"
oov_tokens = bpe.encode(oov_test, allowed_special={"<eos>"})

print("========== Out-of-Vocabulary Example ==========")
print("Input:", oov_test)
print("Tokens:", oov_tokens)
print("Decoded (skip <eos>):", bpe.decode(oov_tokens, skip_special={"<eos>"}))
```



## License

MIT License.
 Feel free to use, modify, and share.
