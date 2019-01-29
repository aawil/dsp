[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

```python
import numpy as np
import nsfg
import thinkstats2
import thinkplot

preg = nsfg.ReadFemPreg() #load in data
live = preg.dropna(subset=['agepreg', 'totalwgt_lb']) #new dataset including only live births

thinkplot.PrePlot(cols=2)

#basic scatter plot
thinkplot.Scatter(live.agepreg, live.totalwgt_lb)
thinkplot.Config(xlabel='Age of mother',
               ylabel='Weight of baby (lb)',
               title='Scatter plot of birth weight, by age of mother')


#bin ages, plot percentiles of weight
bins = np.arange(10, 45, 5)
indices = np.digitize(live.agepreg, bins)
groups = live.groupby(indices)

ages = [group.agepreg.mean() for i, group in groups]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups]

thinkplot.PrePlot(3)
thinkplot.SubPlot(2)

for percent in [75, 50, 25]:
    weights = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(ages, weights, label=label)
    
thinkplot.Show(xlabel='Age of mother (binned)',
               ylabel='Weight of baby',
               title='Percentiles of birth weight, by age of mother')

pearsons = round(thinkstats2.Corr(live.agepreg, live.totalwgt_lb), 4)
spearmans = round(thinkstats2.SpearmanCorr(live.agepreg, live.totalwgt_lb), 4)

print("Pearson's correlation coefficient is", pearsons)
print("Spearman's rank correlation is", spearmans)
```

Output:

![plot](../img/7-2-plots.png)

```
Pearson's correlation coefficient is 0.0688
Spearman's rank correlation is 0.0946
```

Both the plots and the correlation statistics show a slight positive correlation between the age of the mother and the baby's birth weight. It's more visible in the percentiles plot than in the scatter plots. The odd angles at the extreme ends of the percentile plot can be attributed to the low N in the lowest and highest bins.
