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
names(mtcars)
head(mtcars)
print(mtcars)
```

========================================================
### Simple Summaries of Data Simple Summaries of Data
- Five-number summary

```r
summary(mtcars)
```
- Boxplots

```r
boxplot(mtcars$mpg,col="blue",main="Boxplot for mpg")
```

```r
factor(mtcars$cyl)
boxplot(mpg~cyl,data=mtcars,
        col=terrain.colors(3),main="MPG by car cylinders",
        xlab = "cylinders",ylab="mpg")
legend("topright",c("4","6","8"),fill = terrain.colors(3))
```

========================================================
- Histograms

```r
hist(mtcars$hp, col="magenta")
```
- Barplot

```r
barplot(mtcars$mpg,col="green",
        main="MPG for 32 cars")
```

========================================================
### Multiple historgrams

```r
par(mfrow=c(1,2))
hist(mtcars$mpg,col="blue")
hist(mtcars$wt,col="blue")
```
### Scatter plot

```r
plot(mtcars$mpg,mtcars$wt,main="Car Fuel vs Weight",
     xlab="Milage per Gallon",ylab="Weight",
     col = mtcars$cyl,pch=16,cex=3)
legend("topright",legend=c(8,6,4),pch=16,cex=3,
       col=c("grey","magenta","blue"))
dev.copy(png,"test.png") #Copy plot to png file
dev.off() #Close PNG device
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

```r
qplot(x,y,color) #aesthetic
qplot(x,y,color,data) #aesthetic+data
qplot(x,y,color,data,geom="point") #aesthetic+data+geometry
```
- Base plot

```r
data(iris)
qplot(Sepal.Length, Sepal.Width, data=iris)
```

===================
- Add aesthetic (size, shape, color)

```r
qplot(Sepal.Length, Petal.Length, data=iris,
      color=factor(Species),size=factor(Species),
      shape=factor(Species)) #aesthetic
```
- Add geom (points, lines)

```r
qplot(Sepal.Length, Petal.Length, data=iris,
      geom=c("point","smooth")) #geometry
```
- Linear fitting

```r
qplot(Sepal.Length, Petal.Length, data=iris, color=Species,
      geom=c("point","smooth"),method="lm")
```

========================================================
## Basic qplot: Histogram

```r
qplot(Sepal.Length,fill=Species, data=iris)
```

```r
qplot(Sepal.Length,data=iris,geom="density")
```

```r
qplot(Sepal.Length,data=iris,geom="density",
      color=Species)
```
## Basic qplot: Facets

```r
qplot(Sepal.Length,Petal.Length,facets=.~Species, data=iris)
```

========================================================
## Advanced ggplot: 
### Sample plot

```
ggplot(data,aes(x,y)) #data + aesthetic
ggplot(data,aes(x,y)) + geom_point() #data + aesthetic + geometry
```
- Example: in cheat sheet

```r
gp <- ggplot(mpg, aes(hwy, cty))

gp+geom_point(aes(color=cyl))
gp+geom_point(aes(color=factor(cyl)))
gp+geom_point(aes(color=factor(cyl)))+geom_smooth(method="lm")
gp+geom_point(aes(color=factor(cyl)))+geom_smooth(method="lm")
  +facet_grid(.~cyl)

ggsave("plot.png",width=5,height=5)
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

```r
counties <- map_data("county")
SC_counties <- subset(counties,region == "south carolina")
ggplot(data = SC_counties)+
  geom_polygon(aes(x=long,y=lat,fill=subregion),
               color="black")+
  coord_fixed(1.3)+
  guides(fill=FALSE)
```

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
names(gfile)
gfile$CNTRY_NAME

plot(gfile)
plot(gfile,col=rainbow_hcl(50))
llgridlines(gfile,lty=5)

sel <- gfile$CNTRY_NAME=="United Kingdom"
plot(gfile[sel,])
plot(gfile[sel,],col="beige")
```

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

setwd('c:/CLEMSON/GIS/nc/')
file <- nc_open("air.mon.ltm.nc")
nlon <- ncvar_get(file,"lon")
nlat <- ncvar_get(file,"lat")
nlat1 <- sort(-nlat)

temp <- ncvar_get(file,"air")

jet.colors <-colorRampPalette(c( "blue","grey","white","grey","red"))

filled.contour(nlon,nlat1,temp[,,1],
                color.palette = hsv.colors,
               xlab="Longitude",ylab="Latitude",
               plot.axes = {par(usr=c(-180,180,-90,90));map(add=T)},
               key.title = title(main = "R"))
```

