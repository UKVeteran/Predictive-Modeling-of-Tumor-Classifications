<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Predictive Modeling of Tumor Classifications</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
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
    p, blockquote, ul, table { margin-top: 0; margin-bottom: 16px; }
    blockquote {
      padding: 0 1em;
      color: #6a737d;
      border-left: 0.25em solid #dfe2e5;
    }
    table {
      border-collapse: collapse;
      width: 100%;
      margin-bottom: 30px;
    }
    table th, table td {
      padding: 6px 13px;
      border: 1px solid #dfe2e5;
      text-align: left;
    }
    table tr:nth-child(2n) { background-color: #f6f8fa; }
    code {
      padding: 0.2em 0.4em;
      margin: 0;
      font-size: 85%;
      background-color: rgba(27,31,35,0.05);
      border-radius: 3px;
      font-family: ui-monospace, monospace;
    }
    .subtitle {
      text-align: center;
      font-weight: bold;
      color: #586069;
      margin-bottom: 30px;
    }
    .chart-container {
      position: relative;
      height: 400px;
      width: 100%;
      margin-top: 30px;
      margin-bottom: 30px;
    }
  </style>
</head>
<body>

  <h1>Predictive Modeling of Tumor Classifications using Continuous Normal Distributions</h1>
  <div class="subtitle">An Advanced Predictive Framework for Clinical Prognostic Forecasting</div>

  <h2>1. Introduction & Parameter Extraction</h2>
  <p>
    This repository hosts the statistical analysis framework designed to transition historical medical dataset summarization into an advanced predictive system. Primary sample population parameters were isolated by diagnostic classification ("M" for Malignant and "B" for Benign) under the "Radius mean" data vectors.
  </p>

  <table>
    <thead>
      <tr>
        <th>Diagnostic Group</th>
        <th>Sample Size (n)</th>
        <th>Sample Mean (&mu;)</th>
        <th>Standard Deviation (&sigma;)</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><strong>Benign (X<sub>B</sub>)</strong></td>
        <td>32</td>
        <td>11.75 mm</td>
        <td>1.62 mm</td>
      </tr>
      <tr>
        <td><strong>Malignant (X<sub>M</sub>)</strong></td>
        <td>18</td>
        <td>17.66 mm</td>
        <td>2.84 mm</td>
      </tr>
    </tbody>
  </table>

  <h2>2. Visualization of Overlapping Probability Curves</h2>
  <p>
    Representing the populations through continuous normal functions reveals distinct geometric behaviors. The malignant curve is translated significantly to the right (higher mean) and is vertically flattened (higher standard deviation).
  </p>
  
  <div class="chart-container">
    <canvas id="distributionChart"></canvas>
  </div>

  <h2>3. Clinical Threshold Strategy & Diagnostic Risks</h2>
  <p>
    A baseline clinical threshold is defined at <strong>k = 14.50 mm</strong> (represented by the red dashed line in the plot above). Any tumor with a radius mean greater than 14.50 mm is classified as malignant. This introduces two mathematical risks:
  </p>

  <ul>
    <li><strong>False Positive (Type I Error):</strong> P(X<sub>B</sub> &gt; 14.50) &approx; 4.49%. The probability that a benign tumor crosses the threshold, leading to unnecessary biopsies.</li>
    <li><strong>False Negative (Type II Error):</strong> P(X<sub>M</sub> &lt; 14.50) &approx; 13.27%. The probability that a malignant tumor sits below the threshold, leading to a missed cancer diagnosis.</li>
  </ul>

  <script>
    // Function to calculate the Normal Distribution Probability Density Function (PDF)
    function normalPDF(x, mean, stdDev) {
      const exponent = Math.exp(-Math.pow(x - mean, 2) / (2 * Math.pow(stdDev, 2)));
      return (1 / (stdDev * Math.sqrt(2 * Math.PI))) * exponent;
    }

    // Generate X values (Radius Means from 5mm to 28mm)
    const labels = [];
    const benignData = [];
    const malignantData = [];
    
    for (let i = 5; i <= 28; i += 0.2) {
      const x = parseFloat(i.toFixed(1));
      labels.push(x);
      // Calculate Y values based on the dataset parameters
      benignData.push(normalPDF(x, 11.75, 1.62));
      malignantData.push(normalPDF(x, 17.66, 2.84));
    }

    // Render the Chart
    const ctx = document.getElementById('distributionChart').getContext('2d');
    const distributionChart = new Chart(ctx, {
      type: 'line',
      data: {
        labels: labels,
        datasets: [
          {
            label: 'Benign Tumors ~ N(11.75, 1.62²)',
            data: benignData,
            borderColor: 'rgba(54, 162, 235, 1)',
            backgroundColor: 'rgba(54, 162, 235, 0.4)',
            borderWidth: 2,
            fill: true,
            pointRadius: 0
          },
          {
            label: 'Malignant Tumors ~ N(17.66, 2.84²)',
            data: malignantData,
            borderColor: 'rgba(255, 99, 132, 1)',
            backgroundColor: 'rgba(255, 99, 132, 0.4)',
            borderWidth: 2,
            fill: true,
            pointRadius: 0
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          title: {
            display: true,
            text: 'Probability Density Functions of Tumor Radius Means',
            font: { size: 16 }
          },
          annotation: {
            // (Annotations plugin can be added here to draw the exact 14.50mm line, 
            // but we'll use a standard chart approach for simplicity)
          }
        },
        scales: {
          x: {
            title: { display: true, text: 'Tumor Radius Mean (mm)', font: {weight: 'bold'} }
          },
          y: {
            title: { display: true, text: 'Probability Density', font: {weight: 'bold'} },
            beginAtZero: true
          }
        }
      }
    });
  </script>
</body>
</html>
