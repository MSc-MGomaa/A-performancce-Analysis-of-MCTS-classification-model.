# A-performancce-Analysis-of-MCTS-classification-model.
Hyperparameter analysis, and comparison with current  state-of-art classification algorithms.

## Main Idea
<p align="justify">
To evaluate our method, a large number of experiments were performed. As our model receives multiple hyperparameters, our goal is to examine the behavior of each parameter, and find out how sensitive our method for choosing the value of each parameter is. In the second part, the predictive-accuracy of our method will be compared to the state-of-art classification algorithms.

## Q1: Number of iterations
<p align="justify">
Due to the random simulation characteristic of MCTS, a solution is always available, which leads to what is called anytime~mining. Moreover, and due to the best-first search property that MCTS has, that solution improves over time, and converges to the optimal solution if enough time and memory capacity are given. In order to see the effect of increasing the number of iterations over the resulting predictive accuracy, different values of number of iterations will be tested while keeping the values of other parameters fixed.

### Other parameters' values
<p align="justify">
The value of minimum-support was set $10$, a small value to allow the generation of rules which cover at least 10 samples. For the M-estimate, it was set to $10$, to give a chance to the least promising nodes to be explored. As a result, more rules are expected to be generated than setting this parameter to a small value. The Jaccard-similarity takes a value $\in$ [0, 1], so it was set to 0.5.
<p align="justify">
Fig \ref{fig:test1} shows the resulting predictive accuracy when increasing the number of iterations on two datasets, $Wine$ and $Heart$ averaged over ten runs. Regardless of the $Rule Set$ configuration method, it shows a continuous increase. However, in such a case, and with the current settings, the optimal solution has not yet been reached, which means a bigger number of iterations is still needed to discover the search space. The runtime corresponding to each experiment shows an exponential growth when a bigger number of iterations is given.

<p align="center">
<img width="800" height="500" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/test1.jpg">
</p>


