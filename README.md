<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Predictive Modeling of Tumor Classifications</title>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
      line-height: 1.6;
      color: #24292e;
      background-color: #ffffff;
      max-width: 900px;
      margin: 0 auto;
      padding: 30px;
    }
    h1, h2, h3 {
      border-bottom: 1px solid #eaecef;
      padding-bottom: 0.3em;
      margin-top: 24px;
      margin-bottom: 16px;
      font-weight: 600;
    }
    h1 { font-size: 2em; text-align: center; }
    h2 { font-size: 1.5em; }
    h3 { font-size: 1.25em; border-bottom: none; }
    p, blockquote, ul, table {
      margin-top: 0;
      margin-bottom: 16px;
    }
    blockquote {
      padding: 0 1em;
      color: #6a737d;
      border-left: 0.25em solid #dfe2e5;
    }
    table {
      border-collapse: collapse;
      width: 100%;
    }
    table th, table td {
      padding: 6px 13px;
      border: 1px solid #dfe2e5;
      text-align: left;
    }
    table tr:nth-child(2n) {
      background-color: #f6f8fa;
    }
    code {
      padding: 0.2em 0.4em;
      margin: 0;
      font-size: 85%;
      background-color: rgba(27,31,35,0.05);
      border-radius: 3px;
      font-family: ui-monospace, SFMono-Regular, Consolas, "Liberation Mono", Menlo, monospace;
    }
    .subtitle {
      text-align: center;
      font-weight: bold;
      color: #586069;
      margin-bottom: 30px;
    }
  </style>
