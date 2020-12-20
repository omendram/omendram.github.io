

### Introduction
The recent advancements in the field of computing power and efficient neural networks have given time series prediction a new dimension. One such neural network model is called Long Short Term Memory (LSTM). The properties of an LSTM model to retain context gives this model an edge for predicting time series data as indicated by many recent works [1]. This presents the question whether these models can be applied to the Forex market and if there is a possibility for a network to predict when to buy or sell a currency pair in order to maximize the profit. This report suggests an implementation where a range of technical indicators are used as input for an LSTM. Here it is observed that just modeling the Forex market data through an LSTM with some technical analysis is not enough to make successful buy and sell predictions. This paper also observes how training and testing in a Forex data presents drastically different results.

Due to the massive size of the Forex market, it encourages the question whether a pattern can be established in the way the market varies over time. Economists across the world have studied the behavior of the Forex market to establish mathematical patterns to predict trends (refer technical indicators). Thanks to the availability of the historic data of the Forex market, it raises the question whether one could use the methods of data science to predict market trends and hopefully make profit out of that. In this research paper, possible approaches to achieve that have been explored. Unlike regular stock exchanges, the Forex market has no daily opening and closing times. Nor does it have a single physical location. Trades are executed via software platforms and brokers that are open 24 hours a day, for 5 days a week (The market closes on Friday 5pm EST and opens again on Sunday 4pm EST).

The main research question for this project is: "Is it possible to implement a profitable Forex trading algorithm using neural networks?. The following questions will be discussed in order to find an answer to the main research question:

- What technical indicators have the most influence in determining a good buy/sell signal?
- What neural network structure works best on the Forex prediction task?

### Dataset
Forex data is publicly available in csv format.

### Network
The network is divided into two main parts, the feedforward layers and the Long Short Term Memory (LSTM)network. There are two feed forwards layers connected thatare charged with pre-processing the data before feeding itto the LSTM which should be able to find patterns in thetime series. The input for this network are the technicalindicators covering a certain input window. The output ofthe network is a Nx2 matrix where N is equal to the sizeof the input window. For each N there are 2 indicators.The first element is considered a bullish indicator (buy)and the second a bearish indicator (sell). This output canthen be interpreted in different ways to make a decision onwhether to buy, sell or do nothing. The following sectionsexplore the different ways in which the input can be fedto the network and how the output can be interpreted tocalculate the profit of the current iteration. 

<img src="https://github.com/omendram/omendram.github.io/raw/master/assets/img/bollinger-bands.png" width="500">
<img src="https://github.com/omendram/omendram.github.io/raw/master/assets/img/network.png" width="500">


MACDand RSI are examples of technical indicators used as input.Figure 2: Overview of network structure and input/outputThe size of each layer in the network can be adjusted.During testing the best performance was achieved with asmaller network consisting of around 4 nodes in the firstfeedforward layer, 8 nodes in the second feedforward layerand an LSTM size of 6.

#### Input
The input for the model is a window with a dimension of NxM where N is the size of the window and M is the number of technical indicators. One such input sequence might for example be the values for each of the 32 technical indicators over a 30 minute consecutive window, resulting in an input matrix of size 30 by 32. During training there is a variety of ways to sample these sequences from the training data and feed them to the model. The following methods were implemented and tested to see which method performs best.

#### Sequential Input Sequence
This method tries to make the most of the memory effect of the LSTM. In order to do so all the data is run sequentially for each epoch starting at a random position. A random position is chosen from the training set. All batches of the iteration will then be sampled consecutively from this random starting point in the training set. The idea here is that training batches will also have sequential information which maybe be picked up by the network to make a good prediction.

#### Random Input Sequence
After implementing and analyzing the sequential method there was a fear of overfitting the network. Therefore, a new way of inputting the data was designed. This new method, randomizes the windows used as input at every iteration. One single input will still cover a consecutive window, but the iterations will no longer loop over the training data in a sequential way. Instead, a random window is selected for each iteration. This also introduces a different way of interpreting the output that will be explained in the profit calculation section.

#### Overlapping Input Sequences
In order to more accurately represent the data as it would be used in a simulated or live trading environment, multiple input sequences might be used to feed to the model. The idea here is to take a consecutive window from the training data of size K. From this window, a subset is selected starting at index 0 with a sequence size of N. This input is then fed to the network and the output is stored in another collection. The subset is then shifted to the right by 1 minute by selecting a window starting at index 1 with a size of N. This is repeated until the training window with size K has been looped completely.

The result is a series of overlapping input sequences and their output. The output of each if these executions is then flattened to get an output sequence of size K-N. This output is similar to the way the model would be used in a live environment. The profit function is then called on this output to analyze the performance of the overlapping input sequences.

<img src="https://github.com/omendram/omendram.github.io/raw/master/assets/img/overlap_input.png" width="500">

#### Training Batches
During training the selected input method is used to sample training windows from the dataset. In order to reduce noise and allow the profit functions to operate on more data to draw a more meaningful conclusion, one single training step will have multiple batches. For the sequential input method this means that the training step will consist of $B$ sequential input windows while the random input method will have $B$ random windows in a single training step. The overlapping method also uses multiple batches consisting of flattened outputs.

#### Profit Calculations
Depending on the input method, a profit function is used to analyze the output and assign it a value that indicates the performance of the network as it currently stands. It is important to note that the implementation uses multiple batches in each update. This was done to decrease noise and increase accuracy of the model. This way, the implementation allows for the profit to be calculated for each prediction in the batch and then take the average of this profit to get the final cost for the current set of weights. The section on Particle Swarm Optimization will provide more details as to this implementation.

#### Sequential based
Since the data is sequential the trading window has a size of $N \times B$, where $N$ is the size of the window used as input of the network and $B$ the number of batches used. Profit is then calculated considering the first element of the output a bull indicator and the second a bear indicator.

Both short and long positions are allowed in this situation. A position is opened after 5 consecutive timesteps with the same indicator ON and the other OFF. The position is closed after 3 consecutive timesteps with the opposite indicator of the one used to open the position ON, regardless of the value that the opening indicator value.

#### Random based
The data found in the batches is not sequential anymore so they have to be treated separately. This means that there are $B$ trading windows. Each of the windows uses the same profit calculation algorithm and the output of the function is then the average profit over all the batches.

Short and long positions are again possible but in a different way. The first element of the output is used for long positions and the second element for short positions. Both kind of positions are opened and closed using the same algorithm.
A position is opened when an element goes from a value of 0 to 1 and closed when it goes from 1 to 0. This allows having at the same time short and long positions opened therefore, only half of the money is invested every time a position is opened.

#### Overlap based
By using multiple overlapping input windows and flattening the output a series is created that consists of buy and sell signals for each minute. For each buy signal a position is opened at the current market rate. When a sell signal occurs, the position is closed and the gross profit or loss is calculated. This is how the algorithm would be used in the live environment and therefore this approach should produce a more accurate measure of profit for the current model. When a buy signal occurs and a position is opened, all following buy signals are ignored until the position is closed by the first occurring sell signal.
