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
qplot(x,y,color) #aesthetic
qplot(x,y,color,data) #aesthetic+data
qplot(x,y,color,data,geom="point") #aesthetic+data+geometry
```
- Base plot

```r
data(iris)
qplot(Sepal.Length, Sepal.Width, data=iris)
```

![plot of chunk unnamed-chunk-10](R3_RGraphics_true-figure/unnamed-chunk-10-1.png)

===================
- Add aesthetic (size, shape, color)

```r
qplot(Sepal.Length, Petal.Length, data=iris,
      color=factor(Species),size=factor(Species),
      shape=factor(Species)) #aesthetic
```

![plot of chunk unnamed-chunk-11](R3_RGraphics_true-figure/unnamed-chunk-11-1.png)
- Add geom (points, lines)

```r
qplot(Sepal.Length, Petal.Length, data=iris,
      geom=c("point","smooth")) #geometry
```

![plot of chunk unnamed-chunk-12](R3_RGraphics_true-figure/unnamed-chunk-12-1.png)
- Linear fitting

```r
qplot(Sepal.Length, Petal.Length, data=iris, color=Species,
      geom=c("point","smooth"),method="lm")
```

![plot of chunk unnamed-chunk-13](R3_RGraphics_true-figure/unnamed-chunk-13-1.png)

========================================================
## Basic qplot: Histogram

```r
qplot(Sepal.Length,fill=Species, data=iris)
```

![plot of chunk unnamed-chunk-14](R3_RGraphics_true-figure/unnamed-chunk-14-1.png)

```r
qplot(Sepal.Length,data=iris,geom="density")
```

![plot of chunk unnamed-chunk-15](R3_RGraphics_true-figure/unnamed-chunk-15-1.png)

```r
qplot(Sepal.Length,data=iris,geom="density",
      color=Species)
```

![plot of chunk unnamed-chunk-16](R3_RGraphics_true-figure/unnamed-chunk-16-1.png)
## Basic qplot: Facets

```r
qplot(Sepal.Length,Petal.Length,facets=.~Species, data=iris)
```

![plot of chunk unnamed-chunk-17](R3_RGraphics_true-figure/unnamed-chunk-17-1.png)

========================================================
## Advanced ggplot: 
### Sample plot

```
ggplot(data,aes(x,y)) #data + aesthetic
ggplot(data,aes(x,y)) + geom_point() #data + aesthetic + geometry
```
- Example: in cheat sheet

```r
library(ggplot2)
gp <- ggplot(mpg, aes(hwy, cty))

gp+geom_point(aes(color=cyl))
```

![plot of chunk unnamed-chunk-18](R3_RGraphics_true-figure/unnamed-chunk-18-1.png)

```r
gp+geom_point(aes(color=factor(cyl)))
```

![plot of chunk unnamed-chunk-18](R3_RGraphics_true-figure/unnamed-chunk-18-2.png)

```r
gp+geom_point(aes(color=factor(cyl)))+geom_smooth(method="lm")
```

![plot of chunk unnamed-chunk-18](R3_RGraphics_true-figure/unnamed-chunk-18-3.png)

```r
gp+geom_point(aes(color=factor(cyl)))+geom_smooth(method="lm")+facet_grid(.~cyl)
```

![plot of chunk unnamed-chunk-18](R3_RGraphics_true-figure/unnamed-chunk-18-4.png)

```r
#ggsave("plot.png",width=5,height=5)
```

========================================================
### Annotation
- Labels: xlab(), ylab(), labs(), ggtitle()
- global annotation: use theme()
- Standard appearance: 
    - theme_gray()
    - theme_bw()

```r
gp+geom_point(aes(color=factor(cyl),
              size=factor(cyl)))+
  geom_smooth(method="lm")+
  xlab("Highway miles per gallon")+
  ylab("city miles per gallon")+
  ggtitle("Scatter plot for cty & hwy")+
  xlim(10,40)+ylim(10,40)+
  theme_bw(base_size = 15)
```

![plot of chunk unnamed-chunk-19](R3_RGraphics_true-figure/unnamed-chunk-19-1.png)

========================================================
## Some nice ggplots featuring
### Box plot

```r
ggplot(mpg,aes(x=manufacturer,y=hwy,
               fill=factor(manufacturer)))+
  geom_boxplot()+
  geom_jitter()+
  labs(title="Boxplot for Hwy per manufacturer",x="Manufacturer",y="Highway milage")+
  theme_bw()+coord_flip()+
  theme(legend.position = "none")
```

![plot of chunk unnamed-chunk-20](R3_RGraphics_true-figure/unnamed-chunk-20-1.png)

=============================
### Violin plot

```r
g <- ggplot(mpg, aes(class, cty))
g + geom_violin(aes(fill=class)) + 
  labs(title="Violin plot", 
       subtitle="City Mileage vs Class of vehicle",
       caption="Source: mpg",
       x="Class of Vehicle",
       y="City Mileage")
