[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

```python
import nsfg
import thinkstats2

resp = nsfg.ReadFemResp()

actual_kids = thinkstats2.Pmf(resp.numkdhh, label='actual')

biased_kids = actual_kids.Copy(label='biased')
for x, p in actual_kids.Items():
    biased_kids.Mult(x, x) #multiply each probability by number of kids
biased_kids.Normalize() #normalize back so probabilities equal 1

print("Actual mean number of children per household:", actual_kids.Mean())
print("Observed mean number of children per household:", biased_kids.Mean())
```

The actual average number of children per household in our data is 1.02. However, if this was instead a survey of *children* instead of *households*, we get an observed average of 2.40 children per household. The large discrepancy is due to the fact that zero-child households are not visible at all, and that households with more children appear multiple times, once for each child.
