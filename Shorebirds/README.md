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
theme_minimal() + # A simple theme 
labs(y = "Total count of red knots", x = "Day in May of 2018") # Labeling the x & y axes
```
&nbsp; **Output:**

![alt text](https://github.com/gausec/CapeHatteras/blob/main/Results/REKN_bar.png?raw=true)

&nbsp; 3.2 Jitter Plot
```{r}
# Keep months in right order
Districts$Month<-factor(Districts$Month,levels = unique(Districts$Month),ordered = T)
``` 
```{r}
district_select <- Districts[Districts$District %in% c("Bodie", "Hatteras", "Ocracoke"), ]

ggplot(district_select, aes(Month, REKN)) +
geom_jitter(aes(col=District, size=REKN)) +
theme_minimal() +
labs( y = "Total count of red knots",
      x = "Day in May of 2018",
      title = "2018 Red Knot Data at Cape Hatteras National Seashore",
      size="Red knots" ) # Labeling the axes, title, and legend
```

&nbsp; **Output:**

![alt text](https://github.com/gausec/CapeHatteras/blob/main/Results/REKN_jitter.png?raw=true)

&nbsp; 3.2 Adding a linear trend line using the `geom_smooth` [function](https://ggplot2.tidyverse.org/reference/geom_smooth.html)

```{r}
ggplot(district_select, aes(Month, REKN)) +
geom_jitter(aes(col=District, size=REKN)) +
theme_minimal() +
labs( y = "Total count of red knots",
      x = "Day in May of 2018",
      title = "2018 Red Knot Data at Cape Hatteras National Seashore",
      size="Red knots" )+ # Labeling the axes, title, and legend
      geom_smooth(method = "lm", stat = "smooth") # To remove confidence interval around smooth, use se = FALSE
```

&nbsp; **Output:**

![alt text](https://github.com/gausec/CapeHatteras/blob/main/Results/REKN_jitter_trendline.png?raw=true)


