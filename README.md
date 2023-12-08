# GPT-2 Implementation
## Reference : NANO_GPT GITHUB
## Details of all the tasks : [REPORT](https://docs.google.com/document/d/1GagBCirTLk43F-CXOxePy5YKvFI4BYs_cWWwGjaTw8M/edit?usp=sharing)
Data was loaded from OpenWebText of the nanoGPT github.

GPT-2 (124M ) training on OpenWebText:

<img src="https://github.com/AbhishekG-1plus/GPT-2_contlo/assets/77354191/d1b48fa8-1acd-4de8-a272-55f1592bef7d" width="400" height="300">

## Video Demonstration :

1. **Loading Dataset:**
   [Loading Dataset](https://photos.app.goo.gl/BPgqGmufbHSD5pS29)

2. **Training GPT-2(124M):**
   [Training GPT-2(124M)](./images/training_gpt2.png)

3. **Sample Prediction:**
   [Sample Prediction](./images/sample_prediction.png)

## GPT-2 (124M) Implementation

It is a rewrite of [minGPT](https://github.com/karpathy/minGPT). Currently the file `train__task3.py` reproduces GPT-2 (124M) on OpenWebText, running on a single 8XA100 40GB node in about 4 days of training. The code itself is plain and readable: `train_task3.py` is a ~300-line boilerplate training loop and `model_task1.py` a ~300-line GPT model definition, which can optionally load the GPT-2 weights from OpenAI.



## install

```
pip install torch numpy transformers datasets tiktoken wandb tqdm
```

Dependencies:

- [pytorch](https://pytorch.org) <3
- [numpy](https://numpy.org/install/) <3
-  `transformers` for huggingface transformers <3 (to load GPT-2 checkpoints)
-  `datasets` for huggingface datasets <3 (if you want to download + preprocess OpenWebText)
-  `tiktoken` for OpenAI's fast BPE code <3
-  `wandb` for optional logging <3
-  `tqdm` for progress bars <3

## quick start


```
$ python data/shakespeare_char/prepare.py
```

This creates a `train.bin` and `val.bin` in that data directory. Now it is time to train your GPT. The size of it very much depends on the computational resources of your system:

**I have a GPU, trained it on a 24GB GPU**. Great, we can quickly train a baby GPT with the settings provided in the [config/train_shakespeare_char.py](config/train_shakespeare_char.py) config file:

```
$ python train_task3.py config/train_shakespeare_char.py
```

On one GPU this training run takes about 7 minutes and the best validation loss is 2.66. Based on the configuration, the model checkpoints are being written into the `--out_dir` directory `out-shakespeare-char`. So once the training finishes we can sample from the best model by pointing the sampling script at this directory:

```
$ python sample.py --out_dir=out-shakespeare-char
```

This generates a few samples, for example:

```
ANGELO:
And cowards it be strawn to my bed,
And thrust the gates of my threats,
Because he that ale away, and hang'd
An one with him.

DUKE VINCENTIO:
I thank your eyes against it.

DUKE VINCENTIO:
Then will answer him to save the malm:
And what have you tyrannous shall do this?

DUKE VINCENTIO:
If you have done evils of all disposition
To end his power, the day of thrust for a common men
That I leave, to fight with over-liking
Hasting in a roseman.
```

This is after 7 minutes of training on a GPU.