```

![plot of chunk unnamed-chunk-21](R3_RGraphics_true-figure/unnamed-chunk-21-1.png)

 
========================================================
### Histogram

```r
g <- ggplot(mpg, aes(displ)) + scale_fill_brewer(palette = "Spectral")
g + geom_histogram(aes(fill=class), 
                   bins=10, 
                   col="black", 
                   size=.1) +   # change number of bins
  labs(title="Histogram with Fixed Bins", 
       subtitle="Engine Displacement across Vehicle Classes",
       x="enginer displacement (m)",
       y="Frequency count") 
```

![plot of chunk unnamed-chunk-22](R3_RGraphics_true-figure/unnamed-chunk-22-1.png)

========================================================
### Scatter

```r
data("midwest")
gg <- ggplot(midwest, aes(x=area, y=poptotal)) + 
  geom_point(aes(col=state, size=popdensity)) + 
  geom_smooth(method="loess", se=F) + 
  xlim(c(0, 0.1)) + 
  ylim(c(0, 500000)) + 
  labs(subtitle="Area Vs Population", 
       y="Population", 
       x="Area", 
       title="Scatterplot", 
       caption = "Source: midwest")
plot(gg)
```

![plot of chunk unnamed-chunk-23](R3_RGraphics_true-figure/unnamed-chunk-23-1.png)

========================================================
### Density

```r
g <- ggplot(mpg, aes(cty))
g + geom_density(aes(fill=factor(cyl)), alpha=0.8) + 
    labs(title="Density plot", 
         subtitle="City Mileage Grouped by Number of cylinders",
         caption="Source: mpg",
         x="City Mileage",
         fill="# Cylinders")+
    theme_bw()
```

![plot of chunk unnamed-chunk-24](R3_RGraphics_true-figure/unnamed-chunk-24-1.png)

========================================================
### Density 2d

```r
gg <- ggplot(faithful,aes(x=eruptions,y=waiting))
gg + stat_density_2d(aes(fill=..level..),
                     geom="polygon",color="black")+
     geom_smooth(method="lm",linetype=2,color="red")+
     scale_fill_continuous(low="green",high="red")+
     geom_point() +
     theme_bw()
```

![plot of chunk unnamed-chunk-25](R3_RGraphics_true-figure/unnamed-chunk-25-1.png)


========================================================
### Geographic visualization with ggplot

```r
states <- map_data("state")
ggplot(data = states)+
  geom_polygon(aes(x=long,y=lat,fill=region),
               color="black")+
  coord_fixed(1.3)+
  guides(fill=FALSE)
```

![plot of chunk unnamed-chunk-26](R3_RGraphics_true-figure/unnamed-chunk-26-1.png)

```r
counties <- map_data("county")
SC_counties <- subset(counties,region == "south carolina")
ggplot(data = SC_counties)+
  geom_polygon(aes(x=long,y=lat,fill=subregion),
               color="black")+
  coord_fixed(1.3)+
  guides(fill=FALSE)
```

![plot of chunk unnamed-chunk-27](R3_RGraphics_true-figure/unnamed-chunk-27-1.png)

Plot shapefile
=========================
```
Download shape file data here
https://hub.arcgis.com/datasets/a21fdb46d23e4ef896f31475217cbb08_1
Store it in your folder: c:/CLEMSON/GIS/
Unzip it to Countries_WGS84/
```

```
install.packages("rgdal")
install.packages("colorspace")
```


```r
library(rgdal)
library(colorspace)
library(maps)

