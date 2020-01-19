# Suggestion-Mining
Use of "tensorflow" to apply RNN (Recurrent Neural Network) for suggestion mining

This was done as part of Neural Networks Course (BITS Goa), Fall 2019.
(https://www.kaggle.com/c/nnfl-assignment-3).

# Task: Suggestion Mining

-> Suggestion mining can be defined as the extraction of suggestions from unstructured text, where the term 'suggestions' refers to the expressions of tips, advice, recommendations etc. Consumer opinions towards commercial entities like brands, services, and products are generally expressed through online reviews, blogs, discussion forums, or social media platforms. These opinions largely express positive and negative sentiments towards a given entity, but also tend to contain suggestions for improvising the entity or tips to the fellow consumers. We had to perform domain specific suggestion mining, where the test dataset belonged to the same domain as the training and development datasets.

# Data:
-> 8500 sets of reviews and class (0 or 1)
-> Class indicates whether the review suggests something or not.

# Pricedure:
-> Data was not balanced and was made balanced by introducing random duplicates of dominated class.
-> Glove word embedding is used to represent sentences as 300 dimentional vectors.
-> Used one hot encoding for class

# Model:
__________________________________________________________________________________________________
Layer (type)                    Output Shape         Param #     Connected to     

==================================================================================================
input_2 (InputLayer)            (None, 100)          0                                            
__________________________________________________________________________________________________
embedding_3 (Embedding)         (None, 100, 300)     3000000     input_2[0][0]                    
__________________________________________________________________________________________________
spatial_dropout1d_3 (SpatialDro (None, 100, 300)     0           embedding_3[0][0]                
__________________________________________________________________________________________________
bidirectional_4 (Bidirectional) (None, 100, 200)     241200      spatial_dropout1d_3[0][0]        
__________________________________________________________________________________________________
conv1d_7 (Conv1D)               (None, 99, 132)      52932       bidirectional_4[0][0]            
__________________________________________________________________________________________________
global_average_pooling1d_5 (Glo (None, 132)          0           conv1d_7[0][0]                   
__________________________________________________________________________________________________
global_max_pooling1d_5 (GlobalM (None, 132)          0           conv1d_7[0][0]                   
__________________________________________________________________________________________________
concatenate_2 (Concatenate)     (None, 264)          0           global_average_pooling1d_5[0][0] 
                                                                 global_max_pooling1d_5[0][0]     
__________________________________________________________________________________________________
dense_3 (Dense)                 (None, 2)            530         concatenate_2[0][0]     

==================================================================================================
Total params: 3,294,662
Trainable params: 294,662
Non-trainable params: 3,000,000
__________________________________________________________________________________________________


-> Epochs = 400

-> Batch Size = 1000

-> Activations used were 'relu' and 'softmax'

# Results :

-> 95.2845 % accuracy