</head>
<body>

  <h1>Predictive Modeling of Tumor Classifications using Continuous Normal Distributions</h1>
  <div class="subtitle">An Advanced Predictive Framework for Clinical Prognostic Forecasting</div>

  <h2>1. Introduction to Predictive Mathematical Modeling</h2>
  <p>
    This repository hosts the statistical analysis framework designed to transition historical medical dataset summarization into an advanced predictive system using continuous random variables. By modeling tumor radius means through theoretical normal distributions, the framework shifts the clinical paradigm from retrospective summaries to prognostic forecasting.
  </p>

  <h2>2. Step 1: Spreadsheet-Based Parameter Extraction</h2>
  <p>
    Before implementing continuous probability density modeling, primary sample population parameters were isolated and processed using native spreadsheet computations. Raw data points were segregated by diagnostic classification ("M" for Malignant and "B" for Benign) under the "Radius mean" column header.
  </p>

  <h3>2.1 Spreadsheet Extraction Formulas</h3>
  <ul>
    <li><strong>Sample Mean (&mu;):</strong> <code>=AVERAGE(range)</code></li>
    <li><strong>Sample Standard Deviation (&sigma;):</strong> <code>=STDEV.S(range)</code></li>
    <li><strong>Median Value:</strong> <code>=MEDIAN(range)</code></li>
  </ul>

  <blockquote>
    <strong>Methodological Justification for Degrees of Freedom:</strong> 
    The sample variance computation utilizes the <code>STDEV.S</code> operator, which applies Bessel's correction factor (n - 1 degrees of freedom) rather than the absolute population parameters associated with <code>STDEV.P(n)</code>. This is structurally necessary because the underlying data matrix reflects a small representative sample size (n = 50) instead of the absolute population of all clinical instances.
  </blockquote>

  <h3>2.2 Calculated Dataset Summary Metrics</h3>
  <p>
    Applying these functional steps directly to the 32 benign observations and 18 malignant observations yields the mathematical parameters summarized below:
  </p>

  <table>
    <thead>
      <tr>
        <th>Diagnostic Group</th>
        <th>Sample Size (n)</th>
        <th>Sample Mean (&mu;)</th>
        <th>Standard Deviation (&sigma;)</th>
        <th>Median</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><strong>Benign (X<sub>B</sub>)</strong></td>
        <td>32</td>
        <td>11.75 mm</td>
        <td>1.62 mm</td>
        <td>11.89 mm</td>
      </tr>
      <tr>
        <td><strong>Malignant (X<sub>M</sub>)</strong></td>
        <td>18</td>
        <td>17.66 mm</td>
        <td>2.84 mm</td>
        <td>18.30 mm</td>
      </tr>
    </tbody>
  </table>

  <h2>3. Step 2: Defining the Normal Distribution Models</h2>
  <p>
    Let X<sub>B</sub> represent the continuous random variable for the radius mean of a benign tumor mass, and let X<sub>M</sub> represent the continuous random variable for the radius mean of a malignant tumor mass. Utilizing the derived parameters, the formal N(&mu;, &sigma;<sup>2</sup>) distribution profiles are defined as follows:
  </p>

  <ul>
    <li><strong>Benign Curve Representation:</strong> X<sub>B</sub> ~ N(11.75, 1.62<sup>2</sup>)</li>
    <li><strong>Malignant Curve Representation:</strong> X<sub>M</sub> ~ N(17.66, 2.84<sup>2</sup>)</li>
  </ul>

  <h3>3.1 Geometric Analysis of the Probability Curves</h3>
  <p>
    Representing the populations through continuous functions reveals the following geometric behaviors:
  </p>
  <ul>
    <li>
      <strong>Horizontal Translation (Shifting):</strong> The malignant curve profile is translated significantly to the right along the horizontal axis. This behavior is driven by the clear discrepancy between the two expected values (&mu;<sub>M</sub> = 17.66 mm versus &mu;<sub>B</sub> = 11.75 mm), matching the accelerated growth dynamics typical of malignant pathologies.
    </li>
    <li>
      <strong>Vertical and Horizontal Scaling (Flattening):</strong> The malignant distribution shows a wider, flatter profile with a lower peak density. This is a direct mathematical consequence of its larger standard deviation (&sigma;<sub>M</sub> = 2.84 mm versus &sigma;<sub>B</sub> = 1.62 mm), showing the higher rate of structural variation found in cancerous tissue matrices.
    </li>
  </ul>

  <h2>4. Step 4: Clinical Threshold Strategy and Risk Probabilities</h2>
  <p>
    In oncology screening, radiologists establish an operational mathematical decision boundary (k) to determine if a mass requires invasive biopsies. Examining the raw spreadsheet data reveals that the maximum recorded benign radius mean was 14.53 mm. A baseline clinical threshold is therefore established at k = 14.50 mm. Any tumor displaying a radius mean greater than 14.50 mm is classified as malignant.
  </p>
  <p>
    This decision boundary introduces two distinct diagnostic risks, evaluated via integration routines:
  </p>

  <h3>4.1 Quantifying the Risk of a False Positive (P(Type I Error))</h3>
  <p>
    A false positive occurs when a benign tumor has a physical radius exceeding our boundary parameter (X<sub>B</sub> &gt; 14.50), leading to unnecessary surgical procedures and diagnostic anxiety. 
  </p>
  <p>
    Executing this evaluation via a normal cumulative distribution function (Lower = 14.50, &mu; = 11.7465, &sigma; = 1.6231) yields:
  </p>
  <p>
    <code>P(X<sub>B</sub> &gt; 14.50) &approx; 0.0449 &rArr; 4.49%</code>
  </p>
  <p>
    The model shows a 4.49% chance that a patient with a benign tumor will be incorrectly categorized as needing urgent cancer interventions.
  </p>

  <h3>4.2 Quantifying the Risk of a False Negative (P(Type II Error))</h3>
  <p>
    A false negative represents the more severe medical error, where a truly malignant tumor has a radius smaller than our threshold parameter (X<sub>M</sub> &lt; 14.50). This leads to a missed cancer diagnosis and delayed treatment.
  </p>
  <p>
    Applying the matching calculator configurations (Upper = 14.50, &mu; = 17.6583, &sigma; = 2.8362) yields:
  </p>
  <p>
    <code>P(X<sub>M</sub> &lt; 14.50) &approx; 0.1327 &rArr; 13.27%</code>
  </p>
  <p>
    The model shows a 13.27% chance of missing a malignant case. From a medical perspective, this error rate is too high, showing that a threshold of 14.50 mm lacks the sensitivity required to safely rule out cancerous growths.
  </p>

  <h2>5. Step 5: Analytical Commentary and Methodological Reflection</h2>
  
  <h3>5.1 Evaluation of the Normality Assumption</h3>
  <p>
    For the benign population subset, the calculated mean (11.75 mm) and median (11.89 mm) sit closely together. This strong symmetry supports using a continuous normal distribution model for this dataset. However, real-world biological tissues do not perfectly fit ideal mathematical curves, and true clinical tail probabilities often show slight discrepancies due to varying patient characteristics.
  </p>

  <h3>5.2 Strategic Adjustments to the Decision Boundary</h3>
  <p>
    The clinical value of this model depends directly on the location of the boundary parameter k. Choosing 14.50 mm effectively protects patients from unnecessary biopsy scares due to the low 4.49% false positive rate. However, to resolve the critical 13.27% false negative rate, clinicians would need to lower the threshold value k. This structural adjustment would improve diagnostic safety, but would also increase the rate of false positive errors, illustrating the trade-offs required when applying mathematical models to medicine.
  </p>

  <h3>5.3 Sample Size Constraints and Parameter Sensitivity</h3>
  <p>
    Finally, the model's predictive reliability is constrained by its small sample size (n = 50, consisting of 32 benign observations and 18 malignant observations). Because standard deviations are sensitive to sample changes at this scale, a single outlier can distort the shape of the bell curves. This distortion can shift the entire distribution and skew the calculated diagnostic probabilities, which is an important limitation to address when reflecting on the model's real-world accuracy.
  </p>

</body>
</html>
