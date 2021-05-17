# NLP: SMS-Spam-Collection
Detecting if SMS messages are spam or legitimate (ham)

## Introduction
This poject, from Kaggle, is to detect if text messages are spam or ham/legitimate:
https://www.kaggle.com/uciml/sms-spam-collection-dataset/activity

The dataset, collected for SMS spam research, is named "spam.csv" and includes 5572 text messages labelled as spam or ham. 

## Preprocessing
In the following, a data cleanning function, "CleanData", is programmed dropping mostly blank columns, removing punctuations and stopwords, and tokenizing the text messages. Finally, the dataset is split into 4 different sets representing training and test sets and their corresponding labels: x_train, x_test, y_train, y_test. 80% of the original dataset is considered for the training set and 20% for the test set.

## The four models

Four different models are trained, tested and compared for the problem: TFIDF, Word_2_Vec (W2V), Doc_2_Vec (D2V) and a Recurrent Neural Network (RNN). Three metrics are considered to evaluate each model and compare them:

##### Precision: The probability  if a message detected as a spam is truely spam
##### Recall: The probability that a spam is detected as a spam
##### Accuracy: The probability if a text message, no matter spam or ham, is correctly classified.

About the nature of this problem, for users it is very important to receive and read all the ham messages, and they would care a little less if they receive a few spam messages. In other words, the precision is more important than recall and accuracy.

The metrics as calculated by any of the models and printed in the corresponding notebooks are lited below for precision, recall and accuracy, respectively:


###### TFIDF:   1.0,    0.7888,   0.9695
###### W2V:    0.613, 0.354, 0.874
###### D2V:    0.925, 0.385, 0.907
###### RNN:    0.9807, 0.9533, 0.9874


### Result Analysis
If we take TFIDF as the base model for our comparison, each of the W2V, D2V and RNN models add
more complexity to the model incrementaly in the order as mentioned. Taking a quick look at the result suggests that TFIDF, while being the least complex, returns almost the best outcome, especially, that for this problem, precision is the most important metric. Though, RNN, in accuracy, slightly outperforms, and in recall, dramatically outperforms TFIDF. Below is more analysis on resultes by W2V, D2V and RNN.

#### W2V:
The W2V's results are much worse than those of TFIDF for all the three of precision, recall and accuracy which is normal as Word_2_Vec is not intended to create representation for senteces. It is here averaging word vectors of sentences to create representations for the sentences. In other words, the added complexity is not worth it!

#### D2V:
The D2V's results are better than those by the Word_2_Vec model in all the 3 precision, recall and accuracy metrics which is normal considering the Word_2_Vec's drawback with averaging word vectors for each text message. However, this model did not beat the TFIDF model either. So far, adding more complexity to the model, which is the case with both Word_2_Vec and Doc_2_Vec models, has not resulted in any improvement to the TFIDF model.

#### RNN:
The RNN model outperformed W2V and D2V in all the 3 metrics, and outperformed TFIDF model in accuracy and recall metrics while the precision is almost as good. The improvement in recall though is significant.

## Conclusion
It is fully clear that TFIDF and RNN outperfom W2V and D2V by a huge margin. TFIDF seems even more promising with respect to the fact that for the nature of this problem, precision outweighs recall. However, the RNN delivers better accuracy and much better recall at a cost of a slightly worse precision compared to TFIDF. These make RNN a great choice as well. Depending on the importance of either metric to the user, and the complexity of the models, either modedel could be applied.