setwd('c:/CLEMSON/GIS/Countries_WGS84/')
gfile <- readOGR(dsn="Countries_WGS84.shp")
```

```
OGR data source with driver: ESRI Shapefile 
Source: "c:\CLEMSON\GIS\Countries_WGS84\Countries_WGS84.shp", layer: "Countries_WGS84"
with 251 features
It has 2 fields
Integer64 fields read as strings:  OBJECTID 
```

```r
names(gfile)
```

```
[1] "OBJECTID"   "CNTRY_NAME"
```

```r
gfile$CNTRY_NAME
```

```
  [1] Aruba                                  
  [2] Antigua and Barbuda                    
  [3] Afghanistan                            
  [4] Algeria                                
  [5] Azerbaijan                             
  [6] Albania                                
  [7] Armenia                                
  [8] Andorra                                
  [9] Angola                                 
 [10] American Samoa                         
 [11] Argentina                              
 [12] Australia                              
 [13] Austria                                
 [14] Anguilla                               
 [15] Antarctica                             
 [16] Bahrain                                
 [17] Barbados                               
 [18] Botswana                               
 [19] Bermuda                                
 [20] Belgium                                
 [21] Bahamas, The                           
 [22] Bangladesh                             
 [23] Belize                                 
 [24] Bosnia and Herzegovina                 
 [25] Bolivia                                
 [26] Myanmar (Burma)                        
 [27] Benin                                  
 [28] Byelarus                               
 [29] Solomon Islands                        
 [30] Brazil                                 
 [31] Bhutan                                 
 [32] Bulgaria                               
 [33] Bouvet Island                          
 [34] Brunei                                 
 [35] Burundi                                
 [36] Canada                                 
 [37] Cambodia                               
 [38] Chad                                   
 [39] Sri Lanka                              
 [40] Congo                                  
 [41] Zaire                                  
 [42] China                                  
 [43] Chile                                  
 [44] Cayman Islands                         
 [45] Cocos (Keeling) Islands                
 [46] Cameroon                               
 [47] Comoros                                
 [48] Colombia                               
 [49] Northern Mariana Islands               
 [50] Costa Rica                             
 [51] Central African Republic               
 [52] Cuba                                   
 [53] Cape Verde                             
 [54] Cook Islands                           
 [55] Cyprus                                 
 [56] Denmark                                
 [57] Djibouti                               
 [58] Dominica                               
 [59] Jarvis Island                          
 [60] Dominican Republic                     
 [61] Ecuador                                
 [62] Egypt                                  
 [63] Ireland                                
 [64] Equatorial Guinea                      
 [65] Estonia                                
 [66] Eritrea                                
 [67] El Salvador                            
 [68] Ethiopia                               
 [69] Czech Republic                         
 [70] French Guiana                          
 [71] Finland                                
 [72] Fiji                                   
 [73] Falkland Islands (Islas Malvinas)      
 [74] Federated States of Micronesia         
 [75] Faroe Islands                          
 [76] French Polynesia                       
 [77] Baker Island                           
 [78] France                                 
 [79] French Southern & Antarctic Lands      
 [80] Gambia, The                            
 [81] Gabon                                  
 [82] Georgia                                
 [83] Ghana                                  
 [84] Gibraltar                              
 [85] Grenada                                
 [86] Guernsey                               
 [87] Greenland                              
 [88] Germany                                
 [89] Glorioso Islands                       
 [90] Guadeloupe                             
 [91] Guam                                   
 [92] Greece                                 
 [93] Guatemala                              
 [94] Guinea                                 
 [95] Guyana                                 
 [96] Gaza Strip                             
 [97] Haiti                                  
 [98] Heard Island & McDonald Islands        
 [99] Honduras                               
