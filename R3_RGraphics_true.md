Graphical plot in R
========================================================
author: Tue Vu - CyberInfrastructure & Integration Technology 
date:   12/03/2018


Course Content:
========================================================
- Making exploratory graphs
- Principles of analytic graphics
- Plotting systems and graphics devices in R
- The base, lattice, and ggplot2 plotting systems in R
- Clustering methods
- Dimension reduction techniques

Exploratory graph
========================================================
### Why do we use graphs in data analysis? 
- To understand data properties
- To find patterns in data
- To suggest modeling strategies
- To "debug" analyses
- To communicate results

### Characteristics of exploratory graphs 
- They are made quickly
- A large number are made
- The goal is for personal understanding
- Axes/legends are generally cleaned up (later)
- Color/size are primarily used for information

Plotting System
================================
## There are 3 main plotting systems in R
### The **Base** plotting system
    - Start with blank plot and build up the plot
    - Plot is just a series of R command
    - Flexible
## The **Lattice** plotting system (using package::lattice)
    - Plots created using single function call
    - Good for putting many plots to screen
    - Cannot add to plots once created
## The **ggplot** plotting system (using package::ggplot2)
    - Similar to Lattice but easier
    - Many default mode
    - Flexible between Base and Lattice
    
Base plotting system
========================================================
## Important **BASE** graphic parameters
- pch: the plotting symbol (default is open circle)
- lty: the line type (default is solid line), can be dashed, dotted, etc.
- lwd: the line width, specified as an integer multiple
- col: the plotting color, specified as a number, string, or hex code; the colors() function gives you a vector of colors by name
- xlab: character string for the x-axis label
- ylab: character string for the y-axis label

========================================================
## Important **BASE** plotting function
- plot: make a scatterplot, or other type of plot depending on the class of the object being plotted
- lines: add lines to a plot, given a vector x values and a corresponding vector of y values (or a 2-column matrix); this function just connects the dots
- points: add points to a plot
- text: add text labels to a plot using specified x, y coordinates
- title: add annotations to x, y axis labels, title, subtitle, outer margin
- mtext: add arbitrary text to the margins (inner or outer) of the plot
- axis: adding axis ticks/labels


========================================================
## Motor Trend Car Road Tests example

The data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973--74 models).
Usage

```r
data(mtcars)
dim(mtcars)
```

```
[1] 32 11
```

```r
names(mtcars)
```

```
 [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
[11] "carb"
```

```r
head(mtcars)
```

```
                   mpg cyl disp  hp drat    wt  qsec vs am gear carb
Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```

```r
print(mtcars)
```

```
                     mpg cyl  disp  hp drat    wt  qsec vs am gear carb
Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2
```

========================================================
### Simple Summaries of Data Simple Summaries of Data
- Five-number summary

```r
summary(mtcars)
```

```
      mpg             cyl             disp             hp       
 Min.   :10.40   Min.   :4.000   Min.   : 71.1   Min.   : 52.0  
 1st Qu.:15.43   1st Qu.:4.000   1st Qu.:120.8   1st Qu.: 96.5  
 Median :19.20   Median :6.000   Median :196.3   Median :123.0  
 Mean   :20.09   Mean   :6.188   Mean   :230.7   Mean   :146.7  
 3rd Qu.:22.80   3rd Qu.:8.000   3rd Qu.:326.0   3rd Qu.:180.0  
 Max.   :33.90   Max.   :8.000   Max.   :472.0   Max.   :335.0  
      drat             wt             qsec             vs        
 Min.   :2.760   Min.   :1.513   Min.   :14.50   Min.   :0.0000  
 1st Qu.:3.080   1st Qu.:2.581   1st Qu.:16.89   1st Qu.:0.0000  
 Median :3.695   Median :3.325   Median :17.71   Median :0.0000  
 Mean   :3.597   Mean   :3.217   Mean   :17.85   Mean   :0.4375  
 3rd Qu.:3.920   3rd Qu.:3.610   3rd Qu.:18.90   3rd Qu.:1.0000  
 Max.   :4.930   Max.   :5.424   Max.   :22.90   Max.   :1.0000  
       am              gear            carb      
 Min.   :0.0000   Min.   :3.000   Min.   :1.000  
 1st Qu.:0.0000   1st Qu.:3.000   1st Qu.:2.000  
 Median :0.0000   Median :4.000   Median :2.000  
 Mean   :0.4062   Mean   :3.688   Mean   :2.812  
 3rd Qu.:1.0000   3rd Qu.:4.000   3rd Qu.:4.000  
 Max.   :1.0000   Max.   :5.000   Max.   :8.000  
```
- Boxplots

