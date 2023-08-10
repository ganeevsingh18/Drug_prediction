# Drug_prediction

This program identifies Drug and Effects from given Medical Data

Used SciBERT model and Fine-Tuning on Drug/ADE Corpus

DATASET
We use the Ade_corpus_v2_drug_ade_relation subset of the ade_corpus_v2 dataset, which provides labeled spans for drug names and adverse effects. See dataset page here: https://huggingface.co/datasets/ade_corpus_v2

CHANGED FORMAT OF DATASET
Upon further examination of the dataset, we can see that sentences are often repeated to identify different pairs of drugs and adverse reactions. For example, see this sentence from the dataset:
This is not ideal in an NER setting - if we assigned one set of token labels per row in this dataset as-is, we would end up giving different labels to the same tokens in the same sentences. This would confuse the model during fine-tuning, so we need to consolidate all of the ranges provided for each unique sentence, before performing one pass to label all known entities.

TOKENISATION
With the dataset consolidated, we need to assign per-token labels to each sentence. First, we re-define our Python data structure as a Hugging Face Dataset object.
Finally, we can label each token with its entity. We use BIO tagging on two entities, DRUG and EFFECT. This results in five possible classes for each token:
O - outside any entity we care about
B-DRUG - the beginning of a DRUG entity
I-DRUG - inside a DRUG entity
B-EFFECT - the beginning of an EFFECT entity
I-EFFECT - inside an EFFECT entity

RESULT
We have trained the model on Train data and then tested the train model on the TEST data.
The trained model correctly identifies a Drug with precision of 0.9399555226093402 and identifies Effects with precision of 0.7682458386683739
The overall accuracy of the model is 0.9585490352242696

