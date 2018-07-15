# crypto_ml
## Capstone Proposal
Edward Ward  
June 26th, 2018 

## Proposal
_(approx. 2-3 pages)_

### Domain Background
_(approx. 1-2 paragraphs)_

In this section, provide brief details on the background information of the domain from which the project is proposed. Historical information relevant to the project should be included. It should be clear how or why a problem in the domain can or should be solved. Related academic research should be appropriately cited in this section, including why that research is relevant. Additionally, a discussion of your personal motivation for investigating a particular problem in the domain is encouraged but not required.

CryptoCurrency is a form of digital asset that operates in a 24hr, 7 day a week market. It has proven to be a highly volatile market with daily swings of >10% not uncommon. Given the nature of cryptocurrencies being native tokens on the internet there is a significant amount of quantitative data avaliable to analyze. Many people have attempted to value crypto assets with fundamental models however due to their speculative nature it has not proven very effective, for this reason I believe Machine Learning may provide a superior method of estimating future cryptocurrency prices. There are several existing studies on the subject:

* https://arxiv.org/pdf/1612.01277.pdf
*
*

Existing studies have largely focused on using simple price data to predict the movements of bitcoin relative to USD. 

### Problem Statement
_(approx. 1 paragraph)_

There are many crypto-assets one can purchase at any given time. This project aims to maximise returns against a base asset (e.g. Bitcoin, Ethereum or USD). This is an asset selection problem, an allocation of assets will be selected each trading period (24hrs), if the allocation performs better than the base asset that can be considered a succesful period however the model must be evaluated holistically since a 10 small daily gains can be wiped out by one large loss. The performance of the model should be continually evaluted over each period moving forward into the future to watch for any significant changes.


### Datasets and Inputs
_(approx. 2-3 paragraphs)_

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

### Solution Statement
_(approx. 1 paragraph)_

In this section, clearly describe a solution to the problem. The solution should be applicable to the project domain and appropriate for the dataset(s) or input(s) given. Additionally, describe the solution thoroughly such that it is clear that the solution is quantifiable (the solution can be expressed in mathematical or logical terms) , measurable (the solution can be measured by some metric and clearly observed), and replicable (the solution can be reproduced and occurs more than once).

The model can predict whether an asset will increase or decrease against the base asset greater than 50% of the time. The asset will need to be valued against the base asset and the model will predict if this value increases or decreases, if this value matches with the label then the instance will be considered a success. 

### Benchmark Model
_(approximately 1-2 paragraphs)_

In this section, provide the details for a benchmark model or result that relates to the domain, problem statement, and intended solution. Ideally, the benchmark model or result contextualizes existing methods or known information in the domain and problem given, which could then be objectively compared to the solution. Describe how the benchmark model or result is measurable (can be measured by some metric and clearly observed) with thorough detail.

### Evaluation Metrics
_(approx. 1-2 paragraphs)_

In this section, propose at least one evaluation metric that can be used to quantify the performance of both the benchmark model and the solution model. The evaluation metric(s) you propose should be appropriate given the context of the data, the problem statement, and the intended solution. Describe how the evaluation metric(s) are derived and provide an example of their mathematical representations (if applicable). Complex evaluation metrics should be clearly defined and quantifiable (can be expressed in mathematical or logical terms).

### Project Design
_(approx. 1 page)_

Data Collection: Download the data.

Data Pre-Processing: 

1. Create labels for each time period accross each asset.
2. Normalize the data
3. Add any missing features that are implicit. This includes Asset Name, percentage increase from previous day, etc.  
4. Average the data into one set upon which the model will be trained. This likely won't include all the assets since they have varying date lengths. 

Build Neural Net:

Training the model repeatedly on all the data may lead to a highly biased model since the most crypto assets are highly correlated. For this reason I believe it's a good idea to train the model on an agregated/averaged data set and then use transfer learning to implement it on each individual asset. 

I expect to use a Recurrent Neural Net and will most likely use a Multivariate LTSM model. Given that I have not found any similar models used in crytpo asset prediction I will have to experiment a lot to find a good design for the LTSM model. 




In this final section, summarize a theoretical workflow for approaching a solution given the problem. Provide thorough discussion for what strategies you may consider employing, what analysis of the data might be required before being used, or which algorithms will be considered for your implementation. The workflow and discussion that you provide should align with the qualities of the previous sections. Additionally, you are encouraged to include small visualizations, pseudocode, or diagrams to aid in describing the project design, but it is not required. The discussion should clearly outline your intended workflow of the capstone project.

-----------

**Before submitting your proposal, ask yourself. . .**

- Does the proposal you have written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Solution Statement** and **Project Design**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your proposal?
- Have you properly proofread your proposal to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced?
