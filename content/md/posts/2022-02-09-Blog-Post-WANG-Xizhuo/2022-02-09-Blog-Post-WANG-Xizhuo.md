{:title  "Data Science in Finance - Third Blog"
 :layout :post
 :author "WANG Xizhuo"}

## Work I have done these days
- Apply strategy to real data set.

  Apply the basic delta-heding strategy to 5 years data (from 2016 to 2020). Get the evaluation and trading data i.e. daily return rate, volatility, sharpe ratio and so on. 

- Polish Clojure code.

  I spend time on documenting the code and editing functions to make it run more efficiently.  
## Difficulties I encountered
- Problem in generating the evaluation result. 

  The way that the backtesting library calculated daily return is different from my intended calculation. I recalculated in the spreedsheet. 
- Visualizing the generated data.

  I counld not visualize the return result directly from Clojure. Instead, I made the plot directly in excel.
## Heading for the next stage
- Visualize data in Clojure
  
  I will check the visualizing libraries shared in our Slack group and try to visualize the resulting data in Clojure.
- Optimizing delta

  As the topic of my research, I will adjust the calculation of delta and try to optimize delta hedging. The first step will be to take the "volatility smile" into account. 