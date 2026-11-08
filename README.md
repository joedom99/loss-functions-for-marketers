# Loss Functions for Marketers

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/joedom99/loss-functions-for-marketers/blob/main/loss_functions_for_marketers.ipynb)
![Python](https://img.shields.io/badge/Python-3.10%2B-212f3f?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-preinstalled%20in%20Colab-f58235)
![Data](https://img.shields.io/badge/data-simulated-6db7ac)
![License: MIT](https://img.shields.io/badge/License-MIT-198a53.svg)

Companion notebook for the Marketing Data Science article **"Loss Functions for Marketers: How Models Decide What 'Wrong' Means"** on [blog.marketingdatascience.ai](https://blog.marketingdatascience.ai).

## What This Is

When a predictive model learns from data, it minimizes a **loss function**, the formula that decides how much each mistake costs. The loss you choose decides what the prediction aims for, and the prediction shapes the business decision built on it.

This notebook follows one fictional small online gift-box shop through the two main families of loss functions:

- **Regression losses** for predicting numbers: **squared error**, **absolute error**, **Huber loss**, and **pinball (quantile) loss**. It shows how each one produces a different forecast, how a few very large corporate orders pull squared error, and how matching the loss to an asymmetric business cost (running out vs. throwing away) lowers what the shop actually pays.
- **Classification losses** for predicting a yes or no: **log loss (cross-entropy)** and **hinge loss**. It shows which past website visitors are worth a retargeting ad, why calibrated probabilities beat yes-or-no answers when dollars are attached, and why the cutoff should come from the costs rather than from 50%.

It's a follow-up to [Objective Functions for Marketers](https://github.com/joedom99/objective-functions-for-marketers), which covered objectives for business decisions. This one covers objectives for learning from data. Gradient descent is coming in a later article.

All data is simulated with illustrative assumptions. A fixed random seed keeps the results reproducible.

## What's Inside

| File | Description |
|------|-------------|
| `loss_functions_for_marketers.ipynb` | The notebook. Runs top to bottom in Google Colab using only preinstalled libraries. |
| `figures/` | Eleven figures (fig01 to fig11), 300 dpi PNG, Country Fried Creative brand style |
| `tables/` | Seven tables as blog-ready PNG images, each with a CSV copy |
| `requirements.txt` | Libraries for running locally |

The notebook is organized into nine sections:

1. Setup (brand style plus three settings cells: `D` data, `C` costs, `L` loss settings)
2. What a loss function is (the two families)
3. Part 1: One number, four answers
4. Part 2: Big customers pull squared error
5. Part 3: When one kind of miss costs more
6. Part 4: Who should see the retargeting ad?
7. Part 5: Which kind of error hurts your business more?
8. Checking the results (28 checks, including cross-checks against scikit-learn)
9. Summary

## Key Results

With the default settings:

**Regression losses**

- **One number, four answers.** From 500 simulated orders, squared error picks the mean (\$97.63), absolute error the median (\$60.85), Huber loss \$64.40, and pinball loss at q = 0.75 the 75th percentile (\$79.66). Removing six corporate orders moves the mean by a third and the others by 1% to 2%.
- **Outliers can flip a decision.** Holiday corporate orders that the ads didn't cause push the squared-error estimate of revenue per ad dollar to \$2.59, above the \$2.22 breakeven. Absolute error (\$2.01) and Huber (\$2.10) stay below it, closer to the true \$1.80.
- **Match the loss to the costs.** When a missed order costs \$12 and a wasted box costs \$4, the cost-minimizing forecast is the 75th percentile. The pinball model preps about 116 boxes a week instead of 100 and saves about \$859 a year (10%) compared with the squared-error model, despite the worst RMSE and MAE of the four.

**Classification losses**

- **The cutoff comes from the costs.** With a \$3 ad and \$27 in margin per sale, a visitor is worth retargeting above an 11% chance of buying. That cutoff earns \$4,664 per 10,000 visitors. The default 50% cutoff earns \$650, even though it's the most accurate rule (93.7% vs. 85.8%).
- **A default hinge model can be accurate and useless.** With only about 6% of visitors buying, a hinge model trained the default way predicts that nobody buys: 93.6% accurate, \$0 profit.
- **Probabilities keep working when costs change.** A cost-weighted hinge model earns \$4,226 at a \$3 ad, but it has to be retrained for every new cost and stops retargeting anyone at \$6. The log-loss model only needs a new cutoff and stays profitable at every ad cost from \$1 to \$10.

## Related Articles

- [Objective Functions for Marketers: How Models Decide What "Best" Means](https://github.com/joedom99/objective-functions-for-marketers)
- [Is Your Marketing Model Too Accurate?](https://blog.marketingdatascience.ai/is-your-marketing-model-too-accurate-5076f5163326)
- [What Do You Mean by Mean? A Marketer's Guide to Different Types of Averages](https://blog.marketingdatascience.ai/what-do-you-mean-by-mean-a-marketers-guide-to-different-types-of-averages-52cdbf860907)
- [When the Numbers Look Wrong: A Marketer's Guide to Anomaly Detection](https://blog.marketingdatascience.ai/when-the-numbers-look-wrong-a-marketers-guide-to-anomaly-detection-3895e22f2fe7)
- [What Happens Next? Predicting Website Conversions with Logistic Regression](https://blog.marketingdatascience.ai/what-happens-next-predicting-website-conversions-with-logistic-regression-d374875764e2)
- [Why Many Marketing Models Fail: The Problem of Imbalanced Data](https://blog.marketingdatascience.ai/why-many-marketing-models-fail-the-problem-of-imbalanced-data-ceb8123b80b3)

## Author

**Joe Domaleski** is the founder of [Country Fried Creative](https://countryfriedcreative.com), a digital marketing agency in Peachtree City, Georgia. He holds an MBA from Georgia State University and an MS in Analytics from Georgia Tech, and writes about marketing and data science at [blog.marketingdatascience.ai](https://blog.marketingdatascience.ai).
