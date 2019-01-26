[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

```python
import brfss
import scipy.stats
import thinkstats2

#first, model with an ideal normal distribution
min_ht = 177.8 #5'10" in cm
max_ht = 185.42 #6'1" in cm

too_short = scipy.stats.norm.cdf(min_ht, loc=178, scale=7.7)
too_tall = 1 - scipy.stats.norm.cdf(max_ht, loc=178, scale=7.7)

blue_man_eligible = round((1 - (too_short + too_tall)) * 100, 2)

print("According to a modeled distribution, %s%% of men are eligible for the Blue Man Group based on height." % blue_man_eligible)

#look at real data
df = brfss.ReadBrfss()

df_men = df[df.sex==1]

df_men_cdf = thinkstats2.Cdf(df_men.htm3)

too_short_cdf = df_men_cdf.PercentileRank(min_ht)
too_tall_cdf = 100 - df_men_cdf.PercentileRank(max_ht)

blue_man_eligible_cdf = round((100 - (too_short_cdf + too_tall_cdf)), 2)

print("According to the BRFSS data, %s%% of men are eligible for the Blue Man Group based on height." % blue_man_eligible_cdf)
```

Output:
```
According to a modeled distribution, 34.27% of men are eligible for the Blue Man Group based on height.
According to the BRFSS data, 47.73% of men are eligible for the Blue Man Group based on height.
```

The difference between the modeled ideal normal distribution created by `scipy.stats.norm.cdf`, and the rather larger figure derived from the actual data, indicates that the normal distribution may not perfectly represent of the distribution of heights of adult men in the BRFSS data.
