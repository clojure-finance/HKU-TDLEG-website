{:title  "Data Science in Finance - Second Blog"
 :layout :post
 :author "WANG Xizhuo"}

## Work I have done these days
- Managing the option dataset

    The option dataset downloaded from the WRDS website is different from the CRSP dataset used in the backtesting library. Hence, some work is needed to make the dataset standard like formatting.  
- Settling the selection rules for option trading 

    The initial rule for filtering options is to select the options with the top five largest trading volume on a given day. Their position delta is calculated by linear combination. Then the quantity to trade is setted to make the whole position delta neutral.    
- Learning Clojure

    During the coding process, I also learned Clojure and got a deeper understanding about the data structures, especially the immutable sequences. Due to this property, we need to use `swap` and `reset` to change value. 
  
## Difficulties I encountered
- Maintain options

    Although I have walked through the `maintain-tics` function in the backtesting library, I still had no idea about how to maintain the options becuause the option dataset is different from the CRSP dataset. There are various options on the same day, not like the CRSP where there is only one ticker but on consecutive days. To solve this problem, I am thinking about maintaining another dataset for the available options and also another portfolio only for options. By combining the options with the stock and cash portfolio, we can generate the whole position value. 
- Automate trading

    Since the dataset is different, the ways to iterate to the next date may also vary. I am trying to figure out a way to iterate to the next date in the option dataset. 
  
## Heading for the next stage
- Execute automated trading

    I will try to bring the idea of maintaining options into practice and write some codes to automate trading.
- Optimizing delta

    As the topic of my research, I will adjust the calculation of delta and try to optimize delta hedging.
  