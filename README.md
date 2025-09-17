# Multi-Pair Augmented Dickey-Fuller Test
Perform ADF-Test (stationarity test) on several forex pairs at once and rank the results from the most mean-reversion tendency to least

---

## Testing a Currency Pair for Stationarity
Let's imagine you have a historical time series of daily closing prices for EUR/USD (EURUSD=X), and you want to test it for stationarity.

1. Run the Test: You would use a function like adfuller() in Python, feeding it your time series data. The function will run the underlying regression and give you the key outputs: the ADF statistic, the p-value, and critical values at various significance levels.
   
2. Hypotheses:
* Null Hypothesis (H0​): The EUR/USD price series has a unit root (is non-stationary). 😥
* Alternative Hypothesis (H1​): The EUR/USD price series does not have a unit root (is stationary). 🥳

3. Example Output: Let's say the ADF test on your data produces the following results:
* ADF Statistic: -3.25
* p-value: 0.017
* Critical Values:
  * 1% level: -3.45
  * 5% level: -2.87
  * 10% level: -2.57

## Interpreting the Results
Now you must interpret these numbers to make a decision about the time series. There are two primary ways to interpret the results, and they should always lead to the same conclusion.
1. Interpreting the p-value
The p-value is the most common way to interpret the test. You compare it to a pre-determined significance level, typically 0.05.
* Rule: If the p-value is less than or equal to 0.05, you reject the null hypothesis.
* Interpretation: In our example, the p-value of 0.017 is less than 0.05. This means we have strong evidence to reject the null hypothesis and conclude that the EUR/USD time series is stationary. This suggests that prices tend to revert to a mean, making it a good candidate for a mean reversion strategy.

2. Interpreting the ADF Statistic and Critical Values
The ADF statistic itself is a negative number. The more negative it is, the stronger the evidence against the null hypothesis. You compare this statistic to the critical values.
* Rule: If the ADF statistic is more negative than the critical value, you reject the null hypothesis.
* Interpretation: In our example, the ADF statistic of -3.25 is more negative than the 5% critical value of -2.87. This leads us to the same conclusion: we can reject the null hypothesis and confirm that the time series is stationary.

What the Results Mean for Your Trading
* Stationary Series (Reject H0​): This time series is likely to fluctuate around a long-term average. It is a good candidate for a mean reversion strategy. For example, you could sell when the price is far above its moving average and buy when it's far below.
* Non-Stationary Series (Fail to Reject H0​): This time series likely follows a random walk, with no tendency to revert to a mean. It is a good candidate for a trend following strategy, as prices are more likely to continue in their current direction than reverse.

By using the ADF test, you're moving from a subjective "this pair looks like it's ranging" to an objective, data-driven "this pair's statistical properties indicate it's suitable for mean reversion."

## Multi-Pair Test
By running the ADF-test concurrently on several forex pairs and saving the results into a list, we can rank them and then decide which pairs have the most mean-reverting tendency and which have the least.

Set the pair List and the time range to test on
```Python
# Define the list of forex pairs to test
# The '=X' suffix is necessary for forex data on Yahoo Finance
forex_pairs = ['AUDUSD=X', 'EURGBP=X', 'NZDUSD=X', 'USDCHF=X',
               'AUDJPY=X', 'CADJPY=X', 'EURUSD=X', 'GBPUSD=X',
               'NZDJPY=X', 'USDCAD=X', 'CHFJPY=X', 'EURJPY=X',
               'EURNZD=X', 'GBPJPY=X', 'USDJPY=X', 'GC=F']

# Define the time period for the data
start_date = '2015-01-01'
end_date = '2025-01-01'
```

Output Example:
```Bash
--- Ranked Results (Most Mean-Reverting to Least) ---
Pair         ADF Statistic   p-value   
-------------------------------------
USDCAD=X     -3.5570         0.0066    
USDCHF=X     -3.3585         0.0125    
GBPUSD=X     -2.8360         0.0533    
EURUSD=X     -2.7649         0.0635    
EURNZD=X     -2.6920         0.0754    
AUDUSD=X     -2.5885         0.0954    
NZDUSD=X     -2.5133         0.1123    
NZDJPY=X     -2.2632         0.1841    
EURGBP=X     -2.1751         0.2154    
AUDJPY=X     -1.8893         0.3371    
CADJPY=X     -1.1301         0.7029    
GBPJPY=X     -1.0640         0.7292    
EURJPY=X     -0.6527         0.8586    
USDJPY=X     0.0834          0.9649    
CHFJPY=X     0.4417          0.9830    
GC=F         0.5184          0.9854
```

---

Back to [Index](https://github.com/handiko/handiko/blob/master/README.md)
