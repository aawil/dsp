[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

```python
import hinc
import hinc2
import thinkstats2
import numpy as np
from scipy import stats

def pearson_skew(xs):
    median = np.median(xs)
    mean = np.mean(xs)
    var = np.var(xs)
    std = np.sqrt(var)
    return (3 * (mean - median)) / std

def describe_income(upper):
    log_income = hinc2.InterpolateSample(incdata, log_upper=upper)
    interp_income = np.power(10, log_income)
    income_cdf = thinkstats2.Cdf(interp_income)
    print("Median:", np.median(interp_income))
    print("Mean:", np.mean(interp_income))
    print("Proportion below mean:", income_cdf.Prob(np.mean(interp_income)))
    print("Pearson's median skewness:", pearson_skew(interp_income))
    print("Pearson's moment coefficient of skewness:", stats.skew(interp_income))
    print("")
     
incdata = hinc.ReadData()

print("With maximum income of $1,000,000:")
describe_income(6.0)

print("With maximum income of $100,000,000:")
describe_income(8.0)

print("With maximum income of $10,000,000,000:")
describe_income(10.0)
```

Output:

```
With maximum income of $1,000,000:
Median: 51226.93306562372
Mean: 74278.7075311872
Proportion below mean: 0.660005879566872
Pearson's median skewness: 0.7361105192428792
Pearson's moment coefficient of skewness: 4.949920244429584

With maximum income of $100,000,000:
Median: 51226.93306562372
Mean: 457453.4872473685
Proportion below mean: 0.9786294076336377
Pearson's median skewness: 0.2747906496429362
Pearson's moment coefficient of skewness: 14.892459804414134

With maximum income of $10,000,000,000:
Median: 51226.93306562372
Mean: 22526983.866709214
Proportion below mean: 0.986330007022816
Pearson's median skewness: 0.20145260232700665
Pearson's moment coefficient of skewness: 19.842428978052872
```

The distribution of the Census household income data changes radically depending on the upper bound chosen during interpolation. With an unrealistic maximum income of $1,000,000, only two-thirds of the sample is below the mean; at the depressingly still-too-low value of $100,000,000 per year, more than 97% are below the mean income of $457,453. If we use a Bezos-esque figure of ten billion dollars income, the mean is over $20 million. Strangely, the Pearson's median skewness actually goes down, owing to the very high standard deviations of these extremely skewed distributions. The Pearson's moment coefficient (as implemented by ```scipy.stats```), on the other hand, correctly rises with the maximum income.
