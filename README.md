[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/JOFojSQO)
# Programming Assignment 3
**DATA 259**  
**Fall 2024**

## Introduction
For questions on this and other assignments, you may need to write Python code to do data analysis, provide only an explanation in prose, or do both. In this course, we will be using Quarto documents to author assignment submissions and reports to develop our skills in reproducible research tools. Use a code chunk for any code you write in solving problems, and use Markdown for your explanation of what you did. We will not count your answer as correct if we cannot see it/it is written in a code comment.

We recommend one code chunk for each question, but feel free to add more as you see fit. In general, within the Markdown, you should explain the approach you took in your code at a high level in addition to explicitly answering any questions that were asked. It is up to you to decide what code-based analyses, if any, are appropriate for a particular problem.

When you are finished, please render your document to a PDF and upload your assignment in Gradescope. Make sure to select the areas of the page corresponding to the questions on the assignment outline. It is much easier for the graders to give you feedback this way, and you will therefore get your homework assignments back faster. If there is a lot of excess output, either revisit your code to make sure you are not printing excessively, or delete the pages with excess output from the PDF before submitting.

---

## Problem 1
For this assignment, we will be using the UCI income dataset (“income.csv”) that you used in Programming Assignment 2, but with a few additional columns. As you may recall, this is data collected from the US census in 1994. It contains demographic data paired with information about whether the person in the entry has annual income over $50,000.

In this dataset, some variables are considered “sensitive attributes” (protected attributes in some cases). These are generally regarded as inappropriate bases on which to make decisions because of the potential for discrimination.

Before you start: Make sure you understand the concept of a function, and that you can use it. In this Programming Assignment, you should use functions extensively. If you don’t, you’ll find yourself spending a long time writing tedious Python code. However, if you use them effectively, you’ll find yourself reusing common functionality across problems and saving a lot of time as a consequence.

You can use libraries, such as [`fairlearn`](https://fairlearn.org/), to compute the fairness metrics, but make sure you understand how the metrics are computed and how to use the relevant APIs with the right input and output.

1. Retrieve Models
We’ll be working with the two models from Programming Assignment 2 (the Random Forest classifier we provided and the alternative one you built). Retrieve those (as functions or replicate your code here), and ensure you can read/preprocess the data, train the classifiers, and make inferences. You can train the model using the training data and make predictions using the testing data you had in Programming Assignment 2. You can use the same features you used before, even though the dataset we provide you in this assignment may have a few additional columns (just ignore those until we use them explicitly).

2. False Positive and Negative Rates by Gender and Race
For each of the models, obtain the predicted labels `y_pred`, and plot the false positive and false negative rates by different genders and races. You may want to use a grouped bar chart. Describe any patterns you see.

One proposed fairness definition is **disparate impact**. Disparate impact is defined as the ratio:

```
Pr[Y_pred = 1 | A = 1] / Pr[Y_pred = 1 | A = 0]
```

If this ratio is less than some threshold (tau), it is considered to have disparate impact. In this definition, `A = 1` when the person belongs to the group we’re worried about being discriminated against, and `A = 0` when the person belongs to any other group.

3. Evaluate Models by Disparate Impact
Evaluate the two models using this measurement by looking at different groups in gender and race (be sure to be specific about your group definition). Explain the results you see and interpret them in the context of the metric. Can you identify any particular groups that the models seem to disproportionately give positive predictions to? How would it affect the model’s fairness? Give a brief answer.

Another proposed fairness definition is **equalized odds**. For binary classifiers, this requires that:

```
Pr[Y_pred = 1 | A = 0, Y = a] = Pr[Y_pred = 1 | A = 1, Y = a] for a in {0, 1}
```

For each model, obtain the values from both sides of the equation with `A` corresponding to gender. Are they equal (for `Y = 0` or `Y = 1`)? If not, what are the differences? Perform the same calculations with `A` corresponding to white/non-white races in your datasets. What do these numbers say about the two models you have with respect to any potential bias?

The last fairness definition we test is **equal opportunity**. For binary classifiers, this requires that:

```
Pr[Y_pred = 1 | A = 0, Y = 1] = Pr[Y_pred = 1 | A = 1, Y = 1]
```

4. Evaluate Models by Equal Opportunity
For each model, obtain the values from both sides of the equation with `A` corresponding to gender to establish if your model passes this metric. Perform the same calculations with `A` corresponding to white/non-white races in your datasets. What do these numbers say about the two models you have with respect to any potential bias?

5. Compare Equalized Odds vs Equal Opportunity
Compare how your models fare on **equalized odds** versus **equal opportunity**, and comment on the difference between these two metrics in this regard.

6. Examine Predictions from a Black-Box Model
The column `predictions` in the dataset we distributed for Programming Assignment 3 contains predictions from a black-box model we have constructed. Examine the predictions in light of gender and white/non-white races in your dataset. Do they seem fair by **disparate impact** and **equalized odds**?

7. Comparison of Models in Terms of Fairness
You have evaluated predictions of three models so far. Comment on how they compare in terms of fairness. Factoring in both fairness and performance, which of these three models would you recommend using? Explain your choice while highlighting the potential trade-offs you considered during the process.

"Intersectionality" is a term coined by Kimberlé Crenshaw used to refer to the phenomena in anti-discrimination law where plaintiffs alleging discrimination on two bases (e.g., sex and race) would lose cases because the claims would be evaluated separately rather than considering the intersection of different demographic categories.

8. Analyze the accuracy of the two models through this intersectionality lens. Since the number of comparisons to make grows fast with the number of intersectional groupings, choose two intersectional groupings you consider to be of particular importance and evaluate the two models with respect to those groupings. What do you conclude? Give a brief response.