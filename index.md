---
title       : "Data Visualization"
subtitle    : Application with R and ggplot2
author      : Daniel Anderson
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : zenburn      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 
<style>
em {
  font-style: italic
}
</style>

<style>
strong {
  font-weight: bold;
}
</style>



## Agenda
* Very (very very) basic intro to R
* Intro to *ggplot2*
* Application

----
## What is R?
* A programming language
* Tremendously powerful and flexible statistical software that happens to be free
* No point-and-click interface
* Incredible array of external "packages" available for specialized analyses, data visualizations, or to automate much of the data "munging" process

----
## R as a big calculator


```r
3 + 2
```

```
## [1] 5
```


```r
(1/-(3/2)^2) / 2^-1/9
```

```
## [1] -0.09876543
```

------ &twocol
*** =left

# Object Assignment


```r
a <- 3
b <- 2
a + b
```

```
## [1] 5
```

```r
a / (a + b)
```

```
## [1] 0.6
```

*** =right

# Object re-assignment


```r
a <- 3
a
```

```
## [1] 3
```

```r
a <- 7
a
```

```
## [1] 7
```

------ &twocol
## Object Assignment (continued)
*** =left
Objects can be of a variety of types.


```r
string <- "Hello world!"
logical <- TRUE
double <- 3.2587021
Integer <- 6L
```
*** =right
In this case, we can't exactly do arithmetic with all of these. 
  For example


```r
string + double
```

```
## Error in string + double: non-numeric argument to binary operator
```
But, these objects can be extremely useful in programming.

------
## Playing a trick on my friend Shawn
Object assignment can be helpful to play a trick on somebody (this is one I 
  actually did with our friend from Ohio).
  

```r
Ducks <- 2
Buckeyes <- 1
```
Then clear the console, so they can't see the code you've previously written.

------ bg:url(/Users/Daniel/Dropbox/Teaching/CourseR/Weeks/Week1p1/assets/img/fightingduck.jpg)


```r
Ducks > Buckeyes
```

```
## [1] TRUE
```

```r
Ducks < Buckeyes
```

```
## [1] FALSE
```

```r
Buckeyes > Ducks
```

```
## [1] FALSE
```

---- .segue
# RStudio IDE Demo

---- .segue
# ggplot2

----
## The *ggplot2* package
Today, we'll be covering the basics of the *ggplot2* package. Much of this presentation is based on examples from the new *ggplot2* book.

![ggplotBook](./assets/img/ggplotBook.png)

----
## Underlying theory
* *ggplot2* is optimized for speed in exploratory plotting.
* Make ugly plots when exploring, but take the time to beautify them for publication
* Built on a grammar of graphics (not scatter plots, bar plots, etc.)


----
## Part of the many reasons Hadley is a cool guy

<div align = "left">
<img src = assets/img/freeggplot.png width = 1000 height = 500>
</div>

