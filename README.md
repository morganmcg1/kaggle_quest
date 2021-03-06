# Kaggle Google QUEST + Fastai v2

- Notebooks used to train a AWD LSTM language model and classifier using fastai v2 for the [Kaggle Google QUEST Challenge](https://www.kaggle.com/c/google-quest-challenge)

- These are all heavily influenced by the [fastai-v2 ULMFiT and Wikitext tutorials here](http://dev.fast.ai/tutorial.ulmfit)

- I entered the competition quite late and spent too much time on learning the new fastai v2 framework, so didn't actaully get any decent results, but hopefully some of the code here will be useful for you in your LSTM endevours!

## NB1. Q&A Data for Pretraining
Processes and combines 3 different text datasets into a single source ready for language model pre-training. This notebook outputs a 850mb text data file with 84M words/tokens with the following distribution:

- 65% from wiki103
- 18% from Tensorflow 2.0 Q&A
- 17% from the StackSample dataset

## NB 2. Pretraining an AWD LSTM model with fastai v2
This notebook will pretrain an AWD LSTM model using a custom text dataset designed especially for this Q&A competition.

The SentencePiece Tokenizer with Byte-Pair Encoder (bpe) was used for tokenization instead of the standard fastai Spacy tokenizer. It was trained for 7 epochs and it took 2h14m per epoch.

## NB 3. Language Model Finetuning on competition Q&A

Finetune the pretrained AWD LSTM Language Model on the competition Q&A data. Because we are finetuning the LM, we can use all of the competition data, both the train and test set.

## NB 4. AWD LSTM Q&A classification and prediction
Using the encoder from our finetuned language model in a text classification model to be trained on the competition data.

**Note:** As of writing the fastai `SortedDL` dataloader sorts predictions according to item size, however for kaggle we need the predictions output in the same order as the submissions file, which is generally the same order as the input test file.

So there was 1 more step to do after making out preds before I could use them. I had to get the original indexes from the dataloader and then re-sort the preds:
```
pred_idxs = tst_cls_dls.get_idxs()
sorted_preds = [x for _,x in sorted(zip(pred_idxs, list(torch.unbind(preds[0]))))]
```
