# Project Background

The U.S. Patent and Trademark Office (USPTO) offers one of the largest repositories of scientific, technical, and commercial information in the world through its Open Data Portal. Determining the semantic similarity between phrases is critically important during the patent search and examination process to determine if an invention has been described before. For example, if one invention claims "television set" and a prior publication describes "TV set", a model would ideally recognize these are the same and assist a patent attorney or examiner in retrieving relevant documents. This extends beyond paraphrase identification; if one invention claims a "strong material" and another uses "steel", that may also be a match. What counts as a "strong material" varies per domain (it may be steel in one domain and ripstop fabric in another, but you wouldn't want your parachute made of steel).

# Project task
Build a model to match phrases in order to extract contextual information, thereby helping the patent community connect the dots between millions of patent documents.

# Mode and Strategy
Our model is compatible with the HuggingFace framework so you can change the model to any BERT based model you want.

The following shows the unique method we use generating the best solution.

### 1.Data pre-processing:
We delete the formula like chemical formula in the dataset and change in to human languages.
### 2.Data-augmentation:
We add more context text to our train set to help our model better understand the mean of patent phrases under a specific context
### 3.Model selection
We select the most state-of-the art model on Hugging face inluding :

- Microsoft/debert-v3-large

- anferico-bert-for-patent-large

- Microsoft/devert-v3-small

- Microsoft/cocolm-v3-large

- Microsoft/debert-v2-xlarge

- Google/electra-large





### 4.Doble loss:


### 5.Model stacking:



















# Dataset description

The dataset contains pairs of phrases (an anchor and a target phrase) and asked to rate how similar they are on a scale from 0 (not at all similar) to 1 (identical in meaning). This challenge differs from a standard semantic similarity task in that similarity has been scored here within a patent's context, specifically its CPC classification (version 2021.05), which indicates the subject to which the patent relates. For example, while the phrases "bird" and "Cape Cod" may have low semantic similarity in normal language, the likeness of their meaning is much closer if considered in the context of "house".

The scores are in the 0-1 range with increments of 0.25 with the following meanings:

1.0 - Very close match. This is typically an exact match except possibly for differences in conjugation, quantity (e.g. singular vs. plural), and addition or removal of stopwords (e.g. “the”, “and”, “or”).
0.75 - Close synonym, e.g. “mobile phone” vs. “cellphone”. This also includes abbreviations, e.g. "TCP" -> "transmission control protocol".
0.5 - Synonyms which don’t have the same meaning (same function, same properties). This includes broad-narrow (hyponym) and narrow-broad (hypernym) matches.
0.25 - Somewhat related, e.g. the two phrases are in the same high level domain but are not synonyms. This also includes antonyms.
0.0 - Unrelated.

## Files
train.csv - the training set, containing phrases, contexts, and their similarity scores
test.csv - the test set set, identical in structure to the training set but without the score
sample_submission.csv - a sample submission file in the correct format

## Columns
id - a unique identifier for a pair of phrases
anchor - the first phrase
target - the second phrase
context - the CPC classification (version 2021.05), which indicates the subject within which the similarity is to be scored
score - the similarity. This is sourced from a combination of one or more manual expert ratings.

## Evalutaion 
Submissions are evaluated on the Pearson correlation coefficient between the predicted and actual similarity scores.

