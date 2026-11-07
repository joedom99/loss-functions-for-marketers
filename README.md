# Loss Functions for Marketers

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/joedom99/loss-functions-for-marketers/blob/main/loss_functions_for_marketers.ipynb)
![Python](https://img.shields.io/badge/Python-3.10%2B-212f3f?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-preinstalled%20in%20Colab-f58235)
![Data](https://img.shields.io/badge/data-simulated-6db7ac)
![License: MIT](https://img.shields.io/badge/License-MIT-198a53.svg)

Companion notebook for the Marketing Data Science article **"Loss Functions for Marketers: How Models Decide What 'Wrong' Means"** on [blog.marketingdatascience.ai](https://blog.marketingdatascience.ai).

## What This Is

When a predictive model learns from data, it minimizes a **loss function**, the formula that decides how much each mistake costs. The loss you choose decides what the forecast aims for, and the forecast shapes the business decision built on it.

This notebook follows one fictional small online gift-box shop and fits the same data with four losses: **squared error**, **absolute error**, **Huber loss**, and **pinball (quantile) loss**. It shows how each one produces a different forecast, how a few very large corporate orders pull squared error, and how matching the loss to an asymmetric business cost (running out vs. throwing away) lowers what the shop actually pays.

It's a follow-up to [Objective Functions for Marketers](https://github.com/joedom99/objective-functions-for-marketers), which covered objectives for business decisions. This one covers objectives for learning from data. Gradient descent is coming in a later article.

All data is simulated with illustrative assumptions. A fixed random seed keeps the results reproducible.

## What's Inside

| File | Description |
|------|-------------|
| `loss_functions_for_marketers.ipynb` | The notebook. Runs top to bottom in Google Colab using only preinstalled libraries. |
| `figures/` | Seven figures (fig01 to fig07), 300 dpi PNG, Country Fried Creative brand style |
| `tables/` | Six tables as blog-ready PNG images, each with a CSV copy |
| `requirements.txt` | Libraries for running locally |

The notebook is organized into nine sections:

1. Setup (brand style plus three settings cells: `D` data, `C` costs, `L` loss settings)
2. What a loss function is
3. Part 1: One number, four answers
4. Part 2: Big customers pull squared error
5. Part 3: When one kind of miss costs more
6. Part 4: Which kind of error hurts your business more?
7. Loss functions you'll meet elsewhere (log loss and a pointer to gradient descent)
8. Checking the results (20 checks, including a cross-check against scikit-learn)
9. Summary

## Key Results

With the default settings:

- **One number, four answers.** From 500 simulated orders, squared error picks the mean (\$97.63), absolute error the median (\$60.85), Huber loss \$64.40, and pinball loss at q = 0.75 the 75th percentile (\$79.66). Removing six corporate orders moves the mean by a third and the others by 1% to 2%.
- **Outliers can flip a decision.** Holiday corporate orders that the ads didn't cause push the squared-error estimate of revenue per ad dollar to \$2.59, above the \$2.22 breakeven. Absolute error (\$2.01) and Huber (\$2.10) stay below it, closer to the true \$1.80.
- **Match the loss to the costs.** When a missed order costs \$12 and a wasted box costs \$4, the cost-minimizing forecast is the 75th percentile. The pinball model preps about 116 boxes a week instead of 100 and saves about \$859 a year (10%) compared with the squared-error model.
- **The most accurate model isn't the cheapest.** The pinball model has the worst RMSE and MAE of the four and the lowest business cost.
- **The cost ratio picks the quantile.** Across six cost ratios, the lowest-cost quantile tracks the ratio within 0.025.

## Related Articles

- [Objective Functions for Marketers: How Models Decide What "Best" Means](https://github.com/joedom99/objective-functions-for-marketers)
- [Is Your Marketing Model Too Accurate?](https://blog.marketingdatascience.ai)
- [The Cobra Effect: When Marketing Metrics Bite Back](https://blog.marketingdatascience.ai/the-cobra-effect-when-marketing-metrics-bite-back-d4ac686c1b8d)
- [A Marketer's Guide to Calculus](https://blog.marketingdatascience.ai/a-marketers-guide-to-calculus-9ced95758447)
- [Is It Worth It? How to Run a Cost-Benefit Analysis for Better Marketing Decisions](https://blog.marketingdatascience.ai/is-it-worth-it-how-to-run-a-cost-benefit-analysis-for-better-marketing-decisions-5a8dd38216e2)

## Author

**Joe Domaleski** is the founder of [Country Fried Creative](https://countryfriedcreative.com), a digital marketing agency in Peachtree City, Georgia. He holds an MBA from Georgia State University and an MS in Analytics from Georgia Tech, and writes about marketing and data science at [blog.marketingdatascience.ai](https://blog.marketingdatascience.ai).