```r
boxplot(mtcars$mpg,col="blue",main="Boxplot for mpg")
```

![plot of chunk unnamed-chunk-3](R3_RGraphics_true-figure/unnamed-chunk-3-1.png)

```r
factor(mtcars$cyl)
```

```
 [1] 6 6 4 6 8 6 8 4 4 6 6 8 8 8 8 8 8 4 4 4 4 8 8 8 8 4 4 4 8 6 8 4
Levels: 4 6 8
```

```r
boxplot(mpg~cyl,data=mtcars,
        col=terrain.colors(3),main="MPG by car cylinders",
        xlab = "cylinders",ylab="mpg")
legend("topright",c("4","6","8"),fill = terrain.colors(3))
```

![plot of chunk unnamed-chunk-4](R3_RGraphics_true-figure/unnamed-chunk-4-1.png)

========================================================
- Histograms

```r
hist(mtcars$hp, col="magenta")
```

![plot of chunk unnamed-chunk-5](R3_RGraphics_true-figure/unnamed-chunk-5-1.png)
- Barplot

```r
barplot(mtcars$mpg,col="green",
        main="MPG for 32 cars")
```

![plot of chunk unnamed-chunk-6](R3_RGraphics_true-figure/unnamed-chunk-6-1.png)

========================================================
### Multiple historgrams

```r
par(mfrow=c(1,2))
hist(mtcars$mpg,col="blue")
hist(mtcars$wt,col="blue")
```

![plot of chunk unnamed-chunk-7](R3_RGraphics_true-figure/unnamed-chunk-7-1.png)
### Scatter plot

```r
plot(mtcars$mpg,mtcars$wt,main="Car Fuel vs Weight",
     xlab="Milage per Gallon",ylab="Weight",
     col = mtcars$cyl,pch=16,cex=3)
legend("topright",legend=c(8,6,4),pch=16,cex=3,
       col=c("grey","magenta","blue"))
```

![plot of chunk unnamed-chunk-8](R3_RGraphics_true-figure/unnamed-chunk-8-1.png)

```r
dev.copy(png,"test.png") #Copy plot to png file
```

```
png 
  3 
```

```r
dev.off() #Close PNG device
```

```
png 
  2 
```

Graphics Devices
============================
A graphics device is something where you can make a plot appear
When you make a plot in R, it has to be "sent" to a specific graphics device. 

- A window on your computer (screen device): quick visualization
- A PDF, PNG, JPEG file (file device) #recommended for documents, paper, presentation

The most common place for a plot to be "sent" is the screen device

- On a Mac the screen device is launched with the quartz()
- On Windows the screen device is launched with windows()
- On Unix/Linux the screen device is launched with x11()

- save graphic to PDF
- save graphic to PNG, JPEG

```
dev.copy(png,"filename.png")
```

Plotting with ggplot
========================================================
## What is ggplot
- Grammar of Graphics by Leland Wilkinson
- Written by Hadley Wickham - a grad student at Iowa State
- Third graphic system in for **R** (along with **Base** and **Lattice**)


```r
#install.packages(ggplot2)
library(ggplot2)
```

========================================================
## Basic component of ggplot
- A	**data	frame**	
- **aesthetic mappings**:	how	data	are	mapped	to	color,	size		
- **geoms**:	geometric	objects	like	points,	lines,	shapes.		
- **facets**:	for	conditional	plots.		
- **stats**:	statistical	transformations	like	binning,	quanti les,	
smoothing.		
- **scales**:	what	scale	an	aesthetic	map	uses		
- **coordinate	system**

========================================================
## Type of ggplot:
- Basic **qplot**
    - Same as plot in Base plot
    - Syntax in between Base plot and Lattice
    - Nice graphics
    - Difficult for customize
- Advanced **ggplot**
    - Flexible with many built-in function

========================================================
## Basic qplot: Scatter plot
- Plots are made of **aesthetic** (size, shape, color) and **geom** (points, lines)
- Look for data in frame (or from parent directory)










































```
Error in FUN(X[[i]], ...) : object 'color' not found
```
