# Sentiment Analysis with Neural Networks

This is the project review I got for the project "Sentiment Analysis with Neural Networks" in the "AI for trading" nanodegree



## Meets Specifications

Congratulations on meeting all the specifications of this project! I hope that you enjoyed working on the deep learning on text project.

## Importing Twits

- [x] Print the number of twits in the dataset.

	![:thumbsup:](https://review.udacity.com/assets/images/emojis/thumbsup.png ":thumbsup:")

## Preprocessing the Data

- [x] The function  `preprocess`  correctly lowercases, removes URLs, removes ticker symbols, removes punctuation, tokenizes, and removes any single character tokens.

	A regular expression used in the  `preprocess`  function allows us to search for patterns in text in a fast and automated manner.

	`preprocess`  function tokenizes the messages as expected;

	`preprocess("RT @google Our annual look at the year in Google blogging (and beyond) http://t.co/sptHOAh8 $GOOG")`  
gives us;

	`['rt', 'our', 'annual', 'look', 'at', 'the', 'year', 'in', 'google', 'blogging', 'and', 'beyond']`

- [x] Preprocess all the twits into the  `tokenized`  variable.

	You can pickle and serialize these variables like  `tokenized`  variable which takes long to process and save it to the workspace. So that you don't have to re-run all the variables again. That is you can pick up the work where you left off in the last session.

	```
	# saving the tokenized file 
	import pickle
	pickle.dump( tokenized, open( "tokenized.p", "wb" ) )
	# loading the tokenized file
	import pickle 
	tokenized = pickle.load( open( "tokenized.p", "rb" ) )
	```

- [x] Create a bag of words using the tokenized data.

	The bag of words (BOW) is used to encode the words into the numerical form. Because the model cannot use the text directly in its matrix computation.

	I encourage you to use  `tqdm`  progress bar which is useful to keep track of the loading time. Check out this blog  [https://www.geeksforgeeks.org/python-how-to-make-a-terminal-progress-bar-using-tqdm/](https://www.geeksforgeeks.org/python-how-to-make-a-terminal-progress-bar-using-tqdm/)

- [x] Remove most common and rare words by defining the following variables:  `freqs`,  `low_cotoff`,  `high_cutoff`,  `K_most_common`.

	Here, we have to remove/filter out two kinds of tokens.

	Very common words like 'the', 'a', 'an' which don't tell anything about the sentiments of the tweet messages. You can filter out the common words with High-cutoff threshold.

	`High_cutoff`  should not be too high. If the number is too big, we lose lots of important words that we can use in our data.

	Very rare words that show up in very few tweets messages. You can filter out the rare words with  `low_cutoff`  threshold.

	These thresholds should be configured so that not too many words are filtered out but then least frequent words should be filtered.

- [x] Defining the variables : 'vacab', 'id2vocab' and 'filtered' correctly.

	Nice work in using  `vocab`  as a dictionary and creating it with dictionary comprehension.

	Dictionary is a hash table which has constant search time (i.e. O(1) ) while looking up for the element. Check out this course which is about data structures and algorithms  [https://www.udacity.com/course/data-structures-and-algorithms-in-python--ud513](https://www.udacity.com/course/data-structures-and-algorithms-in-python--ud513)

## Neural Network

- [x] The init function correctly initializes the following parameters:  `self.vocab_size`,  `self.embed_size`,  `self.lstm_size`,  `self.lstm_layers`,  `self.dropout`,  `self.embedding`,  `self.lstm`, and  `self.fc`.

	All the required parameters/layers have been initiated as the instance variables.

	```
	        # Setup embedding layer
	        self.embedding = nn.Embedding(vocab_size, embed_size)
	```

	Word embeddings are learned representations of words in the form of vectors. Word Embedding is a technique for reducing the high dimensional representation of words into a low dimensional and dense vector space. Each token/word can be represented by a fixed length vector (embedding size). Semantic relations between words are captured by this technique when training with the neural network using the backpropagation. For example, 'king' and 'queen' are semantically similar as both these words occur in the same context, therefore the learned vectors of these words will be similar/closer in distance.  
These embedding layers have randomly initialized weights. We can also use pre-trained embeddings

- [x] The 'init_hidden' function generates a hidden state

	LSTMs are the type of the recurrent neural nets. In recurrent neural nets weight parameters are shared between the hidden units. That means information given to the hidden unit at time t is not only coming from input unit but also from the hidden units of previous time stamps. So the input nodes and previous hidden states are concatenated together and then multiplied with weights. As a result, back-propagation through time is carried out as the inputs from the previous timestamps are also considered. The sequential learning by sharing the weights is carried within the sequence length hyperparameter in the RNN layer.

	I'd highly encourage you to go over this classical blog on LSTM  [http://colah.github.io/posts/2015-08-Understanding-LSTMs/](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)  
In reality the LSTM network is implemented as given below at the left side of the diagram i.e. as the rolled network. The right-side of the diagram is just for the people to understand all the math and computational theory (it's like we are "imagining" how the network will look like when it is unrolled).

	[![unrolled.png](https://udacity-reviews-uploads.s3.us-west-2.amazonaws.com/_attachments/35191/1634563588/unrolled.png)](https://udacity-reviews-uploads.s3.us-west-2.amazonaws.com/_attachments/35191/1634563588/unrolled.png)

- [x] The 'forward' function performs a forward pass of the model the parameter input using the hidden state.

	Nice work in using  `self.softmax=nn.LogSoftmax(dim=1)`  as later  `torch.exp`  is used in the predict function;  
`torch.exp`  is used to get the softmax probability when you use  `nn.LogSoftmax`  as the output layer function.

	exponent which is  `torch.exp`  cancels the logarithm which is log-softmax

## Training

- [x] Correctly split the data into  `train_features`,  `valid_features`,  `train_labels`, and  `valid_labels`.

	Check out this Udacity video to see why the splitting of the data is needed to be done;  
[https://www.youtube.com/watch?v=Lmxem7ud9yk&list=PLAwxTw4SYaPn_OWPFT9ulXLuQrImzHfOV&index=16](https://www.youtube.com/watch?v=Lmxem7ud9yk&list=PLAwxTw4SYaPn_OWPFT9ulXLuQrImzHfOV&index=16)

- [x] Train your model with dropout and clip the gradient. Print out the training progress with the loss and accuracy.

	You should create the pickled checkpoint of your  `pytorch`  model. Check out how to do that  [https://pytorch.org/tutorials/beginner/saving_loading_models.html](https://pytorch.org/tutorials/beginner/saving_loading_models.html)

	In this way, you don't need to retrain the network after every new session.

	```
	#saving the torch model to the main directory
	import torch
	torch.save(model, '/home/workspace/checkpoint.pth')
	#loading the torch model on to the CPU 
	model = torch.load('checkpoint.pth', map_location=lambda storage, loc: storage)
	```

## Making Predictions

- [x] The  `predict`  function correctly prints out the prediction vector from the trained model.

	Nice work! One of the difference between the prediction and training of the network is that during the prediction, the model is used to give out the prediction output values and there's no weight updates in the model during the prediction. On the other hand, during the training phase, the model is used to calculate the weight values by using gradient descent and minimize the prediction error by the back-propagation algorithm

- [x] Answer what the prediction of the model is and the uncertainty of the prediction.

	In order to further assess the model's performance, you can look into the metrics like recall, precision, specificity, ROC curve, F1 and confusion metrics. Check out these terms on the web if you are unfamiliar. :)
