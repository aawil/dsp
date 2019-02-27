[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

```python
import hypothesis
import first
import numpy as np

class DiffMeansResample(hypothesis.DiffMeansPermute):
    
    def RunModel(self):
        resample_n = np.random.choice(self.pool, self.n, replace=True)
        resample_m = np.random.choice(self.pool, self.m, replace=True)
        return resample_n, resample_m
    
def run_tests(data):
    ht_permute = hypothesis.DiffMeansPermute(data)
    pvalue_permute = ht_permute.PValue()

    ht_resample = DiffMeansResample(data)
    pvalue_resample = ht_resample.PValue()
    
    return pvalue_permute, pvalue_resample

live, firsts, others = first.MakeFrames()
lngth_data = firsts.prglngth.values, others.prglngth.values
wgt_data = firsts.totalwgt_lb.dropna().values, others.totalwgt_lb.dropna().values

lngth_p_permute, lngth_p_resample = run_tests(lngth_data)
wgt_p_permute, wgt_p_resample = run_tests(wgt_data)

print("The p-value for pregnancy length using permutation is", lngth_p_permute)
print("The p-value for pregnancy length using resampling is", lngth_p_resample)

print("The p-value for birth weight using permutation is", wgt_p_permute)
print("The p-value for birth weight using resampling is", wgt_p_resample)
```

Output:

```
The p-value for pregnancy length using permutation is 0.161
The p-value for pregnancy length using resampling is 0.167
The p-value for birth weight using permutation is 0.0
The p-value for birth weight using resampling is 0.0
```

For this data, the permutation and resampling methods yield approximately the same p-values. 
