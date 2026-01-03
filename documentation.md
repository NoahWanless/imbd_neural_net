##----------------Detailed description----------------##
What is this project? What is it doing? What is the context of creating it? What is its purpose?

We have made a Neural Network, a prediction model with the purpose of taking in text movie reviews and predicting whether the movie review is a positive or negative movie review undergoing matrix math, multiplication of the feature vector, by the matrix of weights to gain a new feature vector, which down the road, becomes the output format we desire and thus, a prediciton. Along with training the model as it works so that it can later make better and better predictions using the algorithim of backpropagation as outlined in the textbook we used and then having the model saved in a file so that that model can be loaded in and used later on. 
Sense AI is gaining more and more importance these days, we felt like making a proof of concept to help us gain understanding in the feild (and sense two of use want to go into comupter sicence) we think this would help us better interact with the world of machine learning and AI.
##---Assumptions---##
That the user will only run the code as it is presented, only inputing values between 1 and 10 and if they choose to do otherwise that that will break it
if they choose to attempt to switch it to training mode as directed by commetns, it is assumed that the user understands that they may unintentionally break something however we have provided a fully trained model, so training is unnecassary
##----------------Overview and justification----------------##
Why did you develop your code the way you did? 

The code was made in such a way so that all the 25,000 files that would be needed for training was gotten first, these files are then mapped to a unique number corrisponding to it (all based upon a mapping using a vocab list that came with the data set) which was normalized to a specific length in terms of words per text file
this was done so that the model could actually use the text information, because 1) it would only work with numbers, so strings were not going to work, and 2) because the model needed a constant input size, so it had to be normalized in this way

From this step the input vector goes into the model, which consisted of a list of matrix's this was done because it was a way of compactly loading all the weights information, and it allowed for the forward feeding information through the model to be a simple process of matrix multiplying the weight matirx by the feature vector for that layer, outputing a new feature vector, this allowed the process to be fast and compact. 

This was the process of predicting, but to train we used a algorithim proved in the textbook Kent let us borrow, we did this becasue we new coming up with a custom one would be far too time consuming to undergo in our time constrants, and having a reference would allow us to be able to compare the algorithim with what we actually did so that we could check our work a whole lot easier

Finally we made and implamented a storeing and loading function for the model itself, as we knew that it would take some time for the actual training to happen, so if we needed to have a fully trained model on demand, we cant be waiting for an hour for it to be ready, thus we created the storing and loading functions to better use what we had made, and it would allow for long term storage/
##----------------Works cited----------------##
https://en.cppreference.com/w/cpp/container/map
https://cplusplus.com/reference/map/map/
https://cplusplus.com/reference/random/uniform_real_distribution/
Book: Artificial Intelligence: A Modern Approach 3rd Edition by Stuart Russell
Kent
https://www.tensorflow.org/tutorials/keras/text_classification
https://towardsdatascience.com/derivative-of-the-sigmoid-function-536880cf918e     This was used only to get a formula definition
How each of these sources were used is marked in the code in there files in the respective place were the information
gained from them was used
##----------------Detailed project description #2 ----------------##
##--Data pre-processing--##
### Steps
Processing of a single file (review) consists of 5 steps
1. Get specific file path (and name)
2. Get the contents of the file
3. Clean the contents
4. Parse contents by word
5. Map words to integers
### 1. Get file path
This step gets the file path name, sense we move through the larger file in order, ie 1,2,3... but because the file names are as followes: 0_7.txt and the second number is random (the movie score) we have to cycle through every combo of the first number, and 0-10 of the second to find and open the correct file
### 2. Get the contents of the file
This step gets the file itself in a single string from the txt
### 3. Clean the contents
This step goes through the string removing any unneeded puncuation and html leftovers
### 4. Parse contents by word
This step splits the string by words
### 5. Map words to integers
This step maps every word to an int that is predetermind by a vocab list, and puts it in a vector of ints to be sent away

##--Neural Network--##
This process takes the list of words and matrix mulitplys it by the matrix of weights, creating the first list of activations, this list is then matrix multiplied by the next matrix of weigths, and this process continues until it is down, and the output vector is the prediction of the model
For training however once it calcuates the prediction, it finds error of the output nodes which then is propogated backwards, distruputing the error backwards to all other nodes, this error is then used to calcuate the desried change to the weights, which it then applies to the weights.
This step then is applied to each and every other example in the training example list to fully train the model
//--To see the full techical algorithim we used, refer to referenceALG.jpg--\\
##----------------Manuel----------------##
Imagine a technically competent person is using your program, but knows nothing specific about it.
//---If you are predicting on a pretrained model---\\
download only as many files as you need to save time, and make sure when predicting you change the file vectors to being floats and not ints (as the model needs floats but downloading the files puts them in a format of ints) make sure you get from both pos and neg files using the getNegTrainData and getPosTrainData functions and finally make sure you load in a file that is already trained, not a blank one
//---If you are training a model---\\
make sure you intialize the model with the format 'Model m(modelInfo,(modelInfo size));' where modelinfo size is a int 
and that you remove all predicting code so that it only trains, make sure as it runs through examples (which by the way, make sure the amount of files it gets is large) that it converts them to floats so it can be used and that it runs through all the training exampels (note this will take a long time, its slow, a fully trained model on 25,000 examples took an hour to finish)
finally when it finishes training make sure you store the model into a file so it is saved
##----------------UML Diagrams----------------##

| Review |
|---|
| *Attributes* |
| - bool isPos |
| - vector<int> data |
| *Behaviors* |
| + vector<int> getData() const |
| + bool getType() |

| Matrix |
|---|
| *Attributes* |
| - vector<vector<float> > matrix |
| *Behaviors* |
| + vector<int> getData() const |
| + Matrix(int numOfrows, int numOfcolumns) |
| + Matrix(int numOfrows, int numOfcolumns, int num1) |
| + Matrix(vector<vector<float> >& mat) |
| + vector<float> operator*(vector<float>& featureVector) |
| + Matrix operator+(Matrix& otherM) |
| + vector<float> getColumnvec(int p) |

| Model |
|---|
| *Attributes* |
| - vector<Matrix> layers |
| - vector<Matrix> previousChanges |
| - float learningRate |
| - float beta1 |
| *Behaviors* |
| + Matrix getMat(int num) |
| + void addLayer(Matrix& mat) |
| + void addInfo(int in) |
| + void addChange(Matrix& mat) |
| + void resetLayers( vector<Matrix> newLayers) |
| + void resetChanges(vector<Matrix> newLayers) |
| + Model(int layerInfo[], int numOflayers) |
| + vector<float> predict(vector<float> featureVector) |
| + void storeModel(string path) |
| + void loadModel(string path) |
| + void predictWithtraining(vector<float> featureVector, vector<float> label) |
            

-