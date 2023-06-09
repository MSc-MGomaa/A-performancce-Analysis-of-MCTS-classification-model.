# A-performancce-Analysis-of-MCTS-classification-model.
Hyperparameter analysis, and comparison with current  state-of-art classification algorithms.

## Important Note
The following Analysis is based on the model created when implementing the topics explained in:<br>
[1 : MCTS-For-Rule-learning](https://github.com/MSc-MGomaa/MCTS-For-Rule-learning). <br>
[2 : Separate-and-Conquer-algorithm-for-pattern-set-composition](https://github.com/MSc-MGomaa/Jaccard-based-Similarity-algorithm-in-pattern-mining-tasks).<br>
[3 : Jaccard-based-Similarity-algorithm-in-pattern-mining-tasks](https://github.com/MSc-MGomaa/Jaccard-based-Similarity-algorithm-in-pattern-mining-tasks) <br>

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
On the other side, using the same settings on other datasets showed a different behaviour. The experiment was repeated on two other datasets as shown in the Figure below. After a certain point, the continuous increase showed in the figure before turns into a $choppy\_behavior$. It was expected that after a certain point (under the assumption that, this point represents the optimal solution), the continuous increase turns into a constant. Which means that increasing the number of iterations after that point will yield the same value of the $predictive accuracy$. That expectation is based on the asymmetric characteristic of $MCTS$, which allows the algorithm to favor the promising nodes, Which means, after a certain point, $MCTS$ will lead to the same areas in the search space and, as a result, retrieve the same $predictive accuracy$ value. However, that unstable behavior occurred due to the fact that each dataset has its own internal characteristics, which means that the values assigned as hyperparameters must be tuned to match the characteristics of the current dataset. An example of these hyperparameters is the $jaccard\_similarity~\theta$, increasing the $number of iterations$ yields more $rules$, and as explained in $jaccard Similarity$, the first $rule$ which is non-similar to the current $rule$ is added to the $RuleSet$. In case that $\theta$ value doesn't fit the characteristics of the current dataset, low quality $rules$ will be added to the $RuleSet$, then the resulting performance is expected to be intermittent as shown in the figure below, which reflects the importance of the hyperparamters tuning step. 

<p align="center">
<img width="700" height="300" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/test2.jpg">
</p>


## Q2: Minimum Support Value
<p align="justify">
Choosing an appropriate $minimum\_support$ value plays a vital role in both the resulting $predictive\_accuracy$ and runtime. In the section before, the value of $minimum\_support$ was set to 10, which means that, only the $rules$ that cover at least 10 samples of the given dataset are considered. This value can be considered as a small value, especially when dealing with large datasets, where it will take a long time to run each rollout step in each iteration until an infrequent rule is reached as explained in $rollout\_phase$. At the same time, a small value of $minimum\_support$ allows the discovering of valuable $rules$ during the rollout phase, which are kept in the $external\_memory$ for use in the step of forming $Rule\_Sets$.

<p align="justify">
In this section, we try to figure the effect of increasing the the minimum-support value on the resulting predictive accuracy and runtime. In the following experiments the value of $"1k"$ is used as a number of iterations. Due to the different sizes of datasets available, The range of applicable minimum-support values will take into account the size of the dataset to which they are applied. The figure below shows the experiments conducted to find out this effect. In the $Wine$ case, the max accuracy was achieved when the minimum-support = 30 using the $S\&Q$ approach, which approximately equals the accuracy value we got when the number of iterations was set to $8k$ and minimum-support = $10$. At the same time, the higher the minimum-support value, the lower the running time. At the same experiment, when the minimum-support = 40, the resulting accuracy is zero, as $MCTS$ is not able to generate the $rules$ that cover at least 40 samples. A similar performance was observed on the $Heart$ and \emph{Breast-Cancer} datasets. However, on the $Seeds$ dataset, increasing the number of iterations didn't lead to better results, as the best accuracy was achieved when the minimum-support = 10.

<p align="center">
<img width="700" height="1000" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/test3.jpg">
</p>


## Q3: M-estimate and Jaccard-similarity values
<p align="justify">
As part of the main experiments to evaluate the performance of our method on different datasets, different values of M-estimate and Jaccard-similarity will be used to see how sensitive our method is for choosing the value of each parameter.

<p align="justify">
In $table\_4.1$, 16 datasets have been selected from the UCI repository, to evaluate the performance of our method. It contains the main characteristics of each dataset, such as, the type of each dataset, the number of samples, features, and classes each dataset has. Moreover, the default values of number of iterations and minimum-support, which we considered for each dataset are defined. That consideration took into account, the type, and size of each dataset. For the M-estimate values, the range of values to be tested is $\{0.1, 0.5, 1, 5, 10, 20\}$, and $\{0.2, 0.5, 0.8\}$ for the Jaccard-similarity values, as $\theta \in [0, 1]$. 


<p align="center">
<img width="800" height="400" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/table1.png">
</p>

<p align="justify">
The results of the experiments are summarized in the tables $table\_4.2$, $table\_4.3$, and $table\_4.4$. Moreover, a graphical representation of the performance of each dataset can be seen on Fig $4.7$, and Fig $4.8$. To see how well each M-estimate and Jaccard-similarity value perform, the datasets that have achieved the maximum accuracy using each value will be counted. 

<p align="center">
<img width="850" height="400" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/table2.png">
</p>

<p align="center">
<img width="850" height="400" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/table3.png">
</p>

<p align="center">
<img width="850" height="400" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/table4.png">
</p>

<p align="center">
<img width="650" height="900" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/fig6.png">
</p>

<p align="center">
<img width="650" height="900" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/fig7.png">
</p>

<p align="justify">
Fig 4.9 summarizes the results, where in Fig 4.9.a, the maximum number of datasets that achieved the max accuracy was when M-estimate = 5, while the least number was when m = 0.1. The value of 0.1 represents a strict condition, where only the most promising nodes to be explored. On the other side, the value of 5 gives a chance to the least promising nodes to be explored. And from the results, the second technique ended up with a better performance.


<p align="center">
<img width="700" height="350" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/fig9.png">
</p>

<p align="justify">
Note, the number of datasets that are represented in Fig 4.9.a is 17, as the "Vote" dataset has achieved the max accuracy when M-estimate value = 5 and 10, so it's counted twice. However, the max accuracy value for the same dataset was achieved also when the M-estimate value = 1, but we decided to exclude it, as variance in the results is high compared to the values when M-estimate value = 5 and 10.

<p align="justify">
For the Jaccard-similarity values, Fig 4.9.b shows that, the maximum number of datasets that achieved the max accuracy was when M-estimate = 0.5, which means that, at least half of the samples that are covered by the first $rule$ need to be different from those that are covered by the second $rule$ to be called non-similar $rules$. While the least number was when M-estimate = 0.8, which is considered a large value, and not-recommended specially in case of small datasets. Note, the number of datasets that are represented in Fig 4.9.b is 13, as the remaining datasets achieved the may accuracy value using the $Separate~and~Conquer$ approach.


## Separate and Conquer (VS) Jaccard-similarity
<p align="justify">
To compare the two composition techniques we used in our method to create the $RuleSets$, the maximum accuracy value achieved by each for each dataset should be taken into account. 

<p align="justify">
Fig 4.10 shows the general performance of the two approaches, where Jaccard-similarity shows an outstanding performance, where (12 out of 16) datasets achieved maximum accuracy using this approach. When digging into the details of each dataset, we can figure that the both approaches behaved in a similar way in case of "Numerical" datasets, as shown in Fig.6, and Fig.7. However, in case of "Categorical" datasets, as shown in Fig.7 (Lymph, Mushrooms, Nursery, Tic-tac-toe, and Vote), The $S\&Q$ approach shows stable performance regardless the value of M-estimate compared to the Jaccard-similarity approach, which shows a weakness in case of small M-estimate values.


<p align="center">
<img width="800" height="500" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/Fig10.png">
</p>

<p align="justify">
However, it was noticed during the experiments that the time needed to compose a $RuleSet$ using the $S\&Q$ approach is quite large compared to the one needed when using the Jaccard-similarity approach. That happened due to the fact that, in each iteration, the $S\&Q$ has to find the $rule$ that best describe the current shape of the dataset, which requires the evaluation of all the $rules$ to select the best. On the other side, when using the Jaccard-similarity approach, that sorting is done just for once, and then the similarity equation is used to to add the remaining $rules$ to the $RuleSet$.

## MCTS (VS) State-of-art Classification algorithms
<p align="justify">
To evaluate the general performance of our method, a comparison was made with four algorithms available in WEKA: RIPPER (JRIP), PART, J48 and Random-forest. The maximum accuracy achieved by our method for each dataset will be used as a representative of the performance of our method. The comparison is summarized in table 4.5,  where a competitive performance of our method can be observed. For a better representation of the results in in table 4.5, the results were visualized in Fig 12, where the performance of our method against each state-of-art classification algorithm is plotted independently.


<p align="center">
<img width="800" height="500" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/table5.png">
</p>

<p align="justify">
Fig 12.a compares between our method and the RIPPER approach. A distinctive performance by our method can be observed, where 10 out of 16 datasets have achieved better performance using our approach. For the datasets, where the resulting accuracy is lower than the RIPPER, that difference in accuracy can be justified by the number of iterations that was set to that dataset, specially almost all datasets that showed a better performance using RIPPER are large Numerical-type datasets, such as "Ionosphere" or "Wine", where the a bigger number of iterations was needed to discover the search space.

<p align="justify">
When comparing that performance with J48, PART, and Random-forest as shown in Fig 12.b, Fig 12.c, and Fig 12.d, We note that the number of datasets that achieved better results using these methods is larger compared to our method. However, In the case of J48, the variance between the results achieved using this approach and our method is very small in many cases. And the same is applied for PART. Whereas in the case of Random-Forest, this variance increases, which reflects the characteristic performance of Random-Forest.

<p align="center">
<img width="700" height="600" src="https://github.com/MSc-MGomaa/A-performancce-Analysis-of-MCTS-classification-model./blob/main/Fig12.png">
</p>

At the same time, when all the results are combined together, we notice that the datasets that our method showed weakness in the case of RIPPER are the same in every other algorithm, Confirming our assumption that the number of iterations assigned to these datasets were not sufficient, as these datasets needed to be more explored.






