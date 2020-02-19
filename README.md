# Kaggle Google QUEST + Fastai v2

Notebooks used to train a AWD LSTM language model and classifier using fastai v2 for the [Kaggle Google QUEST Challenge](https://www.kaggle.com/c/google-quest-challenge)

## NB1. Q&A Data for Pretraining
Processes and combines 3 different text datasets into a single source ready for language model pre-training. This notebook outputs a 850mb text data file with 84M words/tokens with the following distribution:

- 65% from wiki103
- 18% from Tensorflow 2.0 Q&A
- 17% from the StackSample dataset
