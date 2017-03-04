---
output:
  pdf_document: default
  html_document: default
---
# Using R with Two Variables

***

I continue to explore the dimoands dataset which I worked with in 'problemsetone'. So, let's load the dataset into the environment.

## A Scatterplot of Price vs X(Length in mm)

First, I load the data and get a short summary on what I have in it.

```{r}
#Load the ggplot package
library(ggplot2)

#Load the diamonds dataset
data("diamonds")

#Getting a summary from the dataset
summary(diamonds)
```

Now I create the scatterplot of price vs x. I use `geom_point()` function to get the scattered format from my plot. 

```{r}
ggplot(aes(x = x, y = price),
       data = diamonds) +
  xlab('Length in mm (x)') +
  ylab('Price in US dollars') +
  geom_point()
```

**Observations:**

- In general the majority length of the diamond is concentrated somewhere above 3mm up to 9mm
- There are a few outliers with length of zero, and a few more with length above 9mm
- The price goes higher as the length of the diamond increases. The distribution looks exponential. The change in price is more steep between 0-5000 dollars, which is for lengths between 3mm-7mm, and from there the change seems to be much slower 

**Some Correlations:**

### What is the correlation between price and x (length in mm)?
```{r}
with(diamonds, cor.test(diamonds$price, diamonds$x, method = 'pearson'))
```

### What is the correlation between price and y (width in mm)?
```{r}
with(diamonds, cor.test(diamonds$price, diamonds$y))
```

### What is the correlation between price and z (depth in mm)?
```{r}
with(diamonds, cor.test(diamonds$price, diamonds$z))
```

***

## A Simple Scatterplot of Price vs Depth

```{r}
ggplot(aes(x = price, y = depth),
       data = diamonds) +
  xlab('Price in dollars') +
  ylab('Depth') +
  geom_point()
```

To get a better look of this plot and play around with it a bit, I want to change the code to make the transparency of the points to be 1/100 of what they are now and mark the x-axis every 2 units.
- The transparency of 1/100 means that for every 100 dots on the scatterplot, 1 will be shown
- Marking the x-axis every 2 unit is with regards to how I want to scale the x-axis

```{r}
ggplot(aes(x = price, y = depth),
       data = diamonds) +
  xlab('Price in dollars') +
  ylab('Depth') +
  geom_point(alpha = 1/100) +
  scale_y_continuous(breaks = seq(0, 80, 2)) +
  coord_cartesian(ylim = c(54, 68)) #To zoom in on the plot on the y-axis
```

Based on the scatterplot most diamonds are between 58-64 value of depth.

**Some Correlations:**

### What is the correlation of depth vs price?
```{r}
with(diamonds, cor.test(diamonds$price, diamonds$depth), method = 'pearson')
```

### Based on the correlation coefficient, would you use depth to predict the price of a diamond?

My response to this question would be no. The correlation coefficient -0.01 is too small to be able to give insights with regards to predicting one variable based on the other. 

***

## A Simple Scatterplot of Price vs Carat

With this plot, I also omit the top 1% of price and carat values.

```{r}
ggplot(aes(x = price, y = carat),
       data = subset(diamonds, price < quantile(diamonds$price, 0.99),
                     carat < quantile(diamonds$carat, 0.99))) +
  geom_point()
```

***

## Scatterplot of Price vs. Volume (x x y x z)

```{r}
#Calculating a rough estimation of volume based on length, width and depth of the diamong
diamonds$volume <- diamonds$x * diamonds$y * diamonds$z

ggplot(aes(x = volume, y = price),
       data = diamonds) +
  geom_point()
```

** Observations **

- There are two outliers which are significantly placed for a volum close to 1000. There is one more significant outlier with a volume close to 4000.
- There are also a few outliers with a volume of zero (this goes back to any of the x, y, or z variables being zero which makes the multiplication zero)
- The relationship between volume and price seems to be exponential-- as volume increases, the price increases as well but with a much faster speed

**Some Correlations:**

### What is the correlation of price and volume, excluding the outliers that are either zero or greater than 800?

To calculate the correlation, I create a new dataframe which contains the volume without the outliers mentioned in the question. This makes my job easier, later when I want to see the correlation between price and volume.

I name the dataframe 'diamonds_volume_without_outliers'. This dataframe will have the same number of variables as the diamonds dataset (i.e. 12), but will have fewer observations, since I am excluding any volume that is zero or above 800.

```{r}
#
diamonds_volume_without_outliers <- subset(diamonds, volume > 0 & volume < 800)
  
with(diamonds, cor.test(diamonds_volume_without_outliers$price, diamonds_volume_without_outliers$volume))
```

### More Adjusments

After subseting the data to exclude volumes that are zero or greater than 800, I want to adjust the transparency of the points and add a linear model to the plot. 

I will also scale the x and y axis to show part of the plot that contains scatters (aka. points).

I use geom_smooth(method = 'lm') to add a linear model to the plot and I chose the color red for it to be more visible on black.

```{r}
ggplot(aes(x = volume, y = price),
       data = diamonds_volume_without_outliers) +
  scale_y_continuous(limits = c(0, 20000), breaks = seq(0, 20000, 2000)) +
  scale_x_continuous(breaks = seq(0, 800, 100)) +
  geom_point(alpha = 1/30, color = 'red') +
  geom_smooth(method = 'lm', color = 'black')
```

### Is This Plot a Suitable Model to Estimate the Price od Diamonds?

Although the correlation value that I calculated for price vs. volume is 0.92 which is a high number, using a plot with a linear model is not helpful to estimate the price of the diamonds.

***

## Mean Price by Clarity

I create a new dataframe and group the diamonds using their clarity, and calculate their mean, median, minimum and maximum values:

```{r}
library(dplyr)

diamondsByClarity <- diamonds %>%
  group_by(clarity) %>%
  summarise(mean_price = mean(price),
            median_price = median(price),
            min_price = min(price),
            max_price = max(price),
            n = n()) #number of diamonds with a specific clarity
head(diamondsByClarity)
```

### Bar Charts of Mean Price

I created summary data frames with the mean price by clarity and color
```{r}
library(gridExtra)

#By clarity
diamonds_by_clarity <- group_by(diamonds, clarity)

#For each category of clarity, what is the mean price?
diamonds_mp_by_clarity <- summarise(diamonds_by_clarity, mean_price = mean(price))

p1 <- ggplot(aes(x = clarity, y = mean_price),
             data = diamonds_mp_by_clarity) + 
  geom_bar(stat = 'identity', fill = I('#85C477'))

#By color
diamonds_by_color <- group_by(diamonds, color)

#For each category of color, what is the mean price?
diamonds_mp_by_color <- summarise(diamonds_by_color, mean_price = mean(price))

p2 <- ggplot(aes(x = color, y = mean_price),
             data = diamonds_mp_by_color) +
  geom_bar(stat = 'identity', fill = I('#7787C4'))

grid.arrange(p1, p2, ncol = 1)

```

** Observations **

- Regarding the clarity, seems the best clarity has a lower mean price than the worst calrity. SI2 with a low clarity has the largest mean price while clarity wise it is not on a good level.
- Regarding the color, seems the best color (D) also has the lowest mean price after E. The worst color (J) has the highest mean price.

With these observations, it looks odd how diamonds with bad clarity and bad colors have higher mean prices.


