<h1 align="center">Predictive Modeling of Tumor Classifications using Continuous Normal Distributions</h1>

<p align="center">
  <em>An Advanced Predictive Framework for Clinical Prognostic Forecasting</em>
</p>

---

## 1. Introduction to Predictive Mathematical Modeling

This repository hosts the statistical analysis framework designed to transition historical medical dataset summarization into an advanced predictive system using continuous random variables. By modeling tumor radius means through theoretical normal distributions, the framework shifts the clinical paradigm from retrospective summaries to prognostic forecasting.

## 2. Step 1: Spreadsheet-Based Parameter Extraction

Before implementing continuous probability density modeling, primary sample population parameters were isolated and processed using native spreadsheet computations. Raw data points were segregated by diagnostic classification ("M" for Malignant and "B" for Benign) under the "Radius mean" column header.

### Calculated Dataset Summary Metrics

| Diagnostic Group | Sample Size (n) | Sample Mean (&mu;) | Standard Deviation (&sigma;) | Median |
| :--- | :---: | :---: | :---: | :---: |
| **Benign (X<sub>B</sub>)** | 32 | 11.75 mm | 1.62 mm | 11.89 mm |
| **Malignant (X<sub>M</sub>)** | 18 | 17.66 mm | 2.84 mm | 18.30 mm |

> **Methodological Justification for Degrees of Freedom:** > The sample variance computation utilizes the `STDEV.S` operator, which applies Bessel's correction factor (n - 1 degrees of freedom). This is structurally necessary because the underlying data matrix reflects a small representative sample size (n = 50) instead of the absolute population of all clinical instances.

## 3. Step 2: Defining the Normal Distribution Models

Let **X<sub>B</sub>** represent the continuous random variable for the radius mean of a benign tumor mass, and let **X<sub>M</sub>** represent the continuous random variable for the radius mean of a malignant tumor mass. 

* **Benign Curve Representation:** X<sub>B</sub> ~ N(11.75, 1.62²)
* **Malignant Curve Representation:** X<sub>M</sub> ~ N(17.66, 2.84²)

### Geometric Analysis of the Probability Curves

*(Note: To display the plot, save an image of your overlapping bell curves as `distribution-plot.png` in your repository and replace the placeholder image below)*

![Probability Density Functions of Tumor Radius Means](distribution-plot.png)

* **Horizontal Translation (Shifting):** The malignant curve profile is translated significantly to the right along the horizontal axis (&mu;<sub>M</sub> = 17.66 mm versus &mu;<sub>B</sub> = 11.75 mm), matching the accelerated growth dynamics typical of malignant pathologies.
* **Vertical and Horizontal Scaling (Flattening):** The malignant distribution shows a wider, flatter profile with a lower peak density due to its larger standard deviation (&sigma;<sub>M</sub> = 2.84 mm versus &sigma;<sub>B</sub> = 1.62 mm).

## 4. Step 3: Clinical Threshold Strategy and Risk Probabilities

Examining the raw spreadsheet data reveals that the maximum recorded benign radius mean was 14.53 mm. A baseline clinical threshold is therefore established at **k = 14.50 mm**. Any tumor displaying a radius mean greater than 14.50 mm is classified as malignant.

This decision boundary introduces two distinct diagnostic risks:

### Quantifying the Risk of a False Positive (Type I Error)
A false positive occurs when a benign tumor has a physical radius exceeding our boundary parameter (X<sub>B</sub> > 14.50), leading to unnecessary surgical procedures. 
* `P(X_B > 14.50) ≈ 0.0449` &rarr; **4.49%** chance of a false positive.

### Quantifying the Risk of a False Negative (Type II Error)
A false negative occurs when a truly malignant tumor has a radius smaller than our threshold parameter (X<sub>M</sub> < 14.50), leading to a missed cancer diagnosis.
* `P(X_M < 14.50) ≈ 0.1327` &rarr; **13.27%** chance of a false negative.

## 5. Step 4: Analytical Commentary and Methodological Reflection
  
* **Evaluation of the Normality Assumption:** For the benign population subset, the calculated mean (11.75 mm) and median (11.89 mm) sit closely together. This strong symmetry supports using a continuous normal distribution model.
* **Strategic Adjustments to the Decision Boundary:** Choosing 14.50 mm effectively protects patients from unnecessary biopsy scares (low 4.49% false positive rate). However, resolving the critical 13.27% false negative rate requires lowering the threshold, which unavoidably increases false positives.
* **Sample Size Constraints:** The model's predictive reliability is constrained by its small sample size (n = 50). Standard deviations are highly sensitive at this scale, meaning a single outlier can distort the shape of the bell curves and skew the calculated probabilities.
