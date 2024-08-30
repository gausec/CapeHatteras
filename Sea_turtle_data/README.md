# Sea turtle data visualization using R
### Data is sourced from publicly available [field reports](https://www.nps.gov/caha/learn/nature/upload/2018_CAHA_Sea-turtle-report_final_report.pdf).

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
&nbsp; 3.1 Stacked bar plot where color corresponds to species and the Y-axis is the year.
```{r}
#Turtlesnocc <-
  ggplot(YearTurtle, aes(x = Year, y = Count, fill = Species.of.Sea.Turtle)) + 
  geom_bar(stat = "identity", color = "black") +
  
  scale_x_continuous(breaks=seq(2004,2024,by=1))+
  
   scale_y_continuous(breaks = seq(0, 50, by = 2))+
  theme_minimal()+
  labs(y = "Total Nests", 
       x = "Year",
       title = "Uncommon Sea Turtle Species Nesting at Cape Hatteras National Seashore",)+
  theme(plot.title = element_text(hjust = .3, vjust = 2.5, size = 18), axis.text = element_text(size=13), axis.title = element_text(size=14), axis.title.x = element_text(margin=margin(t=25)), axis.title.y = element_text(margin=margin(t=25) ))+
scale_fill_manual(values = c("#A9E190", "#FFB000", "#648FFF", "black"))

 

#ggsave("Turtles-nocc.png", plot = Turtlesnocc, width = 15, height = 8, dpi = 500)
```
&nbsp; **Output:**
![alt text](https://github.com/gausec/CapeHatteras/blob/main/Results/uncommon_sea_turtles_at_CAHA.png)
*Note: Legend was added outside of R Studio.*

&nbsp;

&nbsp; 3.2 Using the `geom_jitter` plot, I plotted the total number of strandings per year. The size of a dot represents the total number of strandings in a given year. Color corresponds to species.
```{r}
 ggplot(strand.spec, aes(Species, SpeciesTotal)) +
       geom_jitter(aes(col=Year, size=StrandingYearTotal, )) +
       theme_linedraw() +
       labs(y = "Species-specific totals", x = "Year") 
```
&nbsp; **Output:**

![alt text](https://github.com/gausec/CapeHatteras/blob/main/Results/Strandings.png?raw=true)

&nbsp;

&nbsp; 3.3 A variation of the jitter plot where color corresponds to year and the Y-axis is the species.
```{r}
 ggplot(strand.spec, aes(Species, SpeciesTotal)) +
       geom_jitter(aes(col=Year, size=StrandingYearTotal, )) +
       theme_linedraw() +
       labs(y = "Species-specific totals", x = "Year")
```


