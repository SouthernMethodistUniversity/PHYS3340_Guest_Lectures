---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.12.0
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

```python jupyter={"outputs_hidden": false}
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import warnings
warnings.simplefilter(action='ignore', category=FutureWarning)

%config InlineBackend.figure_format ='retina'
```

# Generating Fractal From Random Points - The Chaos Game


This notebook details how to generate fractals from random points.

To get started, checkout this video by [Numberphile](https://www.youtube.com/watch?v=kbKtFN71Lfs)


## Initial Definitions


The goal of this exercise is to break down the individual steps of the procedure into functions.

To start we generate a list of points that represent our starting point and our verticies.

```python jupyter={"outputs_hidden": false}
def placeStartpoint(npts,fixedpts):
    #Start Point
    #start = (0.5,0.5)
    start = (np.random.random(),np.random.random())

    if fixedpts == []: #generates a set of random verticies
        for i in range(npts):
            randx = np.random.random()
            randy = np.random.random()
            point = (randx,randy)
            fixedpts.append(point)
            
    return (start,fixedpts)
        
```

Next we build our point chooser which will select a random vertex.

```python
def choosePts(npts,fixedpts,frac):
    #chooses a vertex at random
    #further rules could be applied here
    roll = np.floor(npts*np.random.random())
    point = fixedpts[int(roll)]
    
    return point
```

Then we iterate on our points.

```python jupyter={"outputs_hidden": false}
def placeItteratePts(npts,itt,start,fixedpts,frac):
    ittpts = []
    
    for i in range(itt):
        point = choosePts(npts,fixedpts,frac) #chooses a vertex at random
#        halfway = ((point[0]+start[0])*frac,(point[1]+start[1])*frac) #calculates the halfway point between the starting point and the vertex
        halfway = ((point[0]-start[0])*(1.0 - frac)+start[0],(point[1]-start[1])*(1.0 - frac)+start[1])
        ittpts.append(halfway)
        start = halfway #sets the starting point to the new point
        
    return ittpts
```

Lastly, we need to plot all of our points.

```python jupyter={"outputs_hidden": false}
def plotFractal(start,fixedpts,ittpts):
    # set axes range
    plt.xlim(-0.05,1.05)
    plt.ylim(-0.05,1.05)
    plt.axis('equal')
    
    #plots the verticies
    plt.scatter(np.transpose(fixedpts)[0],np.transpose(fixedpts)[1],alpha=0.8, c='black', edgecolors='none', s=30)
    #plots the starting point
    plt.scatter(start[0],start[1],alpha=0.8, c='red', edgecolors='none', s=30)    
    #plots the itterated points
    plt.scatter(np.transpose(ittpts)[0],np.transpose(ittpts)[1],alpha=0.5, c='blue', edgecolors='none', s=2)
    
    plt.show()
    return
```

## Generate Fractal


Once we have all of our functions, we can build a central function that calls everything we might need to generate an image.

```python jupyter={"outputs_hidden": false}
def GenerateFractal(npts,frac,itt,reg=False):
    #Error Control
    if npts < 1 or frac >= 1.0 or frac <= 0.0 or type(npts) is not int or type(frac) is not float or type(itt) is not int:
        print("number of points must be a positive integer, compression fraction must be a positive float less than 1.0, itt must be a positive integer")
        return
    if frac > 0.5:
        print("Warning: compression fractions over 1/2 do not lead to fractals")

    #Initilize Verticies
    if not reg:
        fixedpts = [] #Random Verticies
    else:
        if npts == 3:
            fixedpts = [(0.0,0.0),(1.0,0.0),(0.5,0.5*np.sqrt(3.0))] #Equilateral Triangle (npts = 3)
        elif npts == 4:
            fixedpts = [(0.0,0.0),(1.0,0.0),(1.0,1.0),(0.0,1.0)] #Square
        elif npts == 5:
            fixedpts = [(0.0,2./(1+np.sqrt(5.))),(0.5-2./(5+np.sqrt(5.)),0.0),(0.5,1.0),(0.5+2./(5+np.sqrt(5.)),0.0),(1.0,2./(1+np.sqrt(5.)))] #Regular Pentagon
        elif npts == 6:
            fixedpts = [(0.0,0.5),(1./4,0.5+.25*np.sqrt(3.)),(3./4,0.5+.25*np.sqrt(3.)),(1.0,0.5),(3./4,0.5-.25*np.sqrt(3.)),(1./4,0.5-.25*np.sqrt(3.))] #Regular Hexagon
        elif npts == 2:
            fixedpts = [(0.0,0.0),(1.0,1.0)] #Line
        elif npts == 1:
            fixedpts = [(0.5,0.5)] #Line
        elif npts == 8:
            fixedpts = [(0.0,0.0),(1.0,0.0),(1.0,1.0),(0.0,1.0),(0.5,0.0),(1.0,0.5),(0.5,1.0),(0.0,0.5)] #Carpet
        else:
            print("No regular polygon stored with that many verticies, switching to default with randomly assigned verticies")
            fixedpts = [] #Random Verticies

    #Compression Fraction
#    frac = 1.0/2.0 #Sierpinski's Triangle (npts = 3)
#    frac = 1.0/2.0 #Sierpinski's "Square" (filled square, npts = 4)
#    frac = 1.0/3.0 #Sierpinski's Pentagon (npts = 5)
#    frac = 3.0/8.0 #Sierpinski's Hexagon (npts = 6)

        
    if len(fixedpts) != npts and len(fixedpts) != 0:
        print("The number of verticies don't match the length of the list of verticies. If you want the verticies generated at random, set fixedpts to []")
        return
    if len(fixedpts) != 0:
        print("Fractal Dimension = {}".format(-np.log(npts)/np.log(frac)))
    
        
    (start, fixedpts) = placeStartpoint(npts,fixedpts)
    
    ittpts = placeItteratePts(npts,itt,start,fixedpts,frac)
    
    plotFractal(start,fixedpts,ittpts)
    
    return
    
    
```

## Make A Fractal

```python jupyter={"outputs_hidden": false}
# Call the GenerateFractal function with a number of verticies, a number of itterations, and the compression fraction
# The starting verticies are random by default. An optional input of True will set the verticies to those of a regular polygon.
GenerateFractal(3,.5,5000)
```

#### Regular Polygons


There are some famous fractals that can be generated this way that are rooted in regular polygons. These are often named after the Polish mathematician Waclaw Sierpinski but have existed long before he categorized them. For example [Sierpinski's Triangle](https://en.wikipedia.org/wiki/Sierpi%C5%84ski_triangle) and [Sierpinski's Carpet](https://en.wikipedia.org/wiki/Sierpi%C5%84ski_carpet).

```python jupyter={"outputs_hidden": false}
GenerateFractal(3,.5,50000,True)
```

```python jupyter={"outputs_hidden": false}
GenerateFractal(5,1./3,50000,True)
```

```python jupyter={"outputs_hidden": false}
GenerateFractal(6,3./8,50000,True)
```

```python jupyter={"outputs_hidden": false}
GenerateFractal(8,1./3.,50000,True)
```

<!-- #region heading_collapsed=true -->
#### Exploring Further: Dimension
<!-- #endregion -->

Fractals have, by definition, [fractional dimension](https://en.wikipedia.org/wiki/Fractal_dimension). We can model what that means here.

Roughly, fractional dimension is a measure of how much space a fractal fills and in our case will fall between 1 (a line) and 2 (a plane)

```python hidden=true jupyter={"outputs_hidden": false}
GenerateFractal(1,.5,50000,True)
```

```python hidden=true jupyter={"outputs_hidden": false}
GenerateFractal(2,.5,50000,True)
```

```python hidden=true jupyter={"outputs_hidden": false}
GenerateFractal(4,.5,50000,True)
```

<!-- #region heading_collapsed=true -->
#### Randomness on Large Scales
<!-- #endregion -->

To explore the nature of randomness, we can use our same function but increase the number of verticies that are randomly generated to a significantly large number.

This is an example of a [Monte Carlo method](https://en.wikipedia.org/wiki/Monte_Carlo_method).

```python hidden=true jupyter={"outputs_hidden": false}
GenerateFractal(10,.5,100)
```

```python hidden=true jupyter={"outputs_hidden": false}
GenerateFractal(10,.5,5000)
```

```python hidden=true jupyter={"outputs_hidden": false}
GenerateFractal(100,.5,5000)
```

```python hidden=true jupyter={"outputs_hidden": false}
GenerateFractal(100,.5,100000)
```

## Learn More:



[Chaos Game Wiki](https://en.wikipedia.org/wiki/Chaos_game)


[Numberphile Video](https://www.youtube.com/watch?v=kbKtFN71Lfs)


[Chaos in the Classroom](http://math.bu.edu/DYSYS/chaos-game/chaos-game.html)


[Chaos Rules!](http://www.maa.org/sites/default/files/pdf/upload_library/2/Devaney%202005.pdf)


[Barnsley Fern](https://en.wikipedia.org/wiki/Barnsley_fern)


## Modeling Life


There are many examples of fractals in nature. Here we have generated a fern. If we use the specific values below this is known as [Barnsley's Fern](https://en.wikipedia.org/wiki/Barnsley_fern).

```python
def makeFern(f,itt):            
    colname = ["percent","a","b","c","d","e","f"]
    print(pd.DataFrame(data=np.array(f), columns = colname))
    
    x,y = {0.5,0.0}
    xypts=[]
    if abs(sum(f[j][0] for j in range(len(f)))-1.0) < 10^-10:
        print("Probabilities must sum to 1")
        return
    for i in range(itt):
        rand = (np.random.random())
        cond = 0.0
        for j in range(len(f)):
            if  (cond <= rand) and (rand <= (cond+f[j][0])):
                x = f[j][1]*x+f[j][2]*y+f[j][5]
                y = f[j][3]*x+f[j][4]*y+f[j][6]
                xypts.append((x,y))
            cond = cond + f[j][0]
            
    xmax,ymax = max(abs(np.transpose(xypts)[0])),max(abs(np.transpose(xypts)[1]))
    plt.axes().set_aspect('equal')
    color = np.transpose([[abs(r)/xmax for r in np.transpose(xypts)[0]],[abs(g)/ymax for g in np.transpose(xypts)[1]],[b/itt for b in range(itt)]])
    
    plt.scatter(np.transpose(xypts)[0],np.transpose(xypts)[1],alpha=0.5, facecolors=color, edgecolors='none', s=1)
    
```

#### For Barnsley's Fern:
Use the following values

|__Percent__|__A__|__B__|__C__|__D__|__E__|__F__|
|---|---|---|---|---|---|---|
|0.01|0.0|0.0|0.0|0.16|0.0|0.0|
|0.85|0.85|0.04|-0.04|0.85|0.0|1.60|
|0.07|0.20|-0.26|0.23|0.22|0.0|1.60|
|0.07|-0.15|0.28|0.26|0.24|0.0|0.44|

Of course, this is only one solution so try as changing the values. Some values modify the curl, some change the thickness, others completely rearrange the structure.

```python jupyter={"outputs_hidden": false}
f = ((0.01,0.0,0.0,0.0,0.16,0.0,0.0),
     (0.85,0.85,0.08,-0.08,0.85,0.0,1.60),
     (0.07,0.20,-0.26,0.23,0.22,0.0,1.60),
     (0.07,-0.15,0.28,0.26,0.24,0.0,0.44))

makeFern(f,5000)
```

```python tags=[]

```

```python

```
