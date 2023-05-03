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
The figure below shows the resulting predictive accuracy when increasing the number of iterations on two datasets, $Wine$ and $Heart$ averaged over ten runs. Regardless of the $Rule Set$ configuration method, it shows a continuous increase. However, in such a case, and with the current settings, the optimal solution has not yet been reached, which means a bigger number of iterations is still needed to discover the search space. The runtime corresponding to each experiment shows an exponential growth when a bigger number of iterations is given.

<p align="center">
<img width="700" height="500" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/test1.jpg">
</p>

<p align="justify">
On the other side, using the same settings on other datasets showed a different behaviour. The experiment was repeated on two other datasets as shown in the Figure below. After a certain point, the continuous increase showed in the figure before turns into a $choppy behavior$. It was expected that after a certain point (under the assumption that, this point represents the optimal solution), the continuous increase turns into a constant. Which means that increasing the number of iterations after that point will yield the same value of the $predictive accuracy$. That expectation is based on the asymmetric characteristic of $MCTS$, which allows the algorithm to favor the promising nodes, Which means, after a certain point, $MCTS$ will lead to the same areas in the search space and, as a result, retrieve the same $predictive accuracy$ value. However, that unstable behavior occurred due to the fact that each dataset has its own internal characteristics, which means that the values assigned as hyperparameters must be tuned to match the characteristics of the current dataset. An example of these hyperparameters is the $jaccard\_similarity~\theta$, increasing the $number of iterations$ yields more $rules$, and as explained in $jaccard Similarity$, the first $rule$ which is non-similar to the current $rule$ is added to the $RuleSet$. In case that $\theta$ value doesn't fit the characteristics of the current dataset, low quality $rules$ will be added to the $RuleSet$, then the resulting performance is expected to be intermittent as shown in the figure below, which reflects the importance of the hyperparamters tuning step. 

<p align="center">
<img width="700" height="300" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/test2.jpg">
</p>







