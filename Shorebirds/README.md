# Shorebird data at Cape Hatteras National Seashore
### All data are publicly available from [field reports](https://www.nps.gov/caha/learn/nature/upload/2018_CAHA_shorebirds_final-report_for-web.pdf). Visualization is done in R.
---
&nbsp;
##### 1. Library
```{r}
library(ggplot2)
```
&nbsp;
##### 2. Data
```{r}
OI<- read.csv("ocracoke_AMOY.csv", header=TRUE)
REKN<- as.data.frame(read.csv("REKN.csv", header = TRUE))
Districts<-as.data.frame(read.csv("2023REKN.csv", header=TRUE))
YearTotals<-as.data.frame(read.csv("YearTotals.csv", header = TRUE))
```
&nbsp;
##### 3. Using ggplot2 to plot the data
&nbsp; 3.1 Simple Bar Plot
```{r}
ggplot(
  data = REKN, 
  mapping = aes(
         x=Day, 
         y=Total.REKN,
         xmin=Day,
         xmax= 30)) +
geom_col(
  fill = "lightblue", # bar fill color 
  colour = "white") + # outline color
geom_line(
    colour = "black") + 
theme_minimal() # A simple theme with no background or lines.
```
