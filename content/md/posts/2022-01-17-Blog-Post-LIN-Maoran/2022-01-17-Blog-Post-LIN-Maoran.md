{:title  "Blog Post-LIN Maoran_20220117"
 :layout :post
 :author "LIN Maoran"}

Some Concessions I made.

When constructing my game model, I found that I was too ambitious when trying to incorporate time series factors and what I had done just made the whole model too intricate for me. Hence, I made some concession and returned to my initial signaling model. It was the model proposed by R. Gibbons (1992) about the signaling effects of firms’ equity share offer when seeking for financing.

As is noted in Gibbons (1992), we could assume there were two types of firms with profitability $\pi$: $H$ and $L$. To attract investment $I$ for a project with Revenue $R$, firms could provide an equity share $0 \le s \le 1$ offer for their investors. n Clojure, initially, I was using some random data.
```
(def exogenous (ds/->dataset "resources/raw-data.csv"))
(def I (atom (nth (exogenous "I") 0)))
(def R (atom (nth (exogenous "R") 0)))
    (def rate (atom (nth (exogenous "r") 0)))
    (def H (atom (nth (exogenous "H") 0)))
(def L (atom (nth (exogenous "L") 0)))
```

*Here I was using atom to make these data mutable. I will do numerous tests afterwards. This will give me more flexibility in experimentation.

This project should have more attractiveness than investing elsewhere, which is revealed in:

$$ R \ge I (1 + r) $$

1. Therefore, for firms’ benchmark, their net profit after the offer should be larger than rejecting this project and continuing their own works.

$$ (1 - s)(\pi + R) \ge \pi $$

$$s \le \frac{R}{(\pi + R)}$$
```
(defn benchmark-firm
"The firms' benchmark of s" [P] (/ @R (+ @R P)))
```
2. For investors’ benchmark, with beliefs that there is probability $q$ that the offer was sent by a low-type firm, their stakes should be larger than investing elsewhere. Hence:

$$s \ge \frac{I (1 + r)}{(qL + (1 - q)H + R)} = f(q)$$
```
(defn benchmark-investor
"The firms' benchmark of s" [q]
(/ (* @I (+ 1 @rate)) (+ (* q @L) (* (- 1 q) @H) @R)))
```

3. Hence, the firms will decide to accept or reject the offer according to investors’ belief and benchmark $f(q)$. If investors’ benchmark exceeds their own benchmark, then they will reject the offer.
```
(defn cond-test-high [q] (cond (< (benchmark-firm @H) (benchmark-investor q)) "Reject the Offer." :else (benchmark-investor q)))
```

We could also do it for low type firms, and compare whether there is a pooling or separating equilibrium.
```
(defn outcome [a b] (if (and (number? a) (number? b)) "pool" "separate"))
```

*Here, I did not compare whether $a=b$ (they should be the same if both types of firms accept the offer). The programming calculation was too precise that even an ignorable different could be evaluated as separate. Therefore, when getting the outcome, comparing whether they are the same datatype will be handier for me to get the “real” separating equilibrium.

4. Then I could start my experimentation with different beliefs $q$ using *tech.ml.dataset*.
```
(ds/write! (assoc (ds/->dataset "resources/test-data.csv") "q" (range 0 1.005 0.005)) "resources/test-data.csv")
(def test-data (ds/->dataset "resources/test-data.csv"))
(-> test-data
    (assoc (str "R") @R) (assoc (str "I") @I) (assoc (str "r") @rate) (assoc (str "H") @H)
    (assoc (str "L") @L) (ds/write! "resources/test-outcome.csv"))
(-> (ds/->dataset "resources/test-outcome.csv")
    (assoc (str "equilibrium-high") (for [q ((ds/->dataset "resources/test-outcome.csv") "q") :let [outcome-high (cond-test-high q)]] outcome-high))
    (assoc (str "equilibrium-low") (for [q ((ds/->dataset "resources/test-outcome.csv") "q") :let [outcome-low (cond-test-low q)]] outcome-low))
    (ds/write! "resources/test-outcome.csv"))
(-> (ds/->dataset "resources/test-outcome.csv") (assoc (str "outcome") (for
    [high ((ds/->dataset "resources/test-outcome.csv") (str "equilibrium-high"))
    low ((ds/->dataset "resources/test-outcome.csv") (str "equilibrium-low"))
    :let [outcome (outcome high low)]] outcome))
    (ds/write! "resources/test-outcome.csv"))
(println (ds/head (ds/->dataset "resources/test-outcome.csv")))
```

5. I could also visualize my data using *tech-viz*.<br/>
![data visualization](/posts/2022-01-17-Blog-Post-LIN-Maoran/1.jpg)

```
(as-> (ds/->dataset "resources/test-outcome.csv") test-outcome
(ds/mapseq-reader test-outcome)
(vega/scatterplot test-outcome "q" "equilibrium-low"
    {:title "Equilibrium"
    :label-key "equilibrium-high"
    :background "white"})
(vega/vega->svg-file test-outcome "resources/outcome.svg"))
```

*Here, since *tech.viz* has the Label-key function, I could use different labels to discern under which $q$ there will be a separating equilibrium. According to Vrankić and Skoko (2021), since in this model, the separating equilibrium would happen when high-type firms rejecting the offer, we could differentiate the equilibrium situation using high-type firms’ equilibrium as label.

6. Multiple experimentation was made. Since the exogenous variables were denoted using atom, they became easily convertible using reset or swap.
```
(let [max 29] (loop [n 1] (if (= n max) (println "Done!")
(do (reset! R (nth (exogenous "R") n)) (reset! I (nth (exogenous "I") n))
(reset! rate (nth (exogenous "r") n))
…. (recur (inc n))))))
```

That’s how I constructed a simple signaling game model. The next step is to test this model using real data. The tentative plan is to use tech.ml.dataset to do data manipulation and try to resolve the regression problems using *scicloj.ml*. I should also have further literature review to gear myself up with more game model knowledges.
<br/>
<br/>

### Source
Gibbons, R. (1992). Game Theory for Applied Economists. Princeton: Princeton University Press.

Vrankić, I., & Skoko, P. (2021). The signaling game of a firm with unknown profitability and an investor. *Interdisciplinary Description of Complex Systems*, 19(3), 437-448. doi: http://dx.doi.org/10.7906/indecs.19.3.7