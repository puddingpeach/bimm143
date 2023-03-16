Class 5: Data Visualization
================
Cynthia

# Plotting in R

R has multiple plotting and graphics systems. The most popular of which
is **ggplot2**.

We have already played with “base” R graphics. This comes along with R
“out of the box”.

``` r
plot(cars)
```

![](class05_files/figure-commonmark/unnamed-chunk-1-1.png)

Compared to base R plots ggplot is much more verbose - I need to write
more code to get simple plots like the above.

To use ggplot I need to first install the ggplot2 package. To install
any package in R I use the `install.packages()` command along with the
package name.

The install is a one time only requirement. The package is now on our
computer. I don’t need to re-install it.

However, I can’t just use it without leading it up with a `library()`
call.

``` r
library(ggplot2)
```

``` r
ggplot()
```

![](class05_files/figure-commonmark/unnamed-chunk-3-1.png)

All ggplot figures need at least 3 things:

-data (this is the data.frame with our numbers) -aesthetics (“aes”, how
our data maps to the plot) -geoms (do want lines, points, columns, etc…)

``` r
ggplot(data=cars) +
 aes(x=speed, y=dist) + geom_point() 
```

![](class05_files/figure-commonmark/unnamed-chunk-4-1.png)

I want a trend line to show the relationship between speed and stopping
distance…

``` r
ggplot(data=cars) +
 aes(x=speed, y=dist) + geom_point() + geom_line()
```

![](class05_files/figure-commonmark/unnamed-chunk-5-1.png)

That is not what we want

``` r
ggplot(data=cars) +
 aes(x=speed, y=dist) + geom_point() +geom_smooth() 
```

    `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](class05_files/figure-commonmark/unnamed-chunk-6-1.png)

``` r
bb <- ggplot( data=cars) + aes(x=speed, y=dist) + geom_point()

bb
```

![](class05_files/figure-commonmark/unnamed-chunk-7-1.png)

``` r
bb + geom_smooth(method = "lm", se=FALSE)
```

    `geom_smooth()` using formula = 'y ~ x'

![](class05_files/figure-commonmark/unnamed-chunk-8-1.png)

# Gene expression example

Read the dataset from online

``` r
url <-"https://bioboot.github.io/bimm143_S20/class-material/up_down_expression.txt"
genes <- read.delim(url)
head(genes, 10)
```

             Gene Condition1 Condition2      State
    1       A4GNT -3.6808610 -3.4401355 unchanging
    2        AAAS  4.5479580  4.3864126 unchanging
    3       AASDH  3.7190695  3.4787276 unchanging
    4        AATF  5.0784720  5.0151916 unchanging
    5        AATK  0.4711421  0.5598642 unchanging
    6  AB015752.4 -3.6808610 -3.5921390 unchanging
    7       ABCA7  3.4484220  3.8266509 unchanging
    8   ABCA9-AS1 -3.6808610 -3.5921390 unchanging
    9      ABCC11 -3.5288580 -1.8551732 unchanging
    10      ABCC3  0.9305738  3.2603040         up

``` r
head(genes)
```

            Gene Condition1 Condition2      State
    1      A4GNT -3.6808610 -3.4401355 unchanging
    2       AAAS  4.5479580  4.3864126 unchanging
    3      AASDH  3.7190695  3.4787276 unchanging
    4       AATF  5.0784720  5.0151916 unchanging
    5       AATK  0.4711421  0.5598642 unchanging
    6 AB015752.4 -3.6808610 -3.5921390 unchanging

``` r
nrow(genes)
```

    [1] 5196

``` r
colnames(genes)
```

    [1] "Gene"       "Condition1" "Condition2" "State"     

``` r
table(genes$State)
```


          down unchanging         up 
            72       4997        127 

``` r
ggplot(genes) + aes(Condition1, Condition2, color=State) + geom_point() + 
  labs(title= "Some Plot", subtitle="With a subtitle")
```

![](class05_files/figure-commonmark/unnamed-chunk-14-1.png)

I write some text I want **bold** or *italic*

``` r
p <- ggplot(genes) + 
    aes(x=Condition1, y=Condition2, col=State) +
    geom_point()
p
```

![](class05_files/figure-commonmark/unnamed-chunk-15-1.png)

``` r
p + scale_colour_manual( values=c("blue","gray","red") )
```

![](class05_files/figure-commonmark/unnamed-chunk-16-1.png)

``` r
p + scale_colour_manual(values=c("blue","gray","red")) +
    labs(title="Gene Expresion Changes Upon Drug Treatment",
         x="Control (no drug) ",
         y="Drug Treatment")
```

![](class05_files/figure-commonmark/unnamed-chunk-17-1.png)
