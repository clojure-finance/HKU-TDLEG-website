{:title  "Empirical Analysis: Some Ideas about Basic Data Manipulation and Usage of Machine Learning"
 :layout :post
 :author "LIN Maoran"}

Some ideas when doing empirical analysis.

According to the mathematical model we built, we could find that there exists a negative correlation between investors’ belief and the equilibrium share ratio in the equity offer. With the lower investment confidence, which is denoted by higher q, there are higher probabilities that some equity offers would be rejected (Vrankić & Skoko, 2021). This might lead to a preliminary hypothesis that a higher share ratio in the offer might be correlated with a lower investment confidence and thus, a lower investment success ratio (Vismara, 2016).

1. We could do an empirical analysis to test this hypothesis. As is noted in Vismara (2016), the investment success could be represented by investment amount and numbers of investors. The dataset is retrieved from Refinitiv’s records about the venture capital transaction in China, 2021. Originally, the dataset contains more than 20,000 transaction details. We could thus do some trimming work using the tech.ml.dataset.

    + To choose the data in 2021, we could use the function in tech.v3.datatype to select time according their long temporal fields.
        - ```
            (-> (ds/->dataset "resources/regression-data.csv" {:key-fn keyword})
                (assoc :years (dtype-dt/long-temporal-field :years ((ds/->dataset "resources/China-data.csv" {:key-fn keyword}) :Investment_Date)))
                (ds/filter #(= 2021 (get % :years)))))
            ```
            *Note: We need to make sure our date-time type are YYYY-MM-DD, or they might not be recognized.
    
    + There are some control variables for this regression test such as companies’ industry sectors and investment stage. These variables are categorical variables which contains multiple categories. We could use the function “categorical->number” to translate them to values. If the categories are simply enough, we could also use the “categorical->one-hot” to resolve this problem.
        - ```
            (-> (ds/->dataset "resources/regression-data.csv" {:key-fn keyword})
                (ds/categorical->number [:Investment_Stage])
                (ds/categorical->number [:Company_Status])
                (ds/categorical->number [:Industry_Sector]))
            ```

2. After processing the dataset, we could firstly derive a correlation matrix of our variables to have a preliminary evaluation. We could do that using the “ds-math/correlation-table” in tech.ml.dataset. We could also do that using the “correlation” function in incanter.<br/>
![result](/posts/2022-01-30-Blog-Post-LIN-Maoran/1.jpg)

3. We could find that there is a strong negative correlation between share ratio and number of investors. We could further explore it using the regression machine learning model in tech.ml.

    + The rationale behind would be splitting our dataset into to subsets and test one with the training outcome of another. Here we could use it to predict the investment amount, but more importantly, we need to use it to explain the contribution of equity share ratio.

        - ```
            (def reg-investamt (ds-mod/set-inference-target (dissoc real-data :Num_Investors) :Disclosed_Equity_Contribution))
            (def split-amt (ds-mod/train-test-split reg-investamt))
            (def model-amt (ml/train (:train-ds split-amt) {:model-type :xgboost/regression}))
            (ml/explain model-amt)
            ```
        
        ![outcome](/posts/2022-01-30-Blog-Post-LIN-Maoran/2.jpg)

        According to its outcome, we could find that the share ratio had a significant influence to the final investment amount. This would support us to corroborate our hypothesis. Please note that, here, the gain is not the coefficient of determination Beta in OLS regression. To derive that value, the “linear-model” function in Incanter could be used.

The next step is to improve the precision of this machine learning scheme. We could use the “gridsearch” function to select the optimal model type in tech.ml library. In addition, we could also use Incanter to conduct some statistical test such as t-test, f-test etc. to further testify our hypothesis.