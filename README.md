# Kaggle Google QUEST + Fastai v2

Notebooks used to train a AWD LSTM language model and classifier using fastai v2 for the [Kaggle Google QUEST Challenge](https://www.kaggle.com/c/google-quest-challenge)

## NB1. Q&A Data for Pretraining
Processes and combines 3 different text datasets into a single source ready for language model pre-training. This notebook outputs a 850mb text data file with 84M words/tokens with the following distribution:

- 65% from wiki103
- 18% from Tensorflow 2.0 Q&A
- 17% from the StackSample dataset

## NB 2. Pretraining a AWD LSTM model with fastai v2
This notebook will pretrain an AWD LSTM model using a custom text dataset designed especially for this Q&A competition.

The SentencePiece Tokenizer with Byte-Pair Encoder (bpe) was used for tokenization instead of the standard fastai Spacy tokenizer. It was trained for 7 epochs and it took 2h14m per epoch.
