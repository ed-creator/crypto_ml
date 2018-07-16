# crypto_ml
## Capstone Proposal
Edward Ward  
June 26th, 2018 

## Proposal

### Domain Background

In this section, provide brief details on the background information of the domain from which the project is proposed. Historical information relevant to the project should be included. It should be clear how or why a problem in the domain can or should be solved. Related academic research should be appropriately cited in this section, including why that research is relevant. Additionally, a discussion of your personal motivation for investigating a particular problem in the domain is encouraged but not required.

CryptoCurrency is a form of digital asset that operates in a 24hr, 7 day a week market. It has proven to be a highly volatile market with daily swings of >10% not uncommon. Given the nature of cryptocurrencies living natively on the internet there is a significant amount of open quantitative data avaliable to analyze. Many people have attempted to value crypto assets with fundamental models however due to their speculative nature it has extremely subjective. I believe Machine Learning may prove to be a strong method of estimating short term future cryptocurrency prices. There are several existing academic studies on the subject:

* https://arxiv.org/pdf/1612.01277.pdf
* https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8125674
* https://arxiv.org/pdf/1805.00558.pdf


It is also useful to look at some non-academic implementations of ML on crypto assets:

* https://hackernoon.com/dont-be-fooled-deceptive-cryptocurrency-price-predictions-using-deep-learning-bf27e4837151
* https://medium.com/@huangkh19951228/predicting-cryptocurrency-price-with-tensorflow-and-keras-e1674b0dc58a
* https://github.com/umbertogriffo/An-Experiment-On-Predicting-Cryptocurrency-Prices-With-LSTM

Existing studies have largely focused on using simple price data to predict the movements of bitcoin relative to USD with little investigation in the relationship between crypto assets. In addition to the previous machine learning research on crypto assets much of the work on traditional financial assets (& other time-series focused ML) will also be applicable since the goal of any agent will be consistent and the features will most likely be structured in a similar way. Here are some potentially applicable papers:

* https://ieeexplore.ieee.org/abstract/document/7966019/
* https://www.sciencedirect.com/science/article/abs/pii/S0377221717310652
* https://www.researchgate.net/publication/13853244_Long_Short-term_Memory

### Problem Statement

There are many crypto-assets one can purchase at any given time. This project aims to predict whether a crypto asset will increase or decrease in price relative to a chosen base asset (e.g. Bitcoin, Ethereum or USD) in the next time period. This can be used as an asset selection mechanism, an allocation of assets can be selected each trading period (24hrs), if the allocation performs better than the base asset that can be considered a succesful period however the model must be evaluated holistically since a 10 small daily gains can be wiped out by one large loss. The performance of the model should be continually evaluted over each period moving forward into the future to watch for any significant changes.


### Datasets and Inputs

Crypto assets has very good price data avaliable however more detailed & rich data about other factors id harder to find. I will primairly use https://coinmetrics.io/data-downloads/ as a data source. For each asset there is daily information on:

 * date	
 * txVolume(USD): this refers to the usd value of on-chain transactions that occured  	
 * txCount: this refers to the number of on-chain transactions that occured 	
 * marketcap(USD): total marketcap of the asset (no. of tokens * price0 	
 * price(USD): price in usd	
 * exchangeVolume(USD): volume of transactions accross all exchanges measured	
 * activeAddresses: number of addresses that have interacted with the token (on-chain) 	
 * medianTxValue(USD): median transaction value (on-chain)
 * Asset: The name of the Asset
 
The model will attempt to establish the probability of each asset performing well or poorly agaisnt the base asset for a given period. It will likely require significant data cleaning & normalization of the data, since both absolute values (e.g. marketcap) & relative daily values (% change in marketcap) may help to improve the model. I expect I will use the previous n time periods of a set of assets (including the base asset & asset being evaluated) as the feature set and use the return against the base asset as the label.     

Additional data for consideration is one off data about particular events that may provide an insight into asset performance. For example Date added to a popular exchange (e.g. Binance). This information is publically avaliable but I would have to collect the data myself if I were to use it.  

Social data as described in https://arxiv.org/pdf/1805.00558.pdf would be a very interesting addition however that is currently out of scope for this project.  

### Solution Statement

The model can predict whether an asset will increase or decrease against the base asset greater than 50% of the time. The asset will need to be valued against the base asset and the model will predict if this value increases or decreases, if this value matches with the label then the instance will be considered a success. 

The best analysis of the model will be the performance going into the future. If the model is able to beat the performance of holding the base asset alone I will consider it a success.  

### Benchmark Model

Given this is a fairly under researched topic I found it hard to establish a benchmark model using existing methods. For this reason I am choosing a simple benchmark model of what can be expected by chance based on historical data. E.g. Given the labels [0,1,1,1,1] the benchmark model will randomly select 1 (price increase) with a 80% likelyhood and 0 (price decrease) with a 20% likelyhood.

### Evaluation Metrics
_(approx. 1-2 paragraphs)_

In this section, propose at least one evaluation metric that can be used to quantify the performance of both the benchmark model and the solution model. The evaluation metric(s) you propose should be appropriate given the context of the data, the problem statement, and the intended solution. Describe how the evaluation metric(s) are derived and provide an example of their mathematical representations (if applicable). Complex evaluation metrics should be clearly defined and quantifiable (can be expressed in mathematical or logical terms).

Accuracy can be used to quantify the performance of the benchmark model & the solution model. It is straight forward to determine the correct number of predictions against the total predictions. I will also use log loss to help evaluate over & underfitting of the model. 

### Project Design

Data Collection: Download the data.

Data Pre-Processing: 

1. Create labels for each time period accross each asset.
2. Normalize the data
3. Add any missing features that are implicit. This includes Asset Name, percentage increase from previous day, etc.  
4. Average the data into one set upon which the model will be trained. This likely won't include all the assets since they have varying date lengths.

Build Benchmark Model:

Build a simple model that picks [0,1] with probability adjusted weights. Measure the accuracy of the model. 

Build Neural Net:

Training the model repeatedly on all the data may lead to a highly biased model since the most crypto assets are highly correlated. For this reason I believe it's a good idea to train the model on an one example data set(or an average of the sets).If it's practical & possible I will then use transfer learning to adapt the model for each individual asset. This will require significant more research from me since transfer learning in RNNs is not common and may not be practical.

I expect to use a Recurrent Neural Net and will most likely use a Multivariate LTSM model. Given that I have not found any similar models used in crytpo asset prediction I will have to experiment a lot to find a good design for the LTSM model. My output layer will use sigmoid activation. 


