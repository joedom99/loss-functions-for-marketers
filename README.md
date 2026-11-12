# Loss Functions for Marketers

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/joedom99/loss-functions-for-marketers/blob/main/loss_functions_for_marketers.ipynb)
![Python](https://img.shields.io/badge/Python-3.10%2B-212f3f?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-preinstalled%20in%20Colab-f58235)
![Data](https://img.shields.io/badge/data-simulated-6db7ac)
![License: MIT](https://img.shields.io/badge/License-MIT-198a53.svg)

Companion notebook for the Marketing Data Science article **"Loss Functions for Marketers: How Models Decide What 'Wrong' Means"** on [blog.marketingdatascience.ai](https://blog.marketingdatascience.ai).

## What This Is

When a predictive model learns from data, it minimizes a **loss function**, the formula that decides how much each mistake costs. The loss you choose decides what the prediction aims for, and the prediction shapes the business decision built on it.

This notebook follows one fictional small online gift-box shop through two common families of loss functions:

- **Regression losses** for predicting numbers on a scale, often continuous, like revenue, or counts, like weekly orders: **squared error**, **absolute error**, **Huber loss**, and **pinball (quantile) loss**. It shows how each one produces a different forecast, how a few very large corporate orders pull squared error, and how matching the loss to an asymmetric business cost (running out vs. throwing away) lowers what the shop actually pays.
- **Classification losses** for predicting categories, either binary (buy or don't buy) or one of several. The notebook uses the binary case: **logistic regression** (log loss, also called cross-entropy) and a **support vector machine** (hinge loss). It shows which past website visitors are worth a retargeting ad, why honest, detailed probabilities beat yes-or-no answers when dollars are attached, and why the cutoff should come from the costs rather than from 50%.

It's a follow-up to [Objective Functions for Marketers](https://blog.marketingdatascience.ai/objective-functions-for-marketers-how-models-decide-what-best-means-b737f1705d6b), which covered objectives for business decisions. This one covers objectives for learning from data. Gradient descent is coming in a later article.

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
3. Part 1: One number, four answers (the baseline model)
4. Part 2: Big customers pull squared error (simple linear regression)
5. Part 3: When one kind of miss costs more (quantile regression)
6. Part 4: Who should see the retargeting ad? (logistic regression vs. support vector machines)
7. Part 5: Which kind of error hurts your business more?
8. Checking the results (29 checks: 12 math checks that should hold under any settings and 17 simulation results)
9. Summary

## Article Figure and Table Numbers

The file names follow the notebook's order, which differs from the article's numbering. Figures 1, 3, and 6 and Table 1 in the article are conceptual diagrams, so they aren't in this repo. A few files appear only in the notebook.

| Article | File |
|---------|------|
| Figure 2 | `figures/fig01_loss_shapes.png` |
| Figure 4 | `figures/fig02_total_loss_curves.png` |
| Figure 5 | `figures/fig03_fits_with_outliers.png` |
| Figure 7 | `figures/fig05_cost_by_quantile.png` |
| Figure 8 | `figures/fig08_classification_loss_shapes.png` |
| Figure 9 | `figures/fig09_probabilities_vs_scores.png` |
| Figure 10 | `figures/fig10_profit_by_cutoff.png` |
| Figure 11 | `figures/fig11_profit_by_ad_cost.png` |
| Table 2 | `tables/table01_one_number_four_answers` |
| Table 3 | `tables/table02_revenue_per_ad_dollar` |
| Table 4 | `tables/table03_forecast_decisions` |
| Table 5 | `tables/table04_accuracy_vs_cost` |
| Table 6 | `tables/table05_retargeting_decisions` |
| Table 7 | `tables/table06_which_error_hurts` |
| Notebook only | `fig04_outlier_influence`, `fig06_cost_by_loss`, `fig07_best_quantile_by_cost_ratio`, `table07_summary` |

## Key Results

With the default settings:

**Regression losses**

- **One number, four answers.** From 500 simulated orders, squared error picks the mean (\$97.63), absolute error the median (\$60.85), Huber loss \$64.40, and pinball loss at q = 0.75 the 75th percentile (\$79.66). Removing six corporate orders moves the mean by a third and the others by 1% to 2%.
- **Outliers can flip a decision.** Holiday corporate orders that the ads didn't cause push the squared-error estimate of revenue per ad dollar to \$2.59, above the \$2.22 breakeven. Absolute error (\$2.01) and Huber (\$2.10) stay below it, closer to the true \$1.80.
- **Match the loss to the costs.** When a missed order costs \$12 and a wasted box costs \$4, the cost-minimizing forecast is the 75th percentile. The quantile regression model preps about 116 boxes a week instead of 100 and saves about \$859 a year (10%) compared with the squared-error model, despite the worst RMSE and MAE of the four.

**Classification losses**

- **The cutoff comes from the costs.** With a \$3 ad and \$27 in margin per sale, a visitor is worth retargeting above an 11% chance of buying. That cutoff earns \$4,664 per 10,000 visitors. The default 50% cutoff earns \$650, even though it's the most accurate rule (93.7% vs. 85.8%).
- **A default support vector machine can be accurate and useless.** With only about 6% of visitors buying, a support vector machine trained the default way predicts that nobody buys: 93.6% accurate, \$0 profit.
- **A simple rule gets close.** A cost-weighted support vector machine reduces to "retarget everyone who added to cart" and earns \$4,226, about 91% of the logistic regression result, with no model needed.
- **Calibration helps, but can't add detail.** Platt scaling lets the support vector machine move its cutoff without retraining, but this particular fitted model's scores fall into two clumps, so calibration gives it only two probability levels (3.2% and 21.4%). Both support vector machine approaches stop retargeting anyone at a \$6 ad, while logistic regression needs only a new cutoff and stays profitable at every ad cost from \$1 to \$10.

The retargeting example assumes visitors who don't see the ad don't buy during the campaign window, so every purchase counts as incremental. Real campaigns need an incrementality test to measure that.

## Related Articles

- [Objective Functions for Marketers: How Models Decide What "Best" Means](https://blog.marketingdatascience.ai/objective-functions-for-marketers-how-models-decide-what-best-means-b737f1705d6b)
- [Is Your Marketing Model Too Accurate?](https://blog.marketingdatascience.ai/is-your-marketing-model-too-accurate-5076f5163326)
- [What Do You Mean by Mean? A Marketer's Guide to Different Types of Averages](https://blog.marketingdatascience.ai/what-do-you-mean-by-mean-a-marketers-guide-to-different-types-of-averages-52cdbf860907)
- [When the Numbers Look Wrong: A Marketer's Guide to Anomaly Detection](https://blog.marketingdatascience.ai/when-the-numbers-look-wrong-a-marketers-guide-to-anomaly-detection-3895e22f2fe7)
- [Measuring Lift: A Marketer's Guide to Incrementality](https://blog.marketingdatascience.ai/measuring-lift-a-marketers-guide-to-incrementality-ab4f57b21cc6)
- [Linear Regression: The Classic Machine Learning Algorithm You Need to Know](https://blog.marketingdatascience.ai/linear-regression-the-classic-machine-learning-algorithm-you-need-to-know-1fe0b48b06a3)
- [What Happens Next? Predicting Website Conversions with Logistic Regression](https://blog.marketingdatascience.ai/what-happens-next-predicting-website-conversions-with-logistic-regression-d374875764e2)
- [Why Many Marketing Models Fail: The Problem of Imbalanced Data](https://blog.marketingdatascience.ai/why-many-marketing-models-fail-the-problem-of-imbalanced-data-ceb8123b80b3)
- [Confused? Don't Worry, Your Marketing Model Is Too. Here's How a Confusion Matrix Can Help](https://blog.marketingdatascience.ai/confused-dont-worry-your-marketing-model-is-too-here-s-how-a-confusion-matrix-can-help-63c017375de4)
- [Predicting Customer Lifetime Value: What Will Your Customers Be Worth?](https://blog.marketingdatascience.ai/predicting-customer-lifetime-value-what-will-your-customers-be-worth-d8f2eb2327f8)
- [Marketing Model Selection: There's No Need to Throw AI at Everything](https://blog.marketingdatascience.ai/marketing-model-selection-theres-no-need-to-throw-ai-at-everything-8030ede44248)
- [Is It Worth It? How to Run a Cost-Benefit Analysis for Better Marketing Decisions](https://blog.marketingdatascience.ai/is-it-worth-it-how-to-run-a-cost-benefit-analysis-for-better-marketing-decisions-5a8dd38216e2)

## Author

**Joe Domaleski** is the founder of [Country Fried Creative](https://countryfriedcreative.com), a digital marketing agency in Peachtree City, Georgia. He holds an MBA from Georgia State University and an MS in Analytics from Georgia Tech, and writes about marketing and data science at [blog.marketingdatascience.ai](https://blog.marketingdatascience.ai).
