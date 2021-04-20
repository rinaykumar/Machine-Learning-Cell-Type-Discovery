## Random Forest Machine Learning applied to single cell transcriptomics for cell type discovery
![GitHub top language](https://img.shields.io/github/languages/top/rinaykumar/Machine-Learning-Cell-Type-Discovery)
![GitHub](https://img.shields.io/github/license/rinaykumar/Machine-Learning-Cell-Type-Discovery)

## Training Database
The training data for this experiment was obtained from J. Craig Venter’s ‘e1 positive.csv’ data sheet, consisting of data related to “Cell type discovery using single cell transcriptomics: implications for ontological representation” by Aevermann B. et al, published in Molecular Genetics 27(R1): R40-R47 · March 2018.

Each column represents gene information with numerical values, with the last column representing a classification label of either positive (1) or negative (0). The data was uploaded into Jupyter Notebook and was first checked to see if the total number of rows and columns were equal with the e1 positive.csv file.

<img src="/img/1.png" width='400px'/>

Following this, the number of positive and negative classes in the data set were checked to see if they matched what was in the original data sheet.

<img src="/img/2.png" width='400px'/>
<img src="/img/3.png" width='400px'/>

The data was then checked to see if it was balanced.

<img src="/img/4.png" width='400px'/>

One series of the experiment was conducted by training the Random Forest model with the entire data set, and another was done with splitting the data into train and test sets. 75% of the data randomly chosen was put into the ‘train’ set, and 25% was put in to the ‘test’ set with R’s ‘sample’ function. The train set was then checked to see how many positive and negative labels it contained and was checked to see if it was balanced.

<img src="/img/5.png" width='400px'/>

The train set contained 221 positive classes and 432 negative classes and appears to be balanced. The same checks were conducted on the test set, to see its positive and negative labels, and to see it was balanced.

<img src="/img/6.png" width='400px'/>

The test set contained 78 positive classes and 140 negative classes and appears to be balanced.
In summary, first the number of rows and columns in the original CSV data file were found to be 871 rows and 609 columns. After importing the data into Jupyter Notebook, the rows and columns in the data set were checked and contained the same 871 rows and 609 columns.
Then the number of positive (1) classes and negative (0) classes in the data set were checked in Jupyter Notebook, and showed 299 positive labels and 572 negative labels, which was compared with the number of positive and negative labels in the original CSV data file, which also contained 299 positive and 572 negative labels. The data appeared to be balanced, as positive / samples = 299 / 871 = 0.34 or 34%, which is more than 10%.
For the second series of the experiment involving splitting the data into train and test sets, the number of positive and negative classes in each set were checked, and each set was checked to see it was balanced.

## Software Tools
The first installation was of minicoda for Mac. With minicoda set up, a virtual environment was created for the experiment by cloning the Random Forest Workshop repository from GitHub, as provided by Luis Chumpitaz Diaz. With the virtual environment set up, Jupyter Notebook was used to code and run the experiment in R.
Within Jupyter Notebook, the following R libraries were utilized: randomForest (for the Random Forest model), dplyr (for data frame manipulation), caret (for classification and feature selection), e1071 (for class analysis), and MLmetrics (to generate F1 Scores).

## Experimental Methods and Setup:
The experiment was conducted using models with varying parameters to find the best trained Random Forest model.
The first series was done with the Random Forest model trained with the entire data test, with configurations including NTREE set to 500 and 1000, MTRY set to 0.5*SQRT(N_FEATURES) = 12, SQRT(N_FEATURES) = 24, and 2*SQRT(N_FEATURES) = 48, and CUTOFF values set to 0.1, 0.2, 0.3, etc. to 0.9.
The second series was done with the Random Forest model trained on just the train set, with the same parameters and configurations mentioned above.

## Results of Random Forest Training and Accuracy Estimates:
For each of the models trained in the first series of experiments with the Random Forest model trained on the entire data set, the OOB score and F1 score were checked to find the best trained model. For the first series of tests done with the Random Forest model trained on the entire data set, the configuration with the lowest OOB score and highest F1 score was done with NTREE=500, MTRY=12, and CUTOFF=0.5, and is subsequently named ‘model’.

<img src="/img/7.png" width='600px'/>

The OOB score for this selected model was 0.46%, and the confusion matrix can be seen here.

<img src="/img/8.png" width='400px'/>

The model made 298 positive predictions that were actually positive, and 569 negative predictions that were actually negative, with 1 false positive and 3 false negative predictions. The total negative predictions were 569+3 = 572, and the total positive were 298+1 = 299. These two figures match the original data set’s negatives classes of 572 and positive classes of 299 (as seen in Figure 2).
From this confusion matrix, the F1 score was calculated as follows: F1 = 2TP / (2TP + FP + FN) = 2(298) / (2*298 + 1 + 3) = 0.99333.
The plot of the model was made that showed the error rate plateauing at around 100 trees.

<img src="/img/9.png" width='400px'/>

Since the Random Forest model was trained with the ‘importance’ parameter set to true, the variable importance plot run on the model shows the top ten features when utilizing MDA (Mean Decrease Accuracy), and with Mean Decrease Gini.

<img src="/img/10.png" width='400px'/>

According to this variable importance plot, the top ranked feature with the most impact is the gene TESPA1 with both MDA and Gini, with variations in the remaining nine most important genes between the two MDA and Gini plots.
The second series of experiments were done with the original data split into train and test sets. Variations in parameters were tested for each of the models created with the Random Forest model trained on just the train set, with NTREE, MTRY, and CUTOFF values adjusted in the same way as the first series, with checks on the OOB score and F1 score to find the best trained model on the split train set.

The selected model with the split train set had NTREE=500, MTRY=12, and CUTOFF=0.5, the same parameters as the first model, and the subsequent model was named ‘modelSplit’.

<img src="/img/11.png" width='600px'/>

The OOB score for this selected model was 0.46%, the same as the first model without any data split, and the confusion matrix can be seen here.

<img src="/img/12.png" width='400px'/>

The modelSplit model made 221 positive predictions that were actually positive, and 429 negative predictions that were actually negative, with 0 false positives and 3 false negatives. The total negative predictions were 429+3 = 432, and the total positive were 221. These two figures match the train set’s negatives classes of 432 and positive classes of 221 (as seen in Figure 5).
The F1 score for modelSplit was calculated as follows: F1 = 2TP / (2TP + FP + FN) = 2(221) / (2*221 + 0 + 3) = 0.99325. This F1 score is very similar to the F1 score of the first model done without splitting the data.

Variable importance on modelSplit showed the top ten features with MDA and Gini.

<img src="/img/13.png" width='400px'/>

The top ranked feature with MDA for modelSplit was TESPA1, which is the same as the variable importance plot done with the first model without data split (Figure 10), however the remaining variables/genes differ in the two models.
The prediction phase was conducted with both models, with the prediction done on the first model (without data split) on the entire data set, and with the prediction on the second model, modelSplit (with data split), on the test data set. Each prediction’s confusion matrix had an accuracy of 1, and F1 scores of 1.

## Random Forest Run Time Test:
The selected Random Forest model without data split, with NTREE=500, MTRY=12, and CUTOFFF=0.5, was run on two sample rows from the original data set, one with a positive classification and one with a negative classification, to judge the performance of the model.
The first test was conducted using ‘runtime1’, which was set to row 3 in the data frame. The test was run with the predict function to see if it could predict the classification label. The model correctly predicted the label as positive, or 1.

<img src="/img/14.png" width='400px'/>

The second test was conducted using ‘runtime2’, which was set to row 343 in the data frame. The test again was run with the predict function, and the model accurately predicted the classification label as negative, or 0.

<img src="/img/15.png" width='400px'/>

Based on these two small run time tests, it appeared that the first model (done without data split) was functioning as expected. The test was repeated for the second model (modelSplit – with data split), and it too correctly classified each label.

<img src="/img/16.png" width='400px'/>

## Summary
Both models, ‘model’ done without any data split and trained on the entire data set, and ‘modelSplit’ done with the data split into train and test sets and trained on the train set, had the same OOB score of 0.46% and similar F1 scores of 0.99333 and 0.99325 respectively.
During the prediction phase, ‘model’ was run on the prediction function with the entire data set, and ‘modelSplit’ was run with the test data set, and in each case the resulting confusion matrices had an accuracy of 1 with the number of samples matching the entire data set for ‘model’ and matching the test data set for ‘modelSplit’, with each also having the same F1 scores.
The runtime tests for both ‘model’ and ‘modelSplit’ accurately made the right positive or negative predictions, indicating the models functioned as expected.
What differed most between the two models were the variable importance plots with top ten most important features. While both ‘model’ and ‘modelSplit’ had TESPA1 as the most important feature (with MDA), the remaining nine features varied, which could be within expected statistical range, or indicate some issue with the implementation or training.
