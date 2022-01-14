{:title  "Blog Post-LIN Maoran_20220102"
 :layout :post
 :author "LIN Maoran"}

Given that the project is about the signaling effect of firms’ investing time selection, we should also incorporate $t$ to see how it affects investors’ beliefs.

The first step is making a more detailed definition about the firms’ quality $\lambda$. Suppose we have the project with the success rate $p$<sub>$0$</sub>, and failure rate $p$<sub>$i$</sub>$=1−p$<sub>$0$</sub>. It is the firm deciding at which date $t \ge 0$ it will invest. The rationale of delaying investment is to do experiment and learn about the project, the longer they need to learn, the lower quality the firms have. According to Vrankić and Skoko (2021), this learning process could be following a Poisson process with $\lambda$ as the intensity of observing a low-quality project in firms’ experiment if $\lambda \ge 0$. Hence, the higher the $\lambda$ is, the lower type the firm belongs to.

Hence, the total probability of observing a successful project in firms’ experiment before $t$ would be:

$$x(\lambda, t)=p_0+(1-p_0)e^{-\lambda t}$$

Therefore, the beliefs of firms at t about a successfully investment would be:

$$p^*(\lambda, t)=\frac{p_0}{p_0+(1-p_0)e^{-\lambda t}}$$

**1. Under symmetrical information, this belief will also be known by investors.**

In Clojure, the beliefs under symmetrical information could be denoted as:
```
(defn dilute
"The impacts of observing low quality project in learning"
    [t lamag]
(Math/exp (- 0 (* lamag t))))
(defn possible
    "the total probability of observing a successful project before t"
    [t lamag]
    (+ po (* pi (dilute t lamag))))
(defn belief
    "the beliefs of firms at t about a successfully investment"
    [t lamag]
(/ po (possible t lamag)))
```

**2. However, under asymmetrical information, the investors’ belief about the projects’ success rate should merely be determined by their beliefs $p$ about the firms’ quality in market.**

For investors, their expectation for firms to observe a successful investment project in their experiments would be:

$$\tilde{x}(\lambda, t)=p*x(\lambda_l, t)+(1-p)*x(\lambda_h, t)$$

Then, the investors beliefs about the probability of a successful investment would be:

$$\tilde{p}(t)=\frac{p_0}{\tilde{x}(\lambda, t)}$$

However, the firms’ beliefs would still be:

$$x(\lambda, t)=p_0+(1-p_0)e^{-\lambda t}$$

In Clojure, the investors’ beliefs under asymmetrical information could be denoted as:

;;lamago is the low-type firm’s quality $\lambda_h$, while lamagi is the high-type firm’s quality $\lambda_l$.
```
(def lamago 0.8)
(def lamagi 0.3)
(defn exppossible
    "The investors expected beliefs about observing a successful investment project."
    [p t]
    (+ (* p (possible lamago t)) (* (- 1 p) (possible lamagi t))))

(defn expbelief
    "the beliefs of investors at t about a successfully investment"
    [q t]
(/ po (exppossible p t)))
```

**3. Then, we could incorporate the beliefs into firms’ payoffs and benchmark.**

Here, the firms’ payoff upon a selected investing time t will be $W(\lambda, p, t)=x(\lambda, t)[p(\lambda, t)\pi-I-s(\pi, \tilde{\lambda}, t)]$. To accept the offer, this should be $\ge$ payoff $0$ from giving up.

The investors’ payoff would be: $s(\pi, \tilde{\lambda}, t)$. To accept the offer, this should be $ge$ payoff $I(1+r)^t-I$ from leaving their investment elsewhere with interest rate $r$.
The next step is to depict firms’ strategy about selecting their investment time. Ideally, since they had noticed the investors’ beliefs, firms’ will determine their optimal time $t$ based on investors’ beliefs. Then they will compare this $t$ with their benchmark to decide whether they could accept the offer.
</br>
</br>

### Sources 

Bobtcheff, C., & Levy, R. (2017). More Haste, Less Speed? Signaling through Investment Timing. *American Economic Journal: Microeconomics, 9*(3), 148–186. [http://www.jstor.org/stable/26598494 ](http://www.jstor.org/stable/26598494)

Vrankić, I., & Skoko, P. (2021). The signaling game of a firm with unknown profitability and an investor. *Interdisciplinary Description of Complex Systems*, 19(3), 437-448. doi: [http://dx.doi.org/10.7906/indecs.19.3.7 ](http://dx.doi.org/10.7906/indecs.19.3.7)