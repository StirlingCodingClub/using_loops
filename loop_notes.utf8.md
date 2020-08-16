---
title: "Using loops in coding"
author: "Brad Duthie"
date: "19 August 2020"
output:
  pdf_document: default
  html_document:
    code_folding: show
bibliography: loop_notes.bib
---

Contents
================================================================================

********************************************************************************

**Note: Please think of this document as a living document, which you are free to improve (like a [wiki](https://en.wikipedia.org/wiki/Wiki)) with minor edits, new sections that others might find useful, or [additional resources](#whatelse) that you find that you think others might also find useful. After reading through this, you should have a working understanding of what a loop is and how to use it in your own coding.**

********************************************************************************

- [Introduction: What is a loop?](#what_is_loop)
- [The for loop in R: getting started](#for_gs)
- [The for loop in R: a real example](#for_re)
- [The for loop in R: nested loops](#for_more)
- [The while loop in R](#while_loop)
- [Practice problems](#practice)
- [Additional resources](#whatelse)

********************************************************************************

<a name="what_is_loop">Introduction: What is a loop?</a>
================================================================================

Being able to use loops is a critical skill in programming and working with large arrays of data. Loops make it possible to repeat a set of instructions (i.e., code) `for` a particular set of conditions (e.g., for a range of numbers from 1 to 1000), or `while` a set of conditions still applies (e.g., while a value is still greater than zero). Hence, the use of [for loops](https://en.wikipedia.org/wiki/For_loop) and [while loops](https://en.wikipedia.org/wiki/While_loop) are fundamental for writing and running code efficiently (note that [other types](https://en.wikipedia.org/wiki/Do_while_loop) of loops also exist, but I will not focus on them now). Here I will introduce the key concepts of programming with loops, with particular emphasis on getting started with some practical uses of loops in the R programming language for scientific researchers.

The R programming language includes many base level functions to perform tasks that would otherwise require loops (e.g., functions such as [apply](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/apply) and [tapply](https://www.rdocumentation.org/packages/base/versions/3.5.2/topics/tapply), which effectively repeat a set of instructions to summarise values in an array). Tens of thousands of downloadable [packages](https://cran.r-project.org/) (code, data, and documentation bundled together, written by and for R users) are available in R, most of which include their own functions that can perform specific tasks required in scientific research (e.g., [vegan](https://github.com/vegandevs/vegan), [dplyr](https://dplyr.tidyverse.org/), and [shiny](https://github.com/rstudio/shiny)). Hence, successful data analysis in R can often just be a matter of finding and using an appropriate and reliable package for a given task. Nevertheless, unique data sets and models often require unique code, so base and package functions cannot always be found to do custom tasks. In many situations, the ability to use loops to repeat tasks will make it possible to quickly and confidently develop reproducible code in data analysis. In the long term, this will likely save time; in the short term, it creates an opportunity to develop and practice coding skills.

Below I will demonstrate how to use [for loops](https://en.wikipedia.org/wiki/For_loop) and [while loops](https://en.wikipedia.org/wiki/While_loop).

- A **for loop** iterates a set of instructions *for* a predetermined set of conditions (i.e., when you know how many times you need to iterate the same set of instructions)
- A **while loop** iterates a set of instructions *while* some condition(s) remains satisfied (i.e., when you might not know how many times you need to iterate the same set of instructions, but you do know when the iterations need to stop)

It is not important to completely understand the two definitions above before getting started, just as it is not important to understand a verbal definition of 'multiplication' before learning to multiply two numbers. Seeing examples of loops in practice will make it clear how they work and when to use them. In the next section, I will therefore start with some key examples to show how for loops can be used in R. I will then do the same with while loops. Finally, I will provide some practice problems and additional resources for using loops in programming.

<a name="for_gs">The for loop in R: getting started</a>
================================================================================

Different languages have differ syntaxes for writing for loops. In R, the syntax is as follows:


```r
for(index in set_of_conditions){
  # Code that gets repeated for each condition
}
```

In the above, anything within the bracketed `{` `}` gets repeated with `index` being substituted, sequentially, for all possible conditions `in` the `set_of_conditions`. A more concrete example will help:


```r
for(i in 1:10){
  print(i);
}
```

We can interpret the line `for(i in 1:10)` verbally to explain what is going on in plain English:

> Substitute the index `i` for each value from 1 to 10 (i.e., 1, 2, 3, ..., 8, 9, 10), and run the following bracketed code with each value in sequence. In other words, run the bracketed code first with `i = 1`, then with `i = 2`, and so forth until finishing the loop with `i = 10`. 

Given the above explanation, we can predict what will happen with the example code above, which I now run below.


```r
for(i in 1:10){
  print(i);
}
```

```
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
```

The code has printed integers from 1 to 10. This is obviously a very simple example of using a loop, but it highlights the basic idea. **There are three key points that I want to note with this example before moving on**

**1. the above for loop is effectively doing the same as the code below**


```r
print(1);
print(2);
print(3);
print(4);
print(5);
print(6);
print(7);
print(8);
print(9);
print(10);
```


```
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
```

In the above, I have [unrolled](https://en.wikipedia.org/wiki/Loop_unrolling) the for loop that printed off integers from 1 to 10. But the result is the same. The advantage of using the loop is that it avoids the need to repeat the same code more times than is necessary (consider if we wanted to print values from 1 to 10000 -- much less needs to be changed when using the for loop, and much fewer lines of code need to be written). There is no hard rule for when to use a loop versus when to repeat the same line(s) of code multiple times; it is generally best to use whichever method is most readable to (future) you. In practice, when getting started, it might help to think about what the loops would look like if unrolled -- or even write them both ways to confirm that a loop is working as intended.

**2. There is nothing special about `i`**

In a lot of books and online examples introducing loops, the index `i` is used as it is in my above example. But there is nothing special about `i`, just as there is nothing special about the variable `x` in algebra. The index `i` just serves as a placeholder for whatever actual value is going to be substituted from the set of conditions (i.e., values from 1 to 10 in the above example). We get the exact same result with the following code:


```r
for(value_to_be_printed in 1:10){
  print(value_to_be_printed);
}
```

```
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
```

The above use of the long `value_to_be_printed` instead of the shorter `i` seems unnecessary at first, but it is actually often helpful to give indices specific names like this to make code more readable. Doing so becomes especially helpful when working with multiple indices and loops within loops (an example of this later), or when the number of lines between the starting `{` and ending `}` brackets becomes larger than can be viewed on a computer screen.

**3. There is nothing special about `1:10`**

A lot of introductions to for loops in R will show the set of values to be iterated in this way, but there are equally acceptable ways to write it. For example, consider the below:


```r
for(i in c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)){
  print(i);
}
```

```
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
```

Or even the below, where I first define the set of values with its own variable named `the_set`:


```r
the_set <- c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
for(i in the_set){
  print(i);
}
```

```
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
```

The order of numbers **does** matter. For example, we could reverse the order in which numbers are printed by reversing the set of values:


```r
for(i in 10:1){
  print(i);
}
```

```
## [1] 10
## [1] 9
## [1] 8
## [1] 7
## [1] 6
## [1] 5
## [1] 4
## [1] 3
## [1] 2
## [1] 1
```

We could even print off the numbers in a random order with the below:


```r
random_vec <- sample(x = 1:10, size = 10);
for(i in random_vec){
  print(i);
}
```

```
## [1] 6
## [1] 1
## [1] 2
## [1] 4
## [1] 3
## [1] 5
## [1] 7
## [1] 10
## [1] 8
## [1] 9
```

It is unlikely that there would ever be a need to reverse the order of a set, and for most for loops, the simple `1:N` format will usually be all that that is needed. The point is that there is no reason to feel *constrained* to using this format when writing loops.

<a name="for_re">The for loop in R: a real example</a>
================================================================================

The examples above were intended only to introduce the general idea of using for loops, and their specific syntax in R. In coding, there is rarely such a need to use for loops to simply print off values. More often, for loops are used to repeat the same set of (often complex) instructions for a set of values. As a real example, I will use use the `nhtemp` data set in R.


```r
data(nhtemp); # Reads in the data set
```

The `nhtemp` data set includes a vector that stores the mean annual temperature in degrees Fahrenheit in [New Haven](https://www.google.com/maps/place/New+Haven,+CT,+USA/@40.5046762,-74.5979605,6.75z/data=!4m5!3m4!1s0x89e7d8443a8070e5:0xf6a354c659b264ed!8m2!3d41.308274!4d-72.9278835), Connecticut (USA), from 1912 to 1971.


```r
print(nhtemp);
```

```
## Time Series:
## Start = 1912 
## End = 1971 
## Frequency = 1 
##  [1] 49.9 52.3 49.4 51.1 49.4 47.9 49.8 50.9 49.3 51.9 50.8 49.6 49.3 50.6 48.4
## [16] 50.7 50.9 50.6 51.5 52.8 51.8 51.1 49.8 50.2 50.4 51.6 51.8 50.9 48.8 51.7
## [31] 51.0 50.6 51.7 51.5 52.1 51.3 51.0 54.0 51.4 52.7 53.1 54.6 52.0 52.0 50.9
## [46] 52.6 50.2 52.6 51.6 51.9 50.5 50.9 51.7 51.4 51.7 50.8 51.9 51.8 51.9 53.0
```

In the above data, the first value 49.9 is therefore the mean temperature from 1912, and the last value 53 is the mean temperature from 1971. We can print these off by using the indices `nhtemp[1]` and `nhtemp[60]` (as there are `length(nhtemp)` = 60 temperature years in `nhtemp`).


```r
print(nhtemp[1]);
```

```
## [1] 49.9
```

```r
print(nhtemp[60]);
```

```
## [1] 53
```

We might want to use these data to analyse how the temperature in New Haven has changed over the years from 1912-1972. The first task would likely be to convert the temperatures from Fahrenheit to Celsius. The formula for conversion is as follows,

$$T_{Celsius} = \frac{5}{9}(T_{Fahrenheit} - 32).$$

To get $T_{Celsius}$, it is not actually necessary to use a for loop in R; this can be done in one line of code:


```r
T_Celsius <- (5/9) * (nhtemp - 32);
print(T_Celsius);
```

```
## Time Series:
## Start = 1912 
## End = 1971 
## Frequency = 1 
##  [1]  9.944444 11.277778  9.666667 10.611111  9.666667  8.833333  9.888889
##  [8] 10.500000  9.611111 11.055556 10.444444  9.777778  9.611111 10.333333
## [15]  9.111111 10.388889 10.500000 10.333333 10.833333 11.555556 11.000000
## [22] 10.611111  9.888889 10.111111 10.222222 10.888889 11.000000 10.500000
## [29]  9.333333 10.944444 10.555556 10.333333 10.944444 10.833333 11.166667
## [36] 10.722222 10.555556 12.222222 10.777778 11.500000 11.722222 12.555556
## [43] 11.111111 11.111111 10.500000 11.444444 10.111111 11.444444 10.888889
## [50] 11.055556 10.277778 10.500000 10.944444 10.777778 10.944444 10.444444
## [57] 11.055556 11.000000 11.055556 11.666667
```

But if we know in advance that we will be doing some more complex data manipulation later, in might make sense to start out doing the conversion within a loop instead. To use a loop, we can first define the vector `T_Celsius`, then apply the conversion for each value in `nhtemp`.


```r
T_Celsius <- NULL;
for(year in 1:length(nhtemp)){
  T_Celsius[year] <- (5/9) * (nhtemp[year] - 32);
}
print(T_Celsius);
```

```
##  [1]  9.944444 11.277778  9.666667 10.611111  9.666667  8.833333  9.888889
##  [8] 10.500000  9.611111 11.055556 10.444444  9.777778  9.611111 10.333333
## [15]  9.111111 10.388889 10.500000 10.333333 10.833333 11.555556 11.000000
## [22] 10.611111  9.888889 10.111111 10.222222 10.888889 11.000000 10.500000
## [29]  9.333333 10.944444 10.555556 10.333333 10.944444 10.833333 11.166667
## [36] 10.722222 10.555556 12.222222 10.777778 11.500000 11.722222 12.555556
## [43] 11.111111 11.111111 10.500000 11.444444 10.111111 11.444444 10.888889
## [50] 11.055556 10.277778 10.500000 10.944444 10.777778 10.944444 10.444444
## [57] 11.055556 11.000000 11.055556 11.666667
```

There are a few things to note here.

- In the first line of the above, I have defined `T_Celsius` to be a null variable.
- I have used the index `year` rather than `i` to make it easier to remember what I am looping over.
- The loop goes from 1 to the length of `nhtemp` (`length(nhtemp)` = 60). I could have instead just written `1:60`, but the above has the advantage that if the length of `nhtemp` changes for some reason, the loop will still work. As a exercise, try running the above code for `1:40` or `1:80` to see what happens when the number of years to loop over does not match the number of years in `nhtemp`.

Now say that we actually want to know the *change* in temperature from one year to the next, and to make a new vector `Temp_ch` that stores the difference in degrees Celsius from `year` to `year - 1`. While there are ways to make such a vector in R without a loop, using a for loop is probably most intuitive way to do it.


```r
T_Celsius <- NULL;
Temp_ch   <- NULL;
for(year in 1:length(nhtemp)){
  T_Celsius[year] <- (5/9) * (nhtemp[year] - 32);
  Temp_ch[year]   <- T_Celsius[year] - T_Celsius[year - 1];
}
print(Temp_ch);
```

```
##  [1]          NA  1.33333333 -1.61111111  0.94444444 -0.94444444 -0.83333333
##  [7]  1.05555556  0.61111111 -0.88888889  1.44444444 -0.61111111 -0.66666667
## [13] -0.16666667  0.72222222 -1.22222222  1.27777778  0.11111111 -0.16666667
## [19]  0.50000000  0.72222222 -0.55555556 -0.38888889 -0.72222222  0.22222222
## [25]  0.11111111  0.66666667  0.11111111 -0.50000000 -1.16666667  1.61111111
## [31] -0.38888889 -0.22222222  0.61111111 -0.11111111  0.33333333 -0.44444444
## [37] -0.16666667  1.66666667 -1.44444444  0.72222222  0.22222222  0.83333333
## [43] -1.44444444  0.00000000 -0.61111111  0.94444444 -1.33333333  1.33333333
## [49] -0.55555556  0.16666667 -0.77777778  0.22222222  0.44444444 -0.16666667
## [55]  0.16666667 -0.50000000  0.61111111 -0.05555556  0.05555556  0.61111111
```

In the new line of code added within the above loop, the temperature in degrees Celsius from the previous year `T_Celsius[year - 1]` is subtracted from the temperature from the current year `T_Celsius[year]`. The value of this difference is then stored in `Temp_ch[year]`, so at the end of the loop, each element of `Temp_ch` stores the difference between the current year's temperature and the last year's temperature.

Note that this newly added line within the for loop is a bit dangerous because `T_Celsius[year - 1]` does not exist when `year = 1` (i.e., at the start of the loop). Since there is no value at `T_Celsius[1 - 1]`, R returns an `NA`, so the first value of `Temp_ch = NA`. This is what we want, but if we are not careful, trusting R to fill things in appropriately might cause us problems later. It is usually better to err on the side of caution and think carefully about what each line is doing, using comments to help the readability. The example below makes everything a bit cleaner and clearer.


```r
total_years <- length(nhtemp); # Total years in the data set
# Make vectors with an NA element for each year
T_Celsius   <- rep(x = NA, times = total_years);
Temp_ch     <- rep(x = NA, times = total_years);
for(year in 1:total_years){ # For each year in the data set
  # First calculate the temperature in degrees Celsius
  T_Celsius[year] <- (5/9) * (nhtemp[year] - 32);
  if(year > 1){ # Condition in which difference exists
      Temp_ch[year] <- T_Celsius[year] - T_Celsius[year - 1];
  } # Now T_Celsius[0] will not be attempted
}
print(Temp_ch);
```

```
##  [1]          NA  1.33333333 -1.61111111  0.94444444 -0.94444444 -0.83333333
##  [7]  1.05555556  0.61111111 -0.88888889  1.44444444 -0.61111111 -0.66666667
## [13] -0.16666667  0.72222222 -1.22222222  1.27777778  0.11111111 -0.16666667
## [19]  0.50000000  0.72222222 -0.55555556 -0.38888889 -0.72222222  0.22222222
## [25]  0.11111111  0.66666667  0.11111111 -0.50000000 -1.16666667  1.61111111
## [31] -0.38888889 -0.22222222  0.61111111 -0.11111111  0.33333333 -0.44444444
## [37] -0.16666667  1.66666667 -1.44444444  0.72222222  0.22222222  0.83333333
## [43] -1.44444444  0.00000000 -0.61111111  0.94444444 -1.33333333  1.33333333
## [49] -0.55555556  0.16666667 -0.77777778  0.22222222  0.44444444 -0.16666667
## [55]  0.16666667 -0.50000000  0.61111111 -0.05555556  0.05555556  0.61111111
```

The use of the `if` above is technically unnecessary, but it serves as a nice reminder that it only makes sense to take the difference between temperatures starting in year 2. Now with `T_Celsius` and `Temp_ch` calculated, we can make a nice table of years and temperature values and changes.


```r
years <- 1912:1971;
dat   <- cbind(years, nhtemp, T_Celsius, Temp_ch);
```


 years   nhtemp   T_Celsius       Temp_ch
------  -------  ----------  ------------
  1912     49.9    9.944444            NA
  1913     52.3   11.277778    1.33333333
  1914     49.4    9.666667   -1.61111111
  1915     51.1   10.611111    0.94444444
  1916     49.4    9.666667   -0.94444444
  1917     47.9    8.833333   -0.83333333
  1918     49.8    9.888889    1.05555556
  1919     50.9   10.500000    0.61111111
  1920     49.3    9.611111   -0.88888889
  1921     51.9   11.055556    1.44444444
  1922     50.8   10.444444   -0.61111111
  1923     49.6    9.777778   -0.66666667
  1924     49.3    9.611111   -0.16666667
  1925     50.6   10.333333    0.72222222
  1926     48.4    9.111111   -1.22222222
  1927     50.7   10.388889    1.27777778
  1928     50.9   10.500000    0.11111111
  1929     50.6   10.333333   -0.16666667
  1930     51.5   10.833333    0.50000000
  1931     52.8   11.555556    0.72222222
  1932     51.8   11.000000   -0.55555556
  1933     51.1   10.611111   -0.38888889
  1934     49.8    9.888889   -0.72222222
  1935     50.2   10.111111    0.22222222
  1936     50.4   10.222222    0.11111111
  1937     51.6   10.888889    0.66666667
  1938     51.8   11.000000    0.11111111
  1939     50.9   10.500000   -0.50000000
  1940     48.8    9.333333   -1.16666667
  1941     51.7   10.944444    1.61111111
  1942     51.0   10.555556   -0.38888889
  1943     50.6   10.333333   -0.22222222
  1944     51.7   10.944444    0.61111111
  1945     51.5   10.833333   -0.11111111
  1946     52.1   11.166667    0.33333333
  1947     51.3   10.722222   -0.44444444
  1948     51.0   10.555556   -0.16666667
  1949     54.0   12.222222    1.66666667
  1950     51.4   10.777778   -1.44444444
  1951     52.7   11.500000    0.72222222
  1952     53.1   11.722222    0.22222222
  1953     54.6   12.555556    0.83333333
  1954     52.0   11.111111   -1.44444444
  1955     52.0   11.111111    0.00000000
  1956     50.9   10.500000   -0.61111111
  1957     52.6   11.444444    0.94444444
  1958     50.2   10.111111   -1.33333333
  1959     52.6   11.444444    1.33333333
  1960     51.6   10.888889   -0.55555556
  1961     51.9   11.055556    0.16666667
  1962     50.5   10.277778   -0.77777778
  1963     50.9   10.500000    0.22222222
  1964     51.7   10.944444    0.44444444
  1965     51.4   10.777778   -0.16666667
  1966     51.7   10.944444    0.16666667
  1967     50.8   10.444444   -0.50000000
  1968     51.9   11.055556    0.61111111
  1969     51.8   11.000000   -0.05555556
  1970     51.9   11.055556    0.05555556
  1971     53.0   11.666667    0.61111111

In the next section, I will move on to consider a more complicated example using nested for loops (i.e., a for loop inside of another for loop).

<a name="for_more">The for loop in R: nested loops</a>
================================================================================

Loops can be nested inside one another, such that the inner loop is run one time for each iteration of the outer loop. A common example of when nested loops are useful is in working with two dimensional arrays (e.g., tables or matrices). I will share a quick example from community ecology theory, in which species interactions within a community are often represented by square matrices like the one below,

$$M = 
\begin{bmatrix}
    -1       & -0.2 \\
    -0.3     & -1 
\end{bmatrix}.$$

Community ecology theory is not the focus here, so it is fine to [skip a couple paragraphs](#skip) to just move along to the coding problem. For more context though, each element in the above matrix defines how a slight increase in the density of one species affects the density of another species when species densities are at some equilibrium state. Each row and column in $M$ represents a single species, so there are two species in the above matrix. Where rows and column numbers are identical, we have the diagonal of the matrix; this defines how a species affects its own density (i.e., self-regulation). The off-diagonals define how a slight increase in one species' density affects a different species; in the above example, both species decrease each others densities because each has a negative affect on the other (the species in row 1 is negatively affected by species 2 by a magnitude of $M_{1,2} = -0.2$, and the species in row 2 is negatively affected by species 1 by a magnitude of $M_{2,1} =-0.3$). If one of these two off-diagonal elements were positive and the other were negative (e.g., $M_{1,2} = 0.2$, $M_{2,1} = -0.3$), we could interpret this as a predator-prey interaction. If both off-diagonal elements were positive (e.g., $M_{1,2} = 0.2$, $M_{2,1} = 0.3$), we could interpret this as a mutualistic interaction.

To investigate community stability, theoreticians use random matrix theory to test how likely it is that communities with specific properties will return to equilibrium species densities when perturbed [e.g., @Allesina2015a; @Allesina2012]. Developing this theory sometimes requires generating many large $M$ matrices with random interaction strengths (off-diagonal elements) but uniform interaction types (competitor, predator-prey, or mutualist) and self-regulation (diagonal elements). If we take the case of large $M$ matrices in which all interactions are predator-prey (e.g., a big food web), all pairs of row-column elements need to have opposite signs. In other words, if $M_{i,j}$ is positive, then $M_{j,i}$ needs to be negative. To generate a random matrix with this property, we need go through the elements of $M$ and change the signs of values where appropriate.

<a name = "skip">The **coding** issue</a> is therefore to build a large matrix in which the sign of $M_{i,j}$ is the opposite of $M_{j,i}$. We also want the absolute values of the off-diagonal elements to be random numbers, and the diagonal elements to be -1. These latter two properties can be made with the following lines of code, which will make a $10 \times 10$ matrix as printed off below:


```r
M_vals <- rnorm(n = 100, mean = 0, sd = 1);
M_vals <- round(M_vals, digits = 2);
M_mat  <- matrix(data = M_vals, nrow = 10);
diag(M_mat) <- -1; # Adds -1 values to diagonal
print(M_mat);
```

```
##        [,1]  [,2]  [,3]  [,4]  [,5]  [,6]  [,7]  [,8]  [,9] [,10]
##  [1,] -1.00  1.60 -1.35 -0.89  1.97 -0.73  2.61  1.59 -0.22 -0.54
##  [2,]  0.51 -1.00  1.24 -0.23 -0.64 -0.25  2.03 -1.17  1.64 -0.47
##  [3,]  0.83 -0.42 -1.00  0.80  0.35  0.26 -0.52  0.17  0.29 -0.39
##  [4,] -1.05  0.38  0.05 -1.00  0.45  0.25  0.53 -1.27 -0.64  1.41
##  [5,]  0.05  0.04 -1.15 -0.98 -1.00 -1.49 -1.88 -0.84  0.46  0.83
##  [6,]  0.19  1.23  1.48 -0.84  0.78 -1.00 -0.46 -1.10  1.09  1.02
##  [7,]  1.84  0.51 -1.62  1.37 -0.94 -1.91 -1.00  0.00  0.61 -0.19
##  [8,] -1.34 -0.25  0.47 -1.07 -1.54 -0.42 -1.22 -1.00  0.09 -0.02
##  [9,]  1.42 -0.92  2.53  0.92  1.34  1.17  0.17 -0.40 -1.00  1.55
## [10,] -0.60  0.72  1.17 -1.52 -1.50  0.50 -0.52 -0.96  0.29 -1.00
```

The above random matrix has diagonal elements all equal to $-1$, and off-diagonal elements independently drawn from a standard normal distribution $\mathcal{N}(0, 1)$. **The task is now to to make sure that pairs of off-diagonal elements $M_{i, j}$ and $M_{j, i}$ have opposite signs**. In other words, if `M_mat[1, 3]` is positive, then `M_mat[3, 1]` should be negative (recall that R indices in brackets refer first to the row, then the column of a matrix: `M_mat[row, column]`). Unlike the previous problems in these notes, it is difficult to see how to create such a matrix without using loops (or editing the values by hand). We need to iterate over `M_mat` `for` each row and `for` each column, reversing the signs of off-diagonal elements whenever necessary. To do this, we can use a `for` loop within another `for` loop -- the outer loop iterates over rows, and the inner loop iterates over columns. Whenever a pair of elements `M_mat[i, j]` and `M_mat[j, i]` are found to have the same sign, `M_mat[i, j]` is multiplied by -1.


```r
N_species <- dim(M_mat)[1]; # Get total row & col number
for(i in 1:N_species){ # For each row in the matrix
    for(j in 1:N_species){ # For each column in the row
        if(i < j){ # Only need to look at upper triangle
            elem_sign <- M_mat[i, j] * M_mat[j, i];
            if(elem_sign > 0){
                M_mat[i, j] <- -1 * M_mat[i, j];
            }
        }
    } # Finish all columns in the row
} # Finish all rows
print(M_mat);
```

```
##        [,1]  [,2]  [,3]  [,4]  [,5]  [,6]  [,7]  [,8]  [,9] [,10]
##  [1,] -1.00 -1.60 -1.35  0.89 -1.97 -0.73 -2.61  1.59 -0.22  0.54
##  [2,]  0.51 -1.00  1.24 -0.23 -0.64 -0.25 -2.03  1.17  1.64 -0.47
##  [3,]  0.83 -0.42 -1.00 -0.80  0.35 -0.26  0.52 -0.17 -0.29 -0.39
##  [4,] -1.05  0.38  0.05 -1.00  0.45  0.25 -0.53  1.27 -0.64  1.41
##  [5,]  0.05  0.04 -1.15 -0.98 -1.00 -1.49  1.88  0.84 -0.46  0.83
##  [6,]  0.19  1.23  1.48 -0.84  0.78 -1.00  0.46  1.10 -1.09 -1.02
##  [7,]  1.84  0.51 -1.62  1.37 -0.94 -1.91 -1.00  0.00 -0.61  0.19
##  [8,] -1.34 -0.25  0.47 -1.07 -1.54 -0.42 -1.22 -1.00  0.09  0.02
##  [9,]  1.42 -0.92  2.53  0.92  1.34  1.17  0.17 -0.40 -1.00 -1.55
## [10,] -0.60  0.72  1.17 -1.52 -1.50  0.50 -0.52 -0.96  0.29 -1.00
```

Note that in the matrix `M_mat` modified above, all pairs of off-diagonal elements `M_mat[i, j]` and `M_mat[j, i]` have opposite signs. Why did that work? We can start with the loops, the outer of which (`for(i in 1:N_species)`) started going through rows starting with row `i = 1`. While `i = 1`, the inner loop (`for(j in 1:N_species)`) went through all columns from 1 to 10 in row 1. Each unique combination of row `i` and column `j` identified a unique matrix element `M_mat[i, j]`, and the code then checked to see if any action needed to be taken in two ways. First, the code checked to see `if(i < j)` -- if not, then the whole bracketed `if` statement is skipped and we move on to the next column `j`. This `if` statement prevents the code from unnecessarily checking the same `i` and `j` pair twice, and prevents it from changing the diagonal where `i == j`. Second, the code assigning `elem_sign` checks to see if `M_mat[i, j]` and `M_mat[j, i]` have opposing signs by multiplying the two values together (two positives or two negatives multiplied together will equal a positive value for `elem_sign`; one positive and one negative will equal a negative value). If `elem_sign > 0`, then we know that `M_mat[i, j]` and `M_mat[j, i]` are either both positive or both negative, so we fix this by changing the sign of `M_mat[i, j]` (multiplying by -1). The figure below gives a visual representation of what is happening.

![](images/nested_loops.png)

In the figure above, we start with the case in which `i = 1` (i.e., the first row), and move through each value of `j` from `j = 1` to `j = 10`. If `M_mat[i, j]` is in the upper right triangle of the matrix (i.e., `i < j`; shown in red), then the code checks to see if both `M_mat[i, j]` and `M_mat[j, i]` have the same sign. The loop ends when it has moved through all values of `i` from 1 to 10, hence looking at each element `M_mat[i, j]` in the matrix. 

Once the logic of the nested loop makes sense, the rest comes down to remembering the syntax for for coding loops in R correctly. This comes with practice, so I have included some practice problems using loops below. Next, I will have a (briefer) look at the `while` loop in R. The general idea of iterating the same task many times will be the same, but the conditions under which the task is iterated will change slightly.

<a name="while_loop">The while loop in R</a>
================================================================================

The general idea of a `while loop` is the same as that of a `for loop`. In both cases, we are repeating the same task multiple times. But whereas we could specify the full range of values `in` which to substitute some value (e.g., `i`) within a `for` loop, in a `while` loop, we only specify the conditions under which to continue iterating. The printing of numbers from 1 to 10, as done with the `for` loop above, can also be done with the `while` loop below. 


```r
i <- 1;
while(i <= 10){
    print(i);
    i <- i + 1;
}
```

```
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
```

There are few important things to note. 

1. We need to specify an initial value of `i = 1` (else `print(i)` will not return anything).
2. The loop will continue as long as `i` is less than or equal to 10 (`while(i <= 10)`).
3. It is critical to increment `i` within the loop (i.e., add a value of 1 at the end so `i <- i + 1`).

If we had forgotten number 3, then the value of `i` would always be 1. Aside from only printing the number 1 many times (rather than 1-10), notice that the loop would never actually terminate because `i` would *always* stay less than or equal to 10. This situation is called an '[infinite loop](https://en.wikipedia.org/wiki/Infinite_loop)', and will result in a situation where it is necessary to terminate the loop manually (i.e., tell R to stop it, either using the red stop sign in the Rstudio console, or by holding down 'CTRL + C'). This is almost always to be avoided, but to see what happens, remove the line `i <- i + 1;` and run the rest of code above.

Sometimes the use of `for` versus `while` loops is a matter of personal preference, such as with the simple example of printing a set of numbers from 1 to 10. In some cases, however, use of a `while` loop will make coding easier. 

Consider a situation in which data need to be randomly sampled from a subset of 100 out of 1000 total different entities (the details do not matter -- these entities could be different lochs, fields, or trees in a park). If we just need to sample 100 values out of 1000 without replacement, we can do this with a single line of R code:


```r
subset <- sample(x = 1:1000, size = 100, replace = FALSE);
print(subset);
```

```
##   [1] 670 864 223 163 581 711 779 371 820  20 627 311 248 462 964 628  81 570
##  [19] 474 962 292 563 315 507 771 624 668 767 606 693 351 270 388 640 519 988
##  [37] 285 804  95 194 124 608 807 544 469 633 853 845 114 613 666 580 924 218
##  [55] 908 802 654 240 869 731 142 756 389 526 912 184 635 294 969 739 803 967
##  [73]  53 657 432 476 286 322 249 992 629 671 174 704 665 105 795 417 444 267
##  [91] 195 545 133 997 598 170 566 530 830 549
```

This is easy enough, but what if, having already chosen these 100 entities, we decide that we need *another* 100, for a total of 200 unique samples (without replacement). We could find a creative way of using `sample` again in R (give this a try), but there is a logical way to do this with a `while` loop. The idea is to sample a single value from `1:1000`, then check to see if that value is already in the `subset`. If it is in the `subset`, then throw it out and keep going. If it is not in the `subset`, add it. Continue until the size of `subset` is 200.


```r
while(length(subset) <= 200){
    samp <- sample(x = 1:1000, size = 1);
    if(samp %in% subset == FALSE){
        subset <- c(subset, samp);
    }
}
print(subset);
```

```
##   [1] 670 864 223 163 581 711 779 371 820  20 627 311 248 462 964 628  81 570
##  [19] 474 962 292 563 315 507 771 624 668 767 606 693 351 270 388 640 519 988
##  [37] 285 804  95 194 124 608 807 544 469 633 853 845 114 613 666 580 924 218
##  [55] 908 802 654 240 869 731 142 756 389 526 912 184 635 294 969 739 803 967
##  [73]  53 657 432 476 286 322 249 992 629 671 174 704 665 105 795 417 444 267
##  [91] 195 545 133 997 598 170 566 530 830 549 890 265 158 506 895 881  84 479
## [109] 338 884 856 538 559 927 788  40 958 359 784 457 159 188 986 760 100 247
## [127] 121 710 709 919 262 998 244 384 939 225 297 971 568 763 450  85  44 412
## [145] 966 748 593 433 182  37 749 187 891 600 765 928  12  43 741 754 434 650
## [163] 644 523 907 106 126 935 872 728 564 426 258 298  93 422 424 427 365 386
## [181] 269 342 208 870 522 193 797 783 700  26 961   5  28 275 752 423 460 356
## [199] 401 421 217
```

The `while` loop above will continue as long as `subset` contains less than 200 numbers. If a randomly selected number from 1 to 1000 is **not** in the `subset`, then it is immediately added to make a bigger `subset` with the new number appended to it. The end result is that the above code has added 100 new unique values to the previous sample of 100.


<a name="practice">Practice problems</a>
================================================================================

Below are some practice problems for working with loops. **To see the answers**, click on the '**Details**' arrows to the left at the bottom of each question. Note that your answers might differ from mine -- there is more than one way to solve each problem!

1. Using a `for` or `while` loop, print all of the numbers from 1 to 1000 that are multiples of 17. (*Hint: The mod operator `%%` returns the remainder after division. For example, `14 %% 4` would return a value of 2 because 14/4 = 3 with a remainder of 2.*)


<details>


```r
for(i in 1:1000){
    if(i %% 17 == 0){
        print(i);
    }
}
```

```
## [1] 17
## [1] 34
## [1] 51
## [1] 68
## [1] 85
## [1] 102
## [1] 119
## [1] 136
## [1] 153
## [1] 170
## [1] 187
## [1] 204
## [1] 221
## [1] 238
## [1] 255
## [1] 272
## [1] 289
## [1] 306
## [1] 323
## [1] 340
## [1] 357
## [1] 374
## [1] 391
## [1] 408
## [1] 425
## [1] 442
## [1] 459
## [1] 476
## [1] 493
## [1] 510
## [1] 527
## [1] 544
## [1] 561
## [1] 578
## [1] 595
## [1] 612
## [1] 629
## [1] 646
## [1] 663
## [1] 680
## [1] 697
## [1] 714
## [1] 731
## [1] 748
## [1] 765
## [1] 782
## [1] 799
## [1] 816
## [1] 833
## [1] 850
## [1] 867
## [1] 884
## [1] 901
## [1] 918
## [1] 935
## [1] 952
## [1] 969
## [1] 986
```

</details><br><br>


2. In the `nhtemp`, write a loop to add up the temperatures *for all of the even numbered years*, then divide by the total number of even numbered years to get the average.

<details>


```r
Y <- 1912:1971; # Years
N <- length(nhtemp); # Total temps
A <- 0; # Added temp
C <- 0; # Count
for(i in 1:N){
    if(Y[i] %% 2 == 0){
        A <- A + nhtemp[i];
        C <- C + 1;
    }
}
avg_A <- A/C;
print(avg_A);
```

```
## [1] 50.8
```

</details><br><br>


3. Using a `while` loop, calculate the sum of the series, $Y = \frac{4}{1} - \frac{4}{3} + \frac{4}{5} - \frac{4}{7} + \frac{4}{9} - \frac{4}{11} + \dots$ to at least 10000 terms. What does the value $Y$ appear to approach as more terms are added? (*Hint: Use `if(){}`, or an `if(){}else{}` to switch from `+` to `-`*)


<details>


```r
val  <- 0;
deno <- 1;
iter <- 1;
sign <- 1;
while(iter < 1000000){
    if(sign < 0){
        val  <- val - (4/deno);
    }
    if(sign > 0){
        val <- val + (4/deno);
    }
    sign <- -1 * sign;
    deno <- deno + 2;
    iter <- iter + 1;
}
print(val);
```

```
## [1] 3.141594
```

</details><br><br>

4. From [here](https://www.r-exercises.com/2018/03/30/loops-in-r-exercises/), write a while loop that prints out standard random normal numbers (use rnorm()) but stops (breaks) if you get a number bigger than 1.

<details>


```r
i <- 0;
while(i <= 1){
    i <- rnorm(n = 1);
    print(i);
}
```

```
## [1] -0.5793133
## [1] 0.6331474
## [1] 0.4885816
## [1] 0.7415634
## [1] -0.7024318
## [1] 0.6175136
## [1] 2.244515
```

</details><br><br>


5. Create an $8 \times 8$ matrix `mat` with diagonal values of 1 and off-diagonal values randomly selected from a standard normal distribution $\mathcal{N}(0, 1)$ (using `rnorm`). Using nested `for` loops as in the [above notes](#for_more), swap elements `mat[i, j]` with `mat[j, i]` **only** if `mat[i, j] < mat[j, i]` (so that the higher number is in the lower triangle).

<details>


```r
mat_v     <- rnorm(n = 64, mean = 0, sd = 1);
mat_v     <- round(mat_v, digits = 2);
mat       <- matrix(data = mat_v, nrow = 8);
diag(mat) <- 1;
N <- dim(mat)[1]; 
for(i in 1:N){ 
    for(j in 1:N){
        if(mat[i, j] < mat[j, i]){
            temp_val  <- mat[i, j];
            mat[i, j] <- mat[j, i];
            mat[j, i] <- temp_val;
        }
    } 
} 
print(mat);
```

```
##       [,1]  [,2]  [,3]  [,4]  [,5]  [,6]  [,7]  [,8]
## [1,]  1.00 -1.00 -2.02 -0.84 -0.24  1.07  1.01 -0.46
## [2,]  0.53  1.00 -2.48 -2.57 -0.77 -0.75 -0.02  0.23
## [3,] -0.67 -0.25  1.00 -0.51  0.31  0.74 -0.86  0.68
## [4,]  0.32  1.12  0.28  1.00 -2.29  0.03 -1.86  0.41
## [5,]  0.05  1.22  1.26 -0.11  1.00  0.23 -1.66  1.03
## [6,]  1.61  0.71  0.75  0.26  1.03  1.00 -0.08 -1.36
## [7,]  1.86  0.81  0.56  0.16 -0.49  0.85  1.00 -0.19
## [8,]  0.05  1.61  2.56  0.44  1.21  2.19 -0.10  1.00
```

</details><br><br>

<a name="whatelse">Additional resources</a>
================================================================================

- The [Essence of Loops](https://www.i-programmer.info/programming/theory/8003-the-essence-of-loops.html)


References
================================================================================

