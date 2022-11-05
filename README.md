# sinch-intent-detection

This competition is hosted by Sinch, a global leader in cloud communications for mobile customer engagement. I participated to that competition as a requirement for applying to an internship at Sinch.

The goal of the competition is to predict the intent of a text message. The dataset contains extracted features from text messages.

The train set contains 1663 samples from 45 intents. The test set contains 713 samples. The dataset is imbalanced. Each data point has 768 features probably extracted with sentence BERT. The features are normalized.

## Appproach

### No feature engineering

As the data is an embedding of texts, there is no interpretable meaning behind the features. Because of that, I did not perform any feature engineering. I tried to use the features as they are.

### KNN, Logistic Regression, SVM

I first tried to use KNN, Logistic Regression and SVM. I fine tuned the hyperparameters a bit by hand. The results were not bad but not good enough to be in the top.

### XGBoost

I used the default parameters but it had always overfitting issues, probably because of the high variance of XGBoost models. I tried with much less trees and nodes for each tree but it did not help.

### Recurrent Neural Network

I used a simple RNN and a LSTM. These models struggled to improve their score even on train set. I think that the problem is that the data is not sequential. The data is an embedding of texts, so the order of the words does not matter.

### Fully connected neural network

Fully connected neural networks finally had appealing results! That was expected as features are continuous variables outputed from a neural network.

### Stratified KFold and random search

I decided to use stratified k-fold cross validation to search for the best hyperparameters. I used a random search with 5 folds.

### Ensemble

I combined the outputs of the best models trained on each fold with a simple vote to get the final predictions.

### Pseudo-labeling

To get more data, I used the test set to get pseudo-labels. I used the best model trained on the train set to predict the labels of the test set. I filtered the test set to keep only the samples with a high confidence. I then added the pseudo-labels to the train set and retrained the model.

## Conclusion

This competition was a good opportunity to get back to the source with basic machine learning algorithms. Not much feature engineering was needed as the data is already an embedding of texts. I used a simple ensemble of neural networks to get the best results. I also used pseudo-labeling to get more data. Overall, I am satisfied for a 10-hour work. I could get my internship interview!
