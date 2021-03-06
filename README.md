# Generate_TV_Scripts
Udacity Deep Learning Nanodegree Project #3.

* This repo is about how to generate your own TV Scripts using Recurrent Neural Networks.
* It is implemented by using PyTorch library.
* You can refer to Original Udacity repo [here](https://github.com/udacity/deep-learning-v2-pytorch/tree/master/project-tv-script-generation)

# Project Synopsis

Using the partially provided Seinfield dataset along with Deep Neural Network Algorithms we can generate a new TV Script though that may not exactly look like the Original Script.

# Project Objective

The objective of this Project is to Generate our own Seinfeld TV scripts using RNNs.The input data given is a Seinfeld dataset of scripts from 9 seasons.The Neural Network that we will build will generate a new ,"fake" TV script, based on patterns it recognizes in the given training data.

# Table Of Contents

* Introduction
* Data Description
* Data Pre-Processing
* Building The Neural Network
* Training The Neural Network
* Model Results
* Model Implementation
* Installation

# Introduction

Writing scripts for a TV program is a mundane task.Imagine writing every word which comes out from every character in a movie or a tv drama inorder to generate a complete script.Instead of writing manually,here we are going to generate a TV script using Long Short Term Memory Networks – usually just called “LSTMs” – which are a special kind of RNN,capable of learning long-term dependencies.As These networks are capable of predicting and generating the next words that we are intended to generate sequentially in the script.We will train these networks by feeding them an existing TV script.Once the networks are trained we will generate a new TV script.

## LSTMs
I used LSTMs networks to generate a TV script, which is a special type of Recurrent neural network. Our training data is a small subset of Seinfield Dataset.Seinfield is a TV series having 9 seasons.The dataset contains the conversation between various characters.In this case,I used Recurrent Neural Network(RNN) implemented in PyTorch.

# Data Description

Here we are provided with a small subset of Seinfield Dataset.Seinfield is a TV series having 9 seasons.The dataset contains the conversation between various characters.

# Data Pre-Processing
## Implemented The Following Pre-Processing Functions On The Dataset

### Lookup Table
* Created a Lookup Table with two dictionaries (Word to ID and ID to Word) used for word embeddings
### Tokenize Punctuation
* Splitted the scripts into word arrays and implemented a function for tokenizing punctuation.The punctuation becomes like another word in the word array. This makes it easier     for the RNN to predict the next word.

# Building The Neural Network
## Implemented the following functions as core components for building the RNN

### Batching The Data
* Implemented the batch_data function to batch words data into chunks of size batch_size using the TensorDataset and DataLoader classes.
### Creating Data Loaders
* Created Data Loaders after creating feature_tensors and target_tensors of the correct size and content for a given sequence_length.
### Initializing RNN Model And Defining Layers
* Implemented an RNN using PyTorch's [Module Class](https://pytorch.org/docs/master/nn.html#torch.nn.Module).Here we may choose to use a GRU or an LSTM.To complete the RNN,       we will have to implement the following functions for the class:
#### __init__ - The Initialize Function.
* The initialize function will set the class variables output_size,hidden_dim,n_layers and creates by defining the model layers of the neural network which are embedding_dim and   LSTM and Linear layer which will save them to the class.
#### forward - Forward Propagation Function.
* The forward function is implemented by setting the batch_size,by defining embeddings and lstm_out layers,stacking all the lstm outputs,by calculating fully-connected layer       output,by reshaping the fully-connected layer output to be batch size first,by getting the last batch of labels and finally getting one batch of output word scores and the       hidden state.
* The output of the model should be the last batch of word scores after a complete sequence has been processed.That is,for each input sequence of words, we only want to output     the word scores for a single, most likely, next word.
#### init_hidden - The Initialization Function For An LSTM/GRU Hidden State
* Here we define the hidden state weights and initialize hidden state with zero weights,and move them to GPU for training if available.
### Applying Forward And Back Propogation
* Here we implement this function after Creating new variables for the hidden state(variables in tuple form),by accumulating zero gradients,moving the input and output tensors
  to train them on GPU,if it's available,get the output for input and hidden state from the model,calculate the loss,perform a back propagation step,clip gradients in order to     prevent "exploding gradients" problem,update the weights using optimization function and finally get the average loss over a batch and the hidden state.
* Or in simple terms we can say that,Here we use the RNN class that was implemented to apply forward and back propagation.This function will be called,iteratively,in the           training loop and it should return the average loss over a batch and the hidden state.

# Training The Neural Network
* Setting the hyperparameters which are sequence_length,batch_size,n_layers,learning_rate,embedding_dim,hidden_dim,num_epochs etc for optimal loss values.

# Model Results
* After Training the Neural Network on the preprocessed data,the model achieved a loss rate of 3.16(which is < 3.5) after 10 epochs.

# Model Implementation
* The trained and saved Neural Network was then used to generate a new, "fake" Seinfeld TV script.

# Topics Related To The Project
* Recurrent Neural Networks
* Tensorflow
* Forward And Backward Propogation
* Embeddings
* Word2Vector

# Installation
## a.Installation

Download Anaconda

|        | Linux | Mac | Windows | 
|--------|-------|-----|---------|
| 64-bit | [64-bit (bash installer)][lin64] | [64-bit (bash installer)][mac64] | [64-bit (exe installer)][win64]
| 32-bit | [32-bit (bash installer)][lin32] |  | [32-bit (exe installer)][win32]

[win64]: https://repo.anaconda.com/archive/Anaconda3-2018.12-Windows-x86_64.exe
[win32]: https://repo.anaconda.com/archive/Anaconda3-2018.12-Windows-x86.exe
[mac64]: https://repo.anaconda.com/archive/Anaconda3-2018.12-MacOSX-x86_64.sh
[lin64]: https://repo.anaconda.com/archive/Anaconda3-2018.12-Linux-x86_64.sh
[lin32]: https://repo.anaconda.com/archive/Anaconda3-2018.12-Linux-x86.sh

**Install** [Anaconda](https://docs.anaconda.com/anaconda/install/) on your machine.Detailed instructions:

## b.Create And Activate The Environment

Please go though this [doc](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) before you creating an environment.
After that create a environment using following command

```
conda create --name deep-learning
```

Then activate the environment using following command

```
activate deep-learning
```

#### Git And Version Control
These instructions also assume you have `git` installed for working with Github from a terminal window,but if you do not,you can download that first with the command:
```
conda install git
```

**Now, You Can Create A Local Version Of The Project**

1. Clone the repository,and navigate to the downloaded folder.This may take a minute or to clone due to the included image data.
```
git clone https://github.com/nanditaradha/Project_Tv_Script_Generation.git
cd TV-Script-Generation
```

2. Install PyTorch and torchvision;this should install the latest version of PyTorch.
	
	- __Linux__ or __Mac__: 
	```
	conda install pytorch torchvision -c pytorch 
	```
	- __Windows__: 
	```
	conda install pytorch -c pytorch
	pip install torchvision
	```

3. Install a few required pip packages,which are specified in the requirements text file (including OpenCV).
```
pip install -r requirements.txt
```
Or
```
conda install --yes --file requirements.txt
```

4. That's it!,Now run the project using following command, check your default browser and open dlnd_tv_script_generation.ipynb file

```
jupyter notebook
```







