GSS Analysis 2018
================

This project will serve to showcase a number of data and survey analysis
techniques to explore the data from the 2018 General Social Survey.
These data can be found
[here](https://www.thearda.com/Archive/Files/Downloads/GSS2018_DL2.asp).
For the purpose of this project, I will be using variables such as
*POLVIEWS*, *INCOME16*, *EDUC*, and others to showcase insights.

``` {r}
```

First we need to load in the data and some packages.

``` {r}
library(tidyverse)
library(dplyr)
library(ggplot2)
library(caret)
library(readr)
library(plotly)
library(readxl)
library(psych)

set.seed(12345)
setwd("C:/Users/jorda/OneDrive/Desktop/Data Projects/Survey Analysis")
data <- read_excel("gss2018.XLSX")
```

Now let’s take a look at some of the variables.

``` {r}
describe(data$POLVIEWS) #descriptive statistics

table(data$POLVIEWS) #breakdown of values
```

In this case *POLVIEWS* breaks down as follows:

1)  Extremely liberal
2)  Liberal
3)  Slightly liberal
4)  Moderate, middle of the road
5)  Slightly conservative
6)  Conservative
7)  Extremely conservative
8)  Don’t know
9)  No answer

As we can see the mean response here is 4.23 which would be inbetween
moderate and slightly conservative. However, since all the values are
numeric, 8 and 9, corresponding to “Don’t know” and “No answer”
respectively, throw off the meaning of the descriptive statistics. For
the data set, we have *n = 2,348*, and the extra values in this case
only account for 101 entries, so taking them out would still leave us
with a healthy sample population. We do this with the following.

``` {r}
data_polviews <- filter(data, POLVIEWS < 8)

table(data_polviews$POLVIEWS)
```

Now we only have the response values so we can check the descriptive
statistics agian.

``` {r}
describe(data_polviews$POLVIEWS)
```

Now we can see that removing these value decreased the mean by 0.2,
indicating that the actual mean is much closer to moderate, though ever
so slightly still leaning slightly conservative.

Additionally, I will follow the same steps to clean the *INCOME16*
variable. The response values breakdown as follows:

1)  Under $1,000
2)  $1,000 to 2,999
3)  $3,000 to 3,999
4)  $4,000 to 4,999
5)  $5,000 to 5,999
6)  $6,000 to 6,99
7)  $7,000 to 7,999
8)  $8,000 to 9,999
9)  $10,000 to 12,499
10) $12,500 to 14,999
11) $15,000 to 17,499
12) $17,500 to 19,999
13) $20,000 to 22,499
14) $22,500 to 24,999
15) $25,000 to 29,999
16) $30,000 to 34,999  
17) $35,000 to 39,999  
18) $40,000 to 49,999  
19) $50,000 to 59,999  
20) $60,000 to 74,999  
21) $75,000 to 89,999  
22) $90,000 to 109,999  
23) $110,000 to 129,999
24) $130,000 to 149,999
25) $150,000 to 169,999
26) $170,000 or over  
27) Refused
28) Don’t know

<!-- end list -->

``` {r}
table(data_polviews$INCOME16)
describe(data_polviews$INCOME16)

#using the newly created data_polviews
data_income <- filter(data_polviews, INCOME16 < 27)

plot1 <- ggplot(data_income, aes(factor(POLVIEWS), INCOME16)) +
  geom_boxplot(aes(fill = factor(POLVIEWS)))
```
