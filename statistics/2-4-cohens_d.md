[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

```python
import numpy as np
import nsfg

preg = nsfg.ReadFemPreg() #load in data
live = preg[preg.outcome == 1] #new dataset including only live births

firsts = live[live.birthord == 1] #first births
others = live[live.birthord != 1] #subsequent births

def CohensD(g1, g2):
    diff = g1.mean() - g2.mean()
    var1 = g1.var()
    var2 = g2.var()
    n1 = len(g1)
    n2 = len(g2)
    pvar = (n1*var1 + n2*var2) / (n1 + n2)
    d = diff / np.sqrt(pvar)
    return d
    
length_effect = CohensD(firsts.prglngth, others.prglngth)
weight_effect = CohensD(firsts.totalwgt_lb, others.totalwgt_lb)

print("Cohen's D of pregnancy length is:",length_effect)
print("Cohen's D of birth weight is:",weight_effect)
```

Cohen's D for pregnancy length is 0.029 standard deviations, while the same statistic for birth weight is -0.089 SDs. A negative effect size means that first births, on average, weigh slightly less than subsequent births, even though they result from (on average) very slightly longer pregnancies. The effect size for both measures is very low, less than a tenth of a standard deviation.
