# Predicting-Web-Page-Visits-Using-LSTM
# LSTM Theory
![LSTM3-chain](https://user-images.githubusercontent.com/22417910/149158585-08f0570b-f959-405e-b4d9-f0002b3a71c5.png)

## Why Do we Need LSTM
LSTM are a solution to the issues that a RNN faces. **RNN face 3 main problems:**
1.  Vanishing gradient problem 
2.  Exploding gradient problem 
3. They fail to carry long term dependencies 

One of the primary reason for the failure of RNN is that the weights in RNN are same.

[Read more about the problems in RNN and how LSTM solves it](https://medium.datadriveninvestor.com/how-do-lstm-networks-solve-the-problem-of-vanishing-gradients-a6784971a577)

## Different components of LSTM
![LSTM diagram](https://user-images.githubusercontent.com/22417910/149158642-8116f51a-5b79-4883-a1b0-021ac92d7f16.png)

**The different components of a LSTM are:**
1. Cell state
2. Hidden State
3. Forget gate
4. Input gate
5. Output gate
6. Operators

## Operators
### Point wise operator
A point wise operator simply multiplies the adjacent values of two vectors 

![Pointwise operator](https://user-images.githubusercontent.com/22417910/149158688-3ba1710c-1a54-40b4-a5fb-63ce9bb986a6.png)

### Addition Operator
The addition operation will add the adjacent values of two vectors

![Addition operator](https://user-images.githubusercontent.com/22417910/149158720-57d3eee0-12c3-4e43-85ca-7bca4bef5a78.png)

## What is the Cell State?
Cell state is like a Highway. It lets us carry important information bypassing the mechanism of the LSTM.  When there is a context/state change information gets added or subtracted to the cell state.

## Forget Gate
![LSTM3-focus-f](https://user-images.githubusercontent.com/22417910/149158966-4a0ac42e-696c-4f9c-b57e-5ec03286113f.png)

The Job of a forget gate is to remove data on state change.  As soon as there is a state change we want to remove the old add. 

First we concatenate the input from the past hidden state and the current state input.

![image](https://user-images.githubusercontent.com/22417910/149159034-72513cdb-52d3-4f3c-83da-dae45dfda154.png)

Then we pass it through a sigmoid activation function. The sigmoid pushes all the values between 0 and 1. Values closer to 0 will be forgotten from the cell state and values closer to 1 are added/remembered in the cell state.

![Sigmoid Activation Fucntion](https://user-images.githubusercontent.com/22417910/149159120-05907e0c-3fef-4c42-9868-81015f46e305.png)

**Lets understand why**
The pointwise operation will multiply the output of the sigmoid with the cell state. Values closer to zero reduce the value of the adjacent values in the cell state vector after multiplication and thus the cell state forgets those values.

![Drawing](https://user-images.githubusercontent.com/22417910/149159193-f66d9c67-3d84-49fc-b03f-5b8c4c184ffd.jpeg)

**Note:** Here I have simply assumed that the values will be either 1 0r 0 incase of sigmoid for  making the logic simple. In reality the values are between 0 and 1

## Input Gate
![LSTM3-focus-i](https://user-images.githubusercontent.com/22417910/149159312-6dbc3607-f26e-4de1-8d11-164847d1095c.png)

After removing old unnecessary data we add the new data to cell state and the hidden state.

Lets update the cell state first. We pass the concatenated vector of previous hidden state and the current input through a sigmoid activation function. It pushes the values between 0 &1. Values closer to 1 will be added to the cell state and the current hidden state whereas values closer to 0 will not be added. 

We also pass the data through  a tanh function, it forces values between 1 and -1. Values close to 1 will have more importance and values closer to -1 will have less value. We pass the information through a tanh so that we can distribute the gradient over the network. If we don't apply a tanh then over time gradients will either explode or vanish.(values that are big will explode whereas values that  are small will vanish)

We then calculate the point wise product of both the activation function outputs and simply add it to the cell state using an addition operator.

![Tanh](https://user-images.githubusercontent.com/22417910/149159362-18de4f64-cbf5-439f-adda-975be61eb47b.png)

## Output Gate
![LSTM3-focus-o](https://user-images.githubusercontent.com/22417910/149159387-eebfb364-50f8-4095-8e78-4930fece5ad6.png)

Its time to update the data in the hidden state itself. To do this we must first decide what part of the input is worth updating. For that we pass the input from a sigmoid activation function that compresses the values between 0 & 1.

Next we apply a tanh activation function to the values of the cell state. This output is passed through a pointwise operator along with the output of the sigmoid. 

This its the output to the next hidden layer

# Credits
**All credits to the images goes to the due authors**

- https://colah.github.io/posts/2015-08-Understanding-LSTMs/
- https://blog.mlreview.com/understanding-lstm-and-its-diagrams-37e2f46f1714?gi=4d2b131479110
- https://www.tutorialexample.com/understand-element-wise-multiplication-between-two-vector-machine-learning-tutorial/
- https://www.haroldserrano.com/blog/vectors-in-computer-graphics
- https://en.wikipedia.org/wiki/Sigmoid_function
- https://towardsdatascience.com/activation-functions-neural-networks-1cbd9f8d91d6

# Further Reading
- [Colah Blog](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [CodeEmporium](https://www.youtube.com/watch?v=QciIcRxJvsM)
- [The A.I. Hacker - Michael Phi](https://www.youtube.com/watch?v=8HyCNIVRbSU)
 
