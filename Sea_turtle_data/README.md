# Sea turtle data visualization
### Data is sourced from this publicly available [field data](https://www.nps.gov/caha/learn/nature/upload/2018_CAHA_Sea-turtle-report_final_report.pdf). Figures are made using R.

---
&nbsp;
##### 1. Library
```{r}
library(ggplot2)
```
&nbsp;
##### 2. Data

```{r}
strandings<-read.csv("strandings.csv", header = TRUE)
strand.spec<-read.csv("seaturtle.csv", header = TRUE)
```
&nbsp;
##### 3. Using ggplot2 to plot the data
&nbsp; 3.1 Using the `geom_jitter` plot, I plotted the total number of strandings per year and let the species-specific number of strandings corrospond to point size. Color cooresponds to species.
```{r}
 ggplot(strand.spec, aes(Species, SpeciesTotal)) +
       geom_jitter(aes(col=Year, size=StrandingYearTotal, )) +
       theme_linedraw() +
       labs(y = "Species-specific totals", x = "Year") 
```
&nbsp; **Output:**

![alt text](https://github.com/gausec/CapeHatteras/blob/main/Results/Strandings.png?raw=true)

&nbsp; 3.2 A variation of the jitter plot where color corresponds to year and the Y-axis is the species.
```{r}
 ggplot(strand.spec, aes(Species, SpeciesTotal)) +
       geom_jitter(aes(col=Year, size=StrandingYearTotal, )) +
       theme_linedraw() +
       labs(y = "Species-specific totals", x = "Year")
```
