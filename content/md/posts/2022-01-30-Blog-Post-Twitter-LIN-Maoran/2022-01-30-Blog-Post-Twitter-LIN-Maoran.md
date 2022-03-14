{:title  "Ideas about Data Processing and Getting Regression Statistics"
 :layout :post
 :author "LIN Maoran"}

Some tricks of using Clojure in dataset manipulation and regression test.

To manipulate a dataset with numerous variables and values, we could use some tricks by referring to the library tech.ml.dataset and Incanter.

1. We could not guarantee that all inputs in our dataset could be fully completed with no missing values. Therefore, I could try the built-in function “drop-missing” to remove the rows with missing data.
    ```
    (-> (ds/->dataset "resources/China-data.csv") (ds/drop-missing))
    ```

2. There are some control variables containing multiple categories. We could use the function “categorical->number” to translate them to values. If the categories are simply enough, we could also use the “categorical->one-hot” to resolve this problem.
    ```
    (-> (ds/->dataset "resources/regression-data.csv" {:key-fn keyword}) (ds/categorical->number [:Investment_Stage]))
    ```

3. We could use the regression function to have a linear-regression test for our data.

    + The regression could be done on a matrix, therefore. By doing this, we could select multiple columns in dataset as independent variables:
        ```
        (def reg-data (to-matrix (read-dataset "resources/regression-data.csv")))
        (def num-investor (sel reg-data :cols 4))
        (def x (sel reg-data :cols '(0 1 2 5 6 7 8)))
        ```
    
    + Before the regression, we could firstly use Incanter to derive a correlation-matrix and have a preliminary judgement:
        ```
        (correlation reg-data)
        ```

    + When doing the regression, we could use the “linear-model” function in incanter, which will return us a map with multiple statistical details such as t-test, p-value, r-square etc. We can use “keys” function to see what is contained in that dataset:
        ```
        (keys (linear-model num-investor x))
        ```
    
    + To make it looks more reader-friendly, we could also transfer it to a dataset by tech.ml.dataset.