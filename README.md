# MarketingPlanning_LR

A few important questions this project is seeking to address:

1. Is there a realtionship between advertising budget and sales?
2. How strong is relationships between budget and sales?
3. Which media contribute to sales?
4. How accuratelly we can predict future sales?
5. Is there synergy effect among the advertising media?
   
Lets see at pairplot that shows a relationship between advertising budget and sales.

[!](pics/pairplot.png)

We should conlcude that there is strong positive association between TV and Sales. 

Lets start with Simple Linear Regression

Using TV expedenture as a predictor

[!](pics/TV_regr_Sales.png)

## TV advertising:

|           | coeff  | stand err |    t   | P > t | 0.025 | 0.975 |
|-----------|--------|-----------|:------:|-------|-------|-------|
| intercept | 7.0326 | 0.458     | 15.360 | 0.000 | 6.130 | 7.935 |
| TV        | 0.0475 | 0.003     | 17.668 | 0.000 | 0.042 | 0.053 |

Therefore we can conclude that with absence of any advertising, sales will on average fall somewhere between 6130 and 7935 units. Furthermore, in every $1000 increase in TV advertising there will be an average increase in sales between 42 and 53 units.

I also can perform Hypothesis Test on coefficients. Lets set null Hypothesis and alternative Hypothesis:

$$
\begin{array}{c}
H_0:There\ is\  no\  realtionship\ between\ TV\ and\  Sales \\

H_1:There\ is\  some\  realtionship\ between\ TV\ and\  Sales\\\\
\end{array}
$$

So, since TV coefficient is not equal 0, and small p-value indicates that it is unlikely to observe substantianal asocciation between predictor and target just by chance, I can reject null Hypothesis.

Lets access model perfomance:

| Quality | Value |
|---------|-------|
| RSE     | 3.26  |
| R^2     | 0.61  |
| F-stat  | 312   |

Since, RSE=3.26 than means that any prediction based on TV advertising will be off by 3260 units on avarege, and R^2 is not explained enough variances, I need to examine relationship between other predictors.

## Radio advertising:

|           |  coeff | stand err |    t   |  P>t  | 0.025 |  0.975 |
|:---------:|:------:|:---------:|:------:|:-----:|:-----:|:------:|
| intersept | 9.3116 |   0.563   | 16.542 | 0.000 | 8.202 | 10.422 |
|   Radio   | 0.2025 |   0.020   |  9.921 | 0.000 | 0.162 |  0.243 |

In every $1000 increase in Radio advertising there will be an average increase in sales in 202 units.

## Newspaper advertising:

|           |  coeff  | stand err |   t   |  P>t  |  0.025 |  0.975 |
|:---------:|:-------:|:---------:|:-----:|:-----:|:------:|:------:|
| intersept | 12.3514 |   0.621   | 9.876 | 0.000 | 11.126 | 11.126 |
|   Radio   |  0.0547 |   0.017   | 3.300 | 0.000 |  0.022 |  0.087 |

In every $1000 increase in Newspaper advertising there will be an average increase in sales in 54 units.

Lets try mutliple linear regression.


## TV + Radio + NewsPaper

|           |  coeff | stand err |   t   |   P>t  | 0.025 | 0.975 |
|:---------:|:------:|:---------:|:-----:|:------:|:-----:|:-----:|
| intersept | 2.9389 |   0.3119  |  9.42 |  0.000 | 2.324 | 3.554 |
|     TV    |  0.046 |   0.0014  | 32.81 |  0.000 | 0.043 | 0.049 |
|   Radio   |  0.189 |   0.0086  | 21.89 |  0.001 | 0.172 | 0.206 |
| Newspaper | −0.001 |   0.0059  | −0.18 | 0.8599 | 0.013 | 0.011 |

This reveals that NewsPaper does not effect Sales, but in single regression it does.

Lets see correaltion between predictors:

![](https://github.com/evgenygrobov/MarketingPlaninig_LR/blob/main/pics/Heatmap.png)


The correlation between Radio and Newspaper is 0.35, it suggest that Newspaper is surrogate of the Radio advertising, the newspaper gets credits on effect of radio on sales.

Lets evaluate model perfomance:

| Quality | Value |
|---------|-------|
| RSE     | 1.69  |
| R^2     | 0.897 |
| F-stat  | 570   |

This prediction based on TV+Radio+NewsPaper will be still of by 1690 units.

Lets see at plot

[!](pics/Regr_Sales~Radio+TV.png)

It suggest a synergy interaction effect between advertising media.

## TV+Radio +TV*Radio

|           |  coeff | stand err |    t   |  P>t  | 0.025 | 0.975 |
|:---------:|:------:|:---------:|:------:|:-----:|:-----:|:-----:|
| intersept | 6.7502 |   0.248   | 27.233 | 0.000 | 6.261 | 7.239 |
|     TV    | 0.0191 |   0.002   | 12.699 | 0.000 | 0.016 | 0.022 |
|   Radio   | 0.0289 |   0.002   |  3.241 | 0.001 | 0.011 | 0.046 |
|  TV*Radio | 0.0011 |  5.24e-05 | 20.727 | 0.001 | 0.001 | 0.001 |

R^=0.968 that is improves model perfomance. 

Sales=6.7502 + $1000* (TV) + $1000*(Radio) + $1000*(TV*Radio)
