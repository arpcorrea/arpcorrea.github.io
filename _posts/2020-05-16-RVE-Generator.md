---
title: "RVE Generator"
excerpt: "This code generates a Fibre-Matrix Representative Volumetric Element (RVE) randomly placing fibres."
date: May 16, 2020
categories:
  - Code
tags:
  - RVE
  - Python
---

### RVE Random Generation

The following code creates a Representative Volumetric Element (RVE) containing fibres encompassed by a domain. It ideally
represents a micrography of 2 phases composite (Fibre + Matrix) that yields a value representative of the whole material.

For the sake of simpicity, the current RVE generator creates fibres randomly oriented, which limites the material 
compactation and allow us to reach fibre volumes (Vf) not higher than 50%. It is important to highlight that periodic boundary condition 
is considered (fibres leaving the domain are also found entering in the domain).

The following figure shows what we are expected to create:

![GitHub Logo]({{ site.url }}/assets/images/RVE.JPG)


#### Python Code
We are ready for the source code. Before starting, the code here described was developed on python 2.7. The first step is to import necessary modules.
```python
import math
import random
```

Then, since we are expecting to generate circles (representing the fibres), we need to define pi. Also, the X,Y domain same as fibre diameters need to be entered. Finally, an iteraction bound is used to limit the calculation

```python
pi = math.pi
VfTarget=0.5
X_axis = 10.
Y_axis=10.
CircleDiameter=0.7
maxiteration=2000
```

Great! In order to avoid complications in generating random fibres, 2 fibres are manually placed: (I) a central fibre and (II) the corner fibre. For the later, each corner encompasses 1/4 of the fibre. 

```python
#First fibres positioned: 1 centered and 1 in the 4 corners
Finalfibres=[]
Finalfibres.append([4,0.,0.,CircleDiameter])
Finalfibres.append([4,X_axis,0.,CircleDiameter])
Finalfibres.append([4,X_axis,Y_axis,CircleDiameter])
Finalfibres.append([4,0.,Y_axis,CircleDiameter])
Finalfibres.append([0,X_axis/2.,Y_axis/2.,CircleDiameter])
```

Alright. We have placed the 2 fibres and now we need to know the current fibre volumetric fraction, since we need will iterate the fibre generation until Vf_current = Vf_target (or at least it reaches maxiteration).

```python
#CURRENT VOLUMETRIC FRACTION
Vfactual = (2*pi*(CircleDiameter/2.)**2)/(X_axis*Y_axis)
```

Everything is almost defined... Before starting the random fibres placement, lets create a variable named "flag_iteration". This variable will count the number of iteractions that does not converge.

```python
#FLAG MASURING NUMBER OF ITERACTION 
flag_iteration=0
```

Cool! Are you ready? Lets start the random placement now. First, while Vf_actual < Vf_target, a "dummy Fibre" is randomly generated anywhere in the domain.

```python
#INITIATE RANDOM FIBRES
while Vfactual <= VfTarget:
    xCord=random.uniform(0,X_axis)
    xCord=round(xCord,2)
    yCord=random.uniform(0,Y_axis)
    yCord=round(yCord,2)
    dist = []
    flag = 0
```
Now, it is calculated the centre distance between this "dummy Fibre" and all the other previous "Accepted Fibres". If all the distances are greated than 1.05*D (this 1.05 was just defined to have at least 5%D gap), a flag =1 will say "ok, this fibre might be ellegible".
On the other hand, ff any distance is smaller than 1.05D, a flag=0 will say "sadly, this fibre is not ellegible" and than, flag_iteration will be incremented. 

```python
#TEST DISTANCE   
    for x in range(len(Finalfibres)):
        dist.append(math.sqrt(((xCord-Finalfibres[x][1])**2)+((yCord-Finalfibres[x][2])**2)))        
                 
    if all(i >= 1.05*CircleDiameter for i in dist) == True:      
        flag=1
        flag_iteration = 0
            
    else:
        flag=0
        flag_iteration=flag_iteration+1
```


Great! Now, lets consider only the cases in which flag = 1, meaning that the "dummy fibre" is ellegible to become an "accepted fibre". 5 cases are possible: (I) the fibre has partially extrapolated the top boundary of the domain
(II) the fibre has partially extrapolated the bottom boundary of the domain, (III) the fibre has partially extrapolated the right boundary of the domain, (IV) the fibre has partially extrapolated the left boundary of the domain or
(V) emcompassed by the domain.

In cases I-IV, it is said that the "dummy fibre" is periodic. What does it mean? It means that a "tween dummy fibre" is generated in a way that complements the "original dummy fibre". In other words, the amount that the 
"tween 1 dummy fibre" extrapolates the domain a "tween 2 dummy fibre" needs to compensate. In math, it resumes to: 

<img src="https://latex.codecogs.com/svg.latex?\Large&space;\u^{left} - u^{right} = 0 ; u^{top} - u^{bottom} = 0" title="Finite difference approximation" />

<img src="https://latex.codecogs.com/svg.latex?\Large&space;\u^{left} - u^{right} = 0 ; 

u^{top} - u^{bottom} = 0	" title="Periodic Boundary Condition" />

A visually representation is provided:

![GitHub Logo]({{ site.url }}/assets/images/periodic.JPG)

Alright, if this concept is clear, lets move on. If this "dummy fibre" is periodic, a "tween dummy fibre" will be created and, once again, the distances between the "tween dummy fibre" needs to be checked in respect to all the previous "accepted fibres".
Another constraint here imposed is that only 35% of the radius can extrapolate the domain. This constraint is imposed only for further meshing purposes (which is not the scope of this current post). Remembering that this process can only be done if 
flag_iteration<maxiteration.