[100] Howland Island                         
[101] Croatia                                
[102] Hungary                                
[103] Iceland                                
[104] Indonesia                              
[105] Man, Isle of                           
[106] India                                  
[107] British Indian Ocean Territory         
[108] Iran                                   
[109] Israel                                 
[110] Italy                                  
[111] Ivory Coast                            
[112] Iraq                                   
[113] Japan                                  
[114] Jersey                                 
[115] Jamaica                                
[116] Jan Mayen                              
[117] Jordan                                 
[118] Johnston Atoll                         
[119] Juan De Nova Island                    
[120] Kenya                                  
[121] Kyrgyzstan                             
[122] North Korea                            
[123] Kiribati                               
[124] South Korea                            
[125] Christmas Island                       
[126] Kuwait                                 
[127] Kazakhstan                             
[128] Laos                                   
[129] Lebanon                                
[130] Latvia                                 
[131] Lithuania                              
[132] Liberia                                
[133] Slovakia                               
[134] Liechtenstein                          
[135] Lesotho                                
[136] Luxembourg                             
[137] Libya                                  
[138] Madagascar                             
[139] Martinique                             
[140] Macau                                  
[141] Moldova                                
[142] Mayotte                                
[143] Mongolia                               
[144] Montserrat                             
[145] Malawi                                 
[146] Macedonia                              
[147] Mali                                   
[148] Monaco                                 
[149] Morocco                                
[150] Mauritius                              
[151] Midway Islands                         
[152] Mauritania                             
[153] Malta                                  
[154] Oman                                   
[155] Maldives                               
[156] Montenegro                             
[157] Mexico                                 
[158] Malaysia                               
[159] Mozambique                             
[160] New Caledonia                          
[161] Niue                                   
[162] Norfolk Island                         
[163] Niger                                  
[164] Vanuatu                                
[165] Nigeria                                
[166] Netherlands                            
[167] Norway                                 
[168] Nepal                                  
[169] Nauru                                  
[170] Suriname                               
[171] Netherlands Antilles                   
[172] Nicaragua                              
[173] New Zealand                            
[174] Paraguay                               
[175] Pitcairn Islands                       
[176] Peru                                   
[177] Paracel Islands                        
[178] Spratly Islands                        
[179] Pakistan                               
[180] Poland                                 
[181] Panama                                 
[182] Portugal                               
[183] Papua New Guinea                       
[184] Pacific Islands (Palau)                
[185] Guinea-Bissau                          
[186] Qatar                                  
[187] Reunion                                
[188] Marshall Islands                       
[189] Romania                                
[190] Philippines                            
[191] Puerto Rico                            
[192] Russia                                 
[193] Rwanda                                 
[194] Saudi Arabia                           
[195] St. Pierre and Miquelon                
[196] St. Kitts and Nevis                    
[197] Seychelles                             
[198] South Africa                           
[199] Senegal                                
[200] St. Helena                             
[201] Slovenia                               
[202] Sierra Leone                           
[203] San Marino                             
[204] Singapore                              
[205] Somalia                                
[206] Spain                                  
[207] Serbia                                 
[208] St. Lucia                              
[209] Sudan                                  
[210] Svalbard                               
[211] Sweden                                 
[212] South Georgia and the South Sandwich Is
[213] Syria                                  
[214] Switzerland                            
[215] United Arab Emirates                   
[216] Trinidad and Tobago                    
[217] Thailand                               
[218] Tajikistan                             
[219] Turks and Caicos Islands               
[220] Tokelau                                
[221] Tonga                                  
[222] Togo                                   
[223] Sao Tome and Principe                  
[224] Tunisia                                
[225] Turkey                                 
[226] Tuvalu                                 
[227] Taiwan                                 
[228] Turkmenistan                           
[229] Tanzania, United Republic of           
[230] Uganda                                 
[231] United Kingdom                         
[232] Ukraine                                
[233] United States                          
[234] Burkina Faso                           
[235] Uruguay                                
[236] Uzbekistan                             
[237] St. Vincent and the Grenadines         
[238] Venezuela                              
[239] British Virgin Islands                 
[240] Vietnam                                
[241] Virgin Islands                         
[242] Namibia                                
[243] West Bank                              
[244] Wallis and Futuna                      
[245] Western Sahara                         
[246] Wake Island                            
[247] Western Samoa                          
[248] Swaziland                              
[249] Yemen                                  
[250] Zambia                                 
[251] Zimbabwe                               
251 Levels: Afghanistan Albania Algeria American Samoa Andorra ... Zimbabwe
```

```r
plot(gfile)
```

![plot of chunk unnamed-chunk-28](R3_RGraphics_true-figure/unnamed-chunk-28-1.png)

```r
plot(gfile,col=rainbow_hcl(50))
llgridlines(gfile,lty=5)
```

![plot of chunk unnamed-chunk-28](R3_RGraphics_true-figure/unnamed-chunk-28-2.png)

```r
sel <- gfile$CNTRY_NAME=="United Kingdom"
plot(gfile[sel,])
```

![plot of chunk unnamed-chunk-28](R3_RGraphics_true-figure/unnamed-chunk-28-3.png)

```r
plot(gfile[sel,],col="beige")
```

![plot of chunk unnamed-chunk-28](R3_RGraphics_true-figure/unnamed-chunk-28-4.png)

Plot raster
=========================
Global landcover
```
Download raster file here:
http://due.esrin.esa.int/files/Globcover2009_V2.3_Global_.zip

install.packages("raster")
```


```r
library(raster)
library(rgdal)

setwd('c:/CLEMSON/GIS/Raster/Globcover2009_V2.3_Global_/')
#import raster
Gcover <- raster("GLOBCOVER_L4_200901_200912_V2.3.tif")
#plot raster
plot(Gcover,main="GLobal Land cover")
```

![plot of chunk unnamed-chunk-29](R3_RGraphics_true-figure/unnamed-chunk-29-1.png)

Working with NetCDF
=========================
Global temperature data set
```
Download NetCDF file
ftp://ftp.cdc.noaa.gov/Datasets/cru/hadcrut2/ltm/air.mon.ltm.nc


install.packages("ncdf4")
```


```r
library(ncdf4)
library(RColorBrewer)
library(maps)
setwd('c:/CLEMSON/GIS/nc/')
file <- nc_open("air.mon.ltm.nc")
nlon <- ncvar_get(file,"lon")
nlat <- ncvar_get(file,"lat")
nlat1 <- sort(-nlat)

temp <- ncvar_get(file,"air")

jet.colors <-colorRampPalette(c( "blue","grey","white","grey","red"))

filled.contour(nlon,nlat1,temp[,,1],
                color.palette = jet.colors,
               xlab="Longitude",ylab="Latitude",
               plot.axes = {par(usr=c(-180,180,-90,90));map(add=T)},
               key.title = title(main = "R"))
```

![plot of chunk unnamed-chunk-30](R3_RGraphics_true-figure/unnamed-chunk-30-1.png)

