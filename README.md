#volest#

A complete set of volatility estimators based on Euan Sinclair's Volatility Trading (http://www.amazon.com/Volatility-Trading-CD-ROM-Euan-Sinclair/dp/0470181990).

Volatility estimators include:

* Garman Klass
* Hodges Tompkins
* Parkinson
* Rogers Satchell
* Yang Zhang
* Standard Deviation

Also includes

* Skew
* Kurtosis
* Correlation

For each of the estimators, plot:

* Probability cones
* Rolling quantiles
* Rolling extremes
* Rolling descriptive statistics
* Histogram
* Comparison against arbirary comparable
* Correlation against arbirary comparable
* Regression against arbirary comparable

Also creates a term sheet with all the metrics printed to a PDF

Example usage:

```python

import volest
import datetime as dt

ticker = 'JPM'
start = dt.datetime(2013, 1, 1)
end = dt.datetime(2013, 12, 31)
type = 'GarmanKlass'

window=30
windows=[30, 60, 90, 120]
quantiles=[0.25, 0.75]
bins=100
normed=True
bench='^GSPC'
open=False


vol = volest.VolatilityEstimator(ticker, start, end, type)

# call plt.show() on any of the below
fig, plt = vol.cones(windows=windows, quantiles=quantiles)
fig, plt = vol.rolling_quantiles(window=window, quantiles=quantiles)
fig, plt = vol.rolling_extremes(window=window)
fig, plt = vol.rolling_descriptives(window=window)
fig, plt = vol.histogram(window=window, bins=bins, normed=normed)
fig, plt = vol.benchmark_compare(window=window, bench=bench)
fig, plt = vol.benchmark_correlation(window=window, bench=bench)

# prints regression statistics
print vol.benchmark_regression(window=window, bench=bench)

# creates a pdf term sheet with all metrics
vol.term_sheet(window, windows, quantiles, bins, normed, bench)

```