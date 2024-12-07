# Overview of the analysis: Explain the purpose of this analysis.

## Results: Using bulleted lists and images to support your answers, address the following questions:

## Data Preprocessing

What variable(s) are the target(s) for your model?
* IS_SUCCESSFUL—Was the money used effectively


What variable(s) are the features for your model?
* APPLICATION_TYPE—Alphabet Soup application type
* AFFILIATION—Affiliated sector of industry
* CLASSIFICATION—Government organization classification
* USE_CASE—Use case for funding
* ORGANIZATION—Organization type
* STATUS—Active status
* INCOME_AMT—Income classification
* SPECIAL_CONSIDERATIONS—Special considerations for application
* ASK_AMT—Funding amount requested


What variable(s) should be removed from the input data because they are neither targets nor features?
* EIN and NAME as they are identification columns that may look as columns that don't provide insight to the model


## Compiling, Training, and Evaluating the Model

How many neurons, layers, and activation functions did you select for your neural network model, and why?

features_count = len(X_train[0])
neurons_first_layer = features_count * 2
neurons_second_layer = features_count

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┓
┃ Layer (type)                         ┃ Output Shape                ┃         Param # ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━┩
│ dense (Dense)                        │ (None, 86)                  │           3,784 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_1 (Dense)                      │ (None, 43)                  │           3,741 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_2 (Dense)                      │ (None, 1)                   │              44 │
└──────────────────────────────────────┴─────────────────────────────┴─────────────────┘
 Total params: 7,569 (29.57 KB)
 Trainable params: 7,569 (29.57 KB)
 Non-trainable params: 0 (0.00 B)

 * The objective was to keep the neurons between 2 or 3 times the number of features and the parameters less than or equal to the square root of the number of entries on the data set.


Were you able to achieve the target model performance?
* The objective was to achieve a target predictive accuracy higher than 75%. However, we only got to 73.04%.

268/268 - 0s - 2ms/step - accuracy: 0.7305 - loss: 0.5632
Loss: 0.5632087588310242, Accuracy: 0.7304956316947937


What steps did you take in your attempts to increase model performance?
* AlphabetSoupCharity_Optimization1.ipynb - No improvement => 73.04%
    - add more buckets to APPLICATION_TYPE and CLASSIFICATION
    - add one more layer and reorganize the number of neurons

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┓
┃ Layer (type)                         ┃ Output Shape                ┃         Param # ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━┩
│ dense_15 (Dense)                     │ (None, 72)                  │           3,528 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_16 (Dense)                     │ (None, 48)                  │           3,504 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_17 (Dense)                     │ (None, 48)                  │           2,352 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_18 (Dense)                     │ (None, 1)                   │              49 │
└──────────────────────────────────────┴─────────────────────────────┴─────────────────┘
 Total params: 9,433 (36.85 KB)
 Trainable params: 9,433 (36.85 KB)
 Non-trainable params: 0 (0.00 B)

 268/268 - 0s - 2ms/step - accuracy: 0.7305 - loss: 0.5795
Loss: 0.5795323252677917, Accuracy: 0.7304956316947937

* AlphabetSoupCharity_Optimization2.ipynb - Some improvement => 73.28%
    - using optimized model 1, split the INCOME_AMT into two columns: low_income_values the lower limit of the range and high_income_values the high limit of the range

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┓
┃ Layer (type)                         ┃ Output Shape                ┃         Param # ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━┩
│ dense (Dense)                        │ (None, 65)                  │           2,730 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_1 (Dense)                      │ (None, 41)                  │           2,706 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_2 (Dense)                      │ (None, 41)                  │           1,722 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_3 (Dense)                      │ (None, 1)                   │              42 │
└──────────────────────────────────────┴─────────────────────────────┴─────────────────┘
 Total params: 7,200 (28.12 KB)
 Trainable params: 7,200 (28.12 KB)
 Non-trainable params: 0 (0.00 B)

 268/268 - 0s - 2ms/step - accuracy: 0.7328 - loss: 0.5612
Loss: 0.5612047910690308, Accuracy: 0.7328279614448547

* AlphabetSoupCharity_Optimization3.ipynb - Got above 75% => 75.39%
    - using optimized model 2, add NAME and create buckets
    - add more APPLICATION_TYPE and CLASSIFICATION buckets

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┓
┃ Layer (type)                         ┃ Output Shape                ┃         Param # ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━┩
│ dense_12 (Dense)                     │ (None, 103)                 │           8,240 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_13 (Dense)                     │ (None, 79)                  │           8,216 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_14 (Dense)                     │ (None, 79)                  │           6,320 │
├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤
│ dense_15 (Dense)                     │ (None, 1)                   │              80 │
└──────────────────────────────────────┴─────────────────────────────┴─────────────────┘
 Total params: 22,856 (89.28 KB)
 Trainable params: 22,856 (89.28 KB)
 Non-trainable params: 0 (0.00 B)

 268/268 - 0s - 2ms/step - accuracy: 0.7539 - loss: 0.5267
Loss: 0.5267384052276611, Accuracy: 0.7539358735084534


Summary: Summarize the overall results of the deep learning model. Include a recommendation for how a different model could solve this classification problem, and then explain your recommendation.
* To get an accuracy above 75%, I had to create a model with 22856 parameters (a third of the total entries of the data set), which can lead toward an overfitted model. To improve the accuracy and robustness of the predictions and to reduce overfitting, a random forest model could be a better option.
