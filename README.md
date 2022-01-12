# Predicting-Web-Page-Visits-Using-LSTM
# LSTM Theory

## Why Do we Need LSTM
LSTM are a solution to the issues that a RNN faces. **RNN face 3 main problems:**
1.  Vanishing gradient problem 
2.  Exploding gradient problem 
3. They fail to carry long term dependencies 

One of the primary reason for the failure of RNN is that the weights in RNN are same.

[Read more about the problems in RNN and how LSTM solves it](https://medium.datadriveninvestor.com/how-do-lstm-networks-solve-the-problem-of-vanishing-gradients-a6784971a577)

## Different components of LSTM
**The different components of a LSTM are:**
1. Cell state
2. Hidden State
3. Forget gate
4. Input gate
5. Output gate
6. operators

## Operators
### Point wise operator
A point wise operator simply multiplies the adjacent values of two vectors 

### Addition Operator
The addition operation will add the adjacent values of two vectors

## What is the Cell State?
Cell state is like a Highway. It lets us carry important information bypassing the mechanism of the LSTM.  When there is a context/state change information gets added or subtracted to the cell state.

## Forget Gate
The Job of a forget gate is to remove data on state change.  As soon as there is a state change we want to remove the old add. 
First we concatenate the input from the past hidden state and the current state input.

Then we pass it through a sigmoid activation function. The sigmoid pushes all the values between 0 and 1. Values closer to 0 will be forgotten from the cell state and values closer to 1 are added/remembered in the cell state.

**Lets understand why**
The pointwise operation will multiply the output of the sigmoid with the cell state. Values closer to zero reduce the value of the adjacent values in the cell state vector after multiplication and thus the cell state forgets those values.

**Note:** Here I have simply assumed that the values will be either 1 0r 0 incase of sigmoid for  making the logic simple. In reality the values are between 0 and 1

## Input Gate
After removing old unnecessary data we add the new data to cell state and the hidden state.

Lets update the cell state first. We pass the concatenated vector of previous hidden state and the current input through a sigmoid activation function. It pushes the values between 0 &1. Values closer to 1 will be added to the cell state and the current hidden state whereas values closer to 0 will not be added. 

We also pass the data through  a tanh function, it forces values between 1 and -1. Values close to 1 will have more importance and values closer to -1 will have less value. We pass the information through a tanh so that we can distribute the gradient over the network. If we don't apply a tanh then over time gradients will either explode or vanish.(values that are big will explode whereas values that  are small will vanish)

We then calculate the point wise product of both the activation function outputs and simply add it to the cell state using an addition operator.

## Output Gate
Its time to update the data in the hidden state itself. To do this we must first decide what part of the input is worth updating. For that we pass the input from a sigmoid activation function that compresses the values between 0 & 1.

Next we apply a tanh activation function to the values of the cell state. This output is passed through a pointwise operator along with the output of the sigmoid. 

This its the output to the next hidden layer
