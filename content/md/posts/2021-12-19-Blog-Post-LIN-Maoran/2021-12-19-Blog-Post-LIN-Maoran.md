{:title  "Initial Ideas About the Signaling Game Model for Clojuring"
 :layout :post
 :author "LIN Maoran"}

Initial ideas about the signaling game model I wish my Clojure to simulate.

Suppose for an investment opportunity with payoff $\pi$, there are two types of firms with different profitability $\lambda_h$ and $\lambda_l$.

Considering their needs of investment $I$ for this opportunity, firms would send investment offer to investors.

Firms will try to signal investors that their quality types $\lambda$, preferably, as high-quality firms $\lambda_h$. However, the real $\lambda$ is private information and can only be estimated by investors with beliefs.

1. The investors’ beliefs about the firms’ quality could be represented by their expectation about the probability $p$ that the investment offer is sent by a low-type firm. Hence, $1-p$ represents the probability of a high-type firm.

2. For investors, their beliefs could be $\tilde{\lambda} = p\lambda_l+(1-p)\lambda_h$

During the financing process, the investors will receive their stakes $s(\pi,\tilde{\lambda})$. In debt financing, it would be the interest of loan.

Therefore, the firms and investors’ strategies and payoffs in this model would be:

1. The investors’ preferred payoff from accepting this offer would be $s(\pi,\tilde{\lambda})$, which should be $\ge$ payoff $I(1+r)$ from leaving their investments $I$ with interest rate $r$.

2. The firms’ preferred payoff from accepting this offer should be $(\lambda_h\pi)-s(\pi,\tilde{\lambda})$ or $(\lambda_l\pi)-s(\pi,\tilde{\lambda})$, which should be $\ge$ payoff $0$ from giving up.

Since the project is about the signaling effects of firms’ investment timing options, the next step to build this model is to incorporate the time-series variable $t$ and $\pi_t$ influencing the investors’ probabilistic beliefs about firms’ quality, $\tilde{\lambda}$ and $p$.
<br/>
<br/>
### Sources

Vrankić, I., & Skoko, P. (2021). The signaling game of a firm with unknown profitability and an investor. *Interdisciplinary Description of Complex Systems*, 19(3), 437-448. doi: http://dx.doi.org/10.7906/indecs.19.3.7

Wang, Q., & Kwok, Y. K. (2020). Real option signaling games of debt financing using equity guarantee swaps under asymmetric information. *International Journal of Theoretical and Applied Finance*, 23(05), 2050036.