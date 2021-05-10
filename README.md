# Canopy-Object-Analysis

## Load library
```
library(raster)
library(FIELDimageR)
```

## Load image
```
EX.SC <-stack("EX_StandCount.tif")
plotRGB(EX.SC, r = 1, g = 2, b = 3)
```
![](canopy_RGB.png)<!-- -->

## Removing the soil
```
EX.SC.RemSoil <- fieldMask(mosaic = EX.SC, Red = 1, Green = 2, Blue = 3, index = "HUE")
```
![](canopy_remsoil.png)<!-- -->

## Building the plot shapefile (ncols = 1 and nrows = 7)
```
EX.SC.Shape <- fieldShape(mosaic = EX.SC.RemSoil,ncols = 1, nrows = 7)
```
![](canopy_shapefile.png)<!-- -->

## When all shapes are counted: minSize = 0.00
```
EX1.SC <-fieldCount(mosaic = EX.SC.RemSoil$mask, 
                   fieldShape = EX.SC.Shape$fieldShape,
                   minSize = 0.00)
```
![](canopy_counted.png)<!-- -->

## Object Area
```
EX1.SC$objectSel[[4]]
```
![](canopy_objectarea.PNG)<!-- -->

## No shape rejected because minSize = 0.00
```
EX1.SC$objectReject[[4]]
```

## Change minSize = 0.04
```
EX1.SC<-fieldCount(mosaic = EX.SC.RemSoil$mask, 
                   fieldShape = EX.SC.Shape$fieldShape,
                   minSize = 0.04)
```

## Object Area > 0.04
```
EX1.SC$objectSel[[4]]
```