(It's no longer there, but if you want access to it let me know)


----
## Other resources
The *ggplot2* package is one of the most popular R packages. There are a plethora of resources to learn the syntax. 

* Perhaps the most definitive, and indexes all the capabilities of ggplot2, along with multiple examples 
	+ http://docs.ggplot2.org/current/index.html#

* RStudio cheat sheet can also be helpful
	+ https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf

* R Graphics Cookbook
	+ http://www.cookbook-r.com/Graphs/

----
## Install

We have to install the *ggplot2* package before we can use any of the functions within it.

Please run the following line of code (make sure you copy it exactly - every parentheses, quote, etc., matters).


```r
install.packages("ggplot2", dependencies = TRUE)
```

This will launch a window prompting you to select a mirror. Any will work - I typically use 0-Cloud.

![mirror](./assets/img/mirror.png)

----
## Load ggplot2
At this point, *ggplot2* is installed on your computer, but it is not loaded. In R, you have to install packages once, but load them each time you want to use them (Analogy: Books in a library).

We'll see how to load the package momentarily.

---- 
## Components
Every *ggplot* plot has three components

1. data
	* The data used to produce the plot
2. aesthetic mappings
	* between variables and visual properties
3. layer(s)
	* usually through the geom function to produce geometric shape to be rendered


----
## Basic syntax
![ggplotBasicSyntax](./assets/img/ggplotBasicSyntax.png)

Note that Hadley recommends putting each `geom_XXX` on a separate line to ease clarity. I agree with this suggestion, but will not be following it in these slides to help save space.




----
## mpg data
Dataset on cars and attributes about those cars, including their miles per gallon.


```r
library(ggplot2)
data(mpg)
head(mpg)
```

```
## # A tibble: 6 × 11
##   manufacturer model displ  year   cyl      trans   drv   cty   hwy    fl
##          <chr> <chr> <dbl> <int> <int>      <chr> <chr> <int> <int> <chr>
## 1         audi    a4   1.8  1999     4   auto(l5)     f    18    29     p
## 2         audi    a4   1.8  1999     4 manual(m5)     f    21    29     p
## 3         audi    a4   2.0  2008     4 manual(m6)     f    20    31     p
## 4         audi    a4   2.0  2008     4   auto(av)     f    21    30     p
## 5         audi    a4   2.8  1999     6   auto(l5)     f    16    26     p
## 6         audi    a4   2.8  1999     6 manual(m5)     f    18    26     p
## # ... with 1 more variables: class <chr>
```

----
## Quick caveat

* All the datasets within the *ggplot2* package are in a *tidy* format.
* Tidy, in this case, is a technical term
* *ggplot2* is optimized for tidy data
	+ possible to use without, but better to use tidy data
* The concept of tidy data is beyond the scope of this presentation, but I have other presentations on tidy data. Contact me if you're interested.


----
## Simple example


```r
data(mpg)
ggplot(mpg, aes(x = displ, y = hwy)) + geom_point()
```

![plot of chunk mpgEx1](assets/fig/mpgEx1-1.png)

----
## Quick example 2
Note that the only thing that has changed here is the `geom` 


```r
data(mpg)
ggplot(mpg, aes(x = displ, y = hwy)) + geom_smooth()
```

![plot of chunk mpgEx2](assets/fig/mpgEx2-1.png)

----
## Add an additional layer


```r
ggplot(mpg, aes(x = displ, y = hwy)) + geom_point() + geom_smooth()
```

![plot of chunk mpgEx3](assets/fig/mpgEx3-1.png)

----
## Add an additional aesthetic


```r
ggplot(mpg, aes(x = displ, y = hwy, color = class)) + geom_point() 
```

![plot of chunk mpgEx4](assets/fig/mpgEx4-1.png)

----
## Add smooth line for each class
# Too busy
Note the below spits out some warnings because of the sparsity of the data. I've suppressed them here.


```r
ggplot(mpg, aes(x = displ, y = hwy, color = class)) + geom_point() +
 geom_smooth()
```
![plot of chunk mpgEx5b](assets/fig/mpgEx5b-1.png)

----
## Remove SE


```r
ggplot(mpg, aes(x = displ, y = hwy, color = class)) + geom_point() +
 geom_smooth(se = FALSE)
```

![plot of chunk mpgEx6b](assets/fig/mpgEx6b-1.png)

----
## Change the color of all points


```r
ggplot(mpg, aes(x = displ, y = hwy)) + geom_point(color = "purple") +
 geom_smooth(se = FALSE)
```

![plot of chunk mpgEx7](assets/fig/mpgEx7-1.png)

---- .segue
# Can you guess how we would change the line color?

----


```r
ggplot(mpg, aes(x = displ, y = hwy)) + geom_point(color = "purple") +
 geom_smooth(se = FALSE, color = "gray", size = 2, linetype = "dashed")
```

![plot of chunk mpgEx8](assets/fig/mpgEx8-1.png)

----
Worth mentioning, traditional calls to line color/type/size also work


```r
ggplot(mpg, aes(x = displ, y = hwy)) + geom_point(color = "purple") +
 geom_smooth(se = FALSE, col = "gray", lwd = 2, lty = "dashed")
```

![plot of chunk mpgEx9](assets/fig/mpgEx9-1.png)

----
## Change the "wiggliness" of the smoother


```r
ggplot(mpg, aes(x = displ, y = hwy)) + geom_point(color = "purple") +
 geom_smooth(span = 0.2)
```

![plot of chunk mpgEx10](assets/fig/mpgEx10-1.png)

----
## Geoms for two continuous variables


|Geoms     |Description                                                              |Code             |
|:---------|:------------------------------------------------------------------------|:----------------|
|jitter    |Jitter points (to avoid overlapping)                                     |geom_jitter()    |
|point     |Plot points at each x&#124;y intersection                                |geom_point()     |
|quantile  |Plot lines from quantile regression                                      |geom_quantile()  |
|rug       |Plot 1d scatterplot on margins (stripchart)                              |geom_rug()       |
|smooth    |Plot a smoothing function (many smoothers available)                     |geom_smooth()    |
|text      |Add text annotations                                                     |geom_text()      |
|bin2d     |Bin observations that are close together and color according the density |geom_bin2d()     |
|density2d |Contour lines of the data density                                        |geom_density2d() |
|hex       |Hexagonal bins of data colored according to their density                |geom_hex()       |

----
## Guided practice
* Load the *ggplot2* package. 
* Load the diamonds dataset with `data(diamonds)`
* Set and store the data and aesthetics, in an object `p`, using the following code


```r
data(diamonds)
p <- ggplot(diamonds, aes(carat, price))
```
* Print `p`. What do you see?
* Explore different geoms, with `p + geom_XXX()`(`geom_hex()` requires the *hexbin* package). For example, a basic scatterplot could be produced with


```r
p + geom_point()
```

* Add at least one additional layer (i.e., produce a plot with at least two layers)


-----
## Some possibilities




```r
p + geom_point()
```

![plot of chunk guidedp1_3b](assets/fig/guidedp1_3b-1.png)

----
## Probably better


```r
p + geom_hex()
```

![plot of chunk guidedp1_3c](assets/fig/guidedp1_3c-1.png)

----
## Another similar alternative

```r
p + geom_bin2d()
```

![plot of chunk guidedp1_3d](assets/fig/guidedp1_3d-1.png)

----
## Yet another alternative


```r
p + geom_point(alpha = 0.01) + geom_density2d(color = "red")
```

![plot of chunk guidedp1_3e](assets/fig/guidedp1_3e-1.png)

-----
## Quantiles
Defaults to the 25th, 50th, and 75th percentiles
 

```r
p + geom_quantile()
```

![plot of chunk guidedp1_4](assets/fig/guidedp1_4-1.png)

-----
## Quantiles
Change the quantiles to deciles (from 10th to 90th)


```r
p + geom_quantile(quantiles = seq(0.1, 0.9, 0.1))
```

![plot of chunk guidedp1_5](assets/fig/guidedp1_5-1.png)

----
## Add an extra layer


```r
p + geom_point() + geom_rug() + geom_smooth()
```

![plot of chunk guidedp1_6](assets/fig/guidedp1_6-1.png)

----
## Color by cut


```r
p2cut <- ggplot(diamonds, aes(carat, price, color = cut))
p2cut + geom_point()
```

![plot of chunk guidedp1_7](assets/fig/guidedp1_7-1.png)

----
## Color by color


```r
p2color <- ggplot(diamonds, aes(carat, price, color = color))
p2color + geom_point()
```

![plot of chunk guidedp1_8](assets/fig/guidedp1_8-1.png)

----
## Color by clarity


```r
p2clarity <- ggplot(diamonds, aes(carat, price, color = clarity))
p2clarity + geom_point()
```

![plot of chunk guidedp1_9](assets/fig/guidedp1_9-1.png)

----
## geoms: One variable


|Geoms                  |Description                                                |Code                    |
|:----------------------|:----------------------------------------------------------|:-----------------------|
|area                   |Filled area plot                                           |geom_area(stat = "bin") |
|density                |Density plot                                               |geom_density()          |
|dotplot                |Stacked dotplot, with each dot representing an observation |geom_dotplot()          |
|polygon of Frequencies |Polygon of frequencies                                     |geom_freqpoly           |
|histogram              |Standard histogram                                         |geom_histogram          |
|barplot                |Standard barchart                                          |geom_bar                |

----
## Area plot

```r
price <- ggplot(diamonds, aes(price)) 
price + geom_area(stat = "bin")
```

![plot of chunk geom_area](assets/fig/geom_area-1.png)

----
# Frequency polygons

```r
price + geom_freqpoly()
```

![plot of chunk geom_freqPoly](assets/fig/geom_freqPoly-1.png)

----
## Evaluate frequencies by *cut*


```r
price2 <- ggplot(diamonds, aes(price, color = cut))
price2 + geom_freqpoly(bins = 50)
```

![plot of chunk geom_freqPolyClarity](assets/fig/geom_freqPolyClarity-1.png)

----
## Histograms

```r
price + geom_histogram()
```

![plot of chunk geom_histogram1](assets/fig/geom_histogram1-1.png)

----
# Change binwidth

```r
price + geom_histogram(binwidth = 5)
```

![plot of chunk geom_histogram2](assets/fig/geom_histogram2-1.png)

----
## Barplots


```r
ggplot(mpg, aes(trans)) + geom_bar()
```

![plot of chunk barplot1](assets/fig/barplot1-1.png)

---- .segue
# Plotting categorical variables

----
## boxplots
Note that the categorical variable must be categorical or declared as a factor


```r
bp <- ggplot(mpg, aes(drv, hwy))
bp + geom_boxplot()
```

![plot of chunk boxplots1](assets/fig/boxplots1-1.png)

---- &twocol
## stripcharts

*** =left


```r
bp + geom_point()
```

![plot of chunk stripcharts1](assets/fig/stripcharts1-1.png)

*** =right


```r
bp + geom_jitter()
```

![plot of chunk jitterchart1](assets/fig/jitterchart1-1.png)

-----
## Control the amount of jittering


```r
bp + geom_jitter(width = 0.3, height = 0)
```

![plot of chunk jitter](assets/fig/jitter-1.png)

----
## Useful together


```r
bp + geom_boxplot() + geom_jitter(width = 0.3, height = 0)
```

![plot of chunk boxplotJitter](assets/fig/boxplotJitter-1.png)

----
## Usually better: Violin plots


```r
bp + geom_violin()
```

![plot of chunk violin](assets/fig/violin-1.png)

----
## And can also be combined with data


```r
bp + geom_violin() + geom_jitter(width = 0.3, height = 0)
```

![plot of chunk violin_data](assets/fig/violin_data-1.png)

--- .segue
# Faceting

----
## Produce separate plots according to a specific variable
Back to the mpg dataset:
* Produce a separate plot of the relation between engine size and highway miles per gallon for each car type.


```r
hwy <- ggplot(mpg, aes(displ, hwy))
hwy + geom_point() + facet_wrap(~class)
```

![plot of chunk faceting1](assets/fig/faceting1-1.png)

----
## Add a linear function to each plot


```r
hwy <- ggplot(mpg, aes(displ, hwy))
hwy + geom_point() + geom_smooth(method = "lm") + facet_wrap(~class)
```

![plot of chunk faceting2](assets/fig/faceting2-1.png)

----
## Different faceting
`facet_wrap` vs `facet_grid`

![faceting](./assets/img/faceting.png)

----
## Two variables


```r
hwy + geom_point() + facet_grid(drv ~ cyl)
```

![plot of chunk facetGrid3](assets/fig/facetGrid3-1.png)

----
## Two variables

(The LOESS estimator spits out warnings here again)


```r
hwy + geom_point() + geom_smooth(span = 2) + facet_grid(drv ~ cyl)
```

![plot of chunk facetGrid4](assets/fig/facetGrid4-1.png)

---- &twocol
## Faceting vs Grouping

*** =left


```r
ggplot(mpg, 
	aes(displ, hwy, color = factor(drv))) + 
	geom_point()
```

![plot of chunk facetGrouping1](assets/fig/facetGrouping1-1.png)

*** =right


```r
ggplot(mpg, aes(displ, hwy)) + 
	geom_point() + 
	facet_wrap(~ drv)
```

![plot of chunk facetGrouping2](assets/fig/facetGrouping2-1.png)

----
## Guided practice

You can view the probability density distributions of city miles per gallon by drive-train (four-wheel, front, rear) with the following code.


```r
base <- ggplot(mpg, aes(cty, fill = drv))
base + geom_density(alpha = 0.4) 
```
* First run this code. What do you see? Add `bw = 5` to the `geom_density` function. What happens? Which gives you a better view of the data?

* Add a facet to the plot, to view these three distributions by *year*. Have things changed from 1999 to 2008?

* Modify the code to group by *year* (use `fill = factor(year)` **NOT** `fill = year`) and facet by *drv*. Which do you 
  prefer?

----
Change the binwidth of the densities


```r
base + geom_density(alpha = 0.4, bw = 5)
```

![plot of chunk guidedp2_2](assets/fig/guidedp2_2-1.png)

---
Add a facet to the plot, to view these three distributions by *year*.


```r
base + geom_density(alpha = 0.4) + facet_wrap(~year)
```

![plot of chunk guidedp2_3](assets/fig/guidedp2_3-1.png)

----
Group by *year* and facet by *drv*


```r
base2 <- ggplot(mpg, aes(cty, fill = factor(year)))
base2 + geom_density(alpha = 0.4) + facet_wrap(~drv)
```

![plot of chunk guidedp2_4](assets/fig/guidedp2_4-1.png)

---- .segue
# Themes (quickly, if there's time)

----
## Overview of themes
* Themes do not change how the data are rendered
* Only change visual properties
* Many built-in themes
	+ Even more available through extension packages (specifically *ggthemes*)
* Fully customizable (though the syntax becomes lengthier)

----
## theme_gray (default)


```r
baseP <- ggplot(economics, aes(date, unemploy)) + geom_line()
baseP + theme_gray()
```

![plot of chunk theme_gray](assets/fig/theme_gray-1.png)

----
## theme_bw


```r
baseP + theme_bw()
```

![plot of chunk theme_bw](assets/fig/theme_bw-1.png)

----
## theme_classic


```r
baseP + theme_classic()
```

![plot of chunk theme_classic](assets/fig/theme_classic-1.png)

----
## theme_dark


```r
baseP + theme_dark()
```

![plot of chunk theme_dark](assets/fig/theme_dark-1.png)

----
## theme_minimal


```r
baseP + theme_minimal()
```

![plot of chunk theme_minimal](assets/fig/theme_minimal-1.png)

----
## Further customization
* See http://docs.ggplot2.org/dev/vignettes/themes.html
* See *ggplot2* book, Chapter 8

<br>
**Take Home Message:** If you want it to look a certain way, you can do it (essentially nothing is impossible). Often there are others who have developed themes that will be close to what you want, which is easier than developing your own theme (although that can be rewarding in its own right).