```python
]#TEST FOR FIBRE IN THE EDGES
    if flag_iteration <maxiteration:
    
        if flag ==1:
            
            
# TOP
            if (yCord > Y_axis-0.65*CircleDiameter/2.) and (yCord < Y_axis-0.35*CircleDiameter/2.):
                xtemp = xCord
                ytemp = yCord-Y_axis
                for x in range(len(Finalfibres)):
                    dist.append(math.sqrt(((xtemp-Finalfibres[x][1])**2)+((ytemp-Finalfibres[x][2])**2)))
                if all(i >= 1.05*CircleDiameter for i in dist) == True:      
                    j=1
                    Finalfibres.append([j,xCord,yCord,CircleDiameter])
                    Finalfibres.append([j,xtemp,ytemp,CircleDiameter])
                    Vfactual = Vfactual + pi*((CircleDiameter/2.)**2)/(X_axis*Y_axis) 
                else:
                    Vfactual=Vfactual
                
# BOTTOM
            if (yCord < 0.65*CircleDiameter/2.) and (yCord > 0.35*CircleDiameter/2.):
                xtemp = xCord
                ytemp = yCord+Y_axis
                for x in range(len(Finalfibres)):
                    dist.append(math.sqrt(((xtemp-Finalfibres[x][1])**2)+((ytemp-Finalfibres[x][2])**2)))
                if all(i >= 1.05*CircleDiameter for i in dist) == True:      
                    j=-1
                    Finalfibres.append([j,xCord,yCord,CircleDiameter])
                    Finalfibres.append([j,xtemp,ytemp,CircleDiameter])
                    Vfactual = Vfactual + pi*((CircleDiameter/2.)**2)/(X_axis*Y_axis) 
                else:
                    Vfactual=Vfactual       
                    
     
# LEFT
            if (xCord < 0.65*CircleDiameter/2.) and (xCord > 0.35* CircleDiameter/2.) :
                xtemp = xCord+X_axis
                ytemp = yCord
                for x in range(len(Finalfibres)):
                    dist.append(math.sqrt(((xtemp-Finalfibres[x][1])**2)+((ytemp-Finalfibres[x][2])**2)))
                if all(i >= 1.05*CircleDiameter for i in dist) == True:      
                    j=-2
                    Finalfibres.append([j,xCord,yCord,CircleDiameter])
                    Finalfibres.append([j,xtemp,ytemp,CircleDiameter])
                    Vfactual = Vfactual + pi*((CircleDiameter/2.)**2)/(X_axis*Y_axis) 
                else:
                    Vfactual=Vfactual    
                    
# RIGHT
            if (xCord > X_axis-0.65*CircleDiameter/2.) and (xCord < X_axis-0.35*CircleDiameter/2.):
                xtemp = xCord-X_axis
                ytemp = yCord
                for x in range(len(Finalfibres)):
                    dist.append(math.sqrt(((xtemp-Finalfibres[x][1])**2)+((ytemp-Finalfibres[x][2])**2)))
                if all(i >= 1.05*CircleDiameter for i in dist) == True:      
                    j=2
                    Finalfibres.append([j,xCord,yCord,CircleDiameter])
                    Finalfibres.append([j,xtemp,ytemp,CircleDiameter])
                    Vfactual = Vfactual + pi*((CircleDiameter/2.)**2)/(X_axis*Y_axis) 
                else:
                    Vfactual=Vfactual               
    
    
# MIDDLE
            if (xCord > CircleDiameter) and (xCord < X_axis-CircleDiameter) and (yCord > CircleDiameter) and (yCord < Y_axis-CircleDiameter):
                    j=0
                    Finalfibres.append([j,xCord,yCord,CircleDiameter])
                    Vfactual = Vfactual + pi*((CircleDiameter/2.)**2)/(X_axis*Y_axis) 
        else:
            Vfactual=Vfactual   
    else:
        Vfactualstring=str(round(Vfactual*100,2))
        print("max iteration reached")
        print("Final Vf is "+ Vfactualstring+ "%")
        break
```

Good job! You finished your RVE!! All your "accepted fibres" are stored in a list called "Finalfibres". Now, lets plot and visually check it! 
```python
#Printing the RVE
from tkinter import *

root = Tk()

canvas = Canvas(width=X_axis*100, height=Y_axis*100)
canvas.pack()
canvas.create_rectangle(0,0,X_axis*100,Y_axis*100,  outline="yellow")


for x in range(len(Finalfibres)):
    canvas.create_oval(Finalfibres[x][1]*100-Finalfibres[x][3]/2*100, Finalfibres[x][2]*100-Finalfibres[x][3]/2*100,Finalfibres[x][1]*100+Finalfibres[x][3]/2*100,Finalfibres[x][2]*100+Finalfibres[x][3]/2*100)


root.mainloop()  # This call BLOCKS (so your program waits until you close the window!)
```

![GitHub Logo]({{ site.url }}/assets/images/RVE.JPG)

Your RVE should look like this . 

A final observation is here necessary: although we set Vf_target = 0.5 (meaning Vf= 50%), the random distribution algorithm (the one here described) will hardly achieve it with the ration domain/FibreDiameter here defined.
Within this current algorithm, Vf = 45-47% is easely achieved. Other algorithms (for example closes neighborhood RVE generator) are more powerful and can be used to achieve up to 60-63% Vf. 





