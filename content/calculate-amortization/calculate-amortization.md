+++
date = '2025-06-04T23:13:15-05:00'
title = 'Calculate Amortization'
tags = ['mortgage', 'finance', 'amortization']
+++

### Calculate your amortization

All you need to do is input the following:
  * Price
  * Length of mortage, in years
  * Projected interest rate, in %

<form onsubmit="calculateAmortization(); return false;" style="max-width:400px;margin:auto;">
  <label>Loan Amount:<br>
    <input type="number" id="loanAmount" required step="0.01">
  </label>

  <label>Annual Interest Rate (%):<br>
    <input type="number" id="annualInterest" required step="0.01">
  </label>

  <label>Loan Term (Years):<br>
    <input type="number" id="loanTerm" required>
  </label>

  <button type="submit">Calculate</button>
</form>

<div id="result" style="max-width:400px;margin:auto;margin-top:1em;"></div>

<script>
function calculateAmortization() {
  const principal = parseFloat(document.getElementById('loanAmount').value);
  const annualRate = parseFloat(document.getElementById('annualInterest').value) / 100;
  const years = parseInt(document.getElementById('loanTerm').value);
  const monthlyRate = annualRate / 12;
  const numPayments = years * 12;

  const x = Math.pow(1 + monthlyRate, numPayments);
  const monthlyPayment = (principal * x * monthlyRate) / (x - 1);
  const totalPayment = monthlyPayment * numPayments;
  const totalInterest = totalPayment - principal;

  document.getElementById('result').innerHTML = `
  <strong>Results:</strong><br>
  Monthly Payment: $${monthlyPayment.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 })}<br>
  Total Payment: $${totalPayment.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 })}<br>
  Total Interest: $${totalInterest.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 })}
`;

}
</script>
