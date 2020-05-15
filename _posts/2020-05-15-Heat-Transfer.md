---
title: Heat Transfer
categories: Posts
tags: [Python][Heat Transfer]
author: arpc
---

### Solving 2-D Heat Transfer problem using Python  

The following tries solves the classical conduction-convection problem in a 2-dimension problem. The goal is to reproduce the temperature distribution in a domain composed by two blocks of different thermal properties. A centrally located zone is constantly at a higher temperature and the two blocks do not exchange heat (ideally a vacuum between them).  


The following image shows the problem to be solved.
![GitHub Logo]({{ site.url }}/assets/images/heat_transfer_no_exhange.jpg)

#### The Heat Transfer Equation
The heat equation is a partial differential equation that describes how the distribution of some quantity (in this case, heat) evolves over time in a solid medium, as it spontaneously flows from places where it is higher towards places where it is lower. It is a special case of the diffusion equation. This equation was first developed and solved by Joseph Fourier in 1822 to describe heat flow.

In the special cases of propagation of heat in an aniisotropic and homogeneous medium in a 2-dimensional space, the heat flow equation results in the following

<img src="https://latex.codecogs.com/svg.latex?\Large&space;\frac{\mathrm{d} T}{\mathrm{d} t} = Dx\frac{\partial^2 T}{\partial x^2} + Dy\frac{\partial^2 T}{\partial y^2}" title="2D heat transfer equation" />

where Dx and Dy are the thermal diffusivity and is related to the thermal conductivity, material density and heat capacity as:

<img src="https://latex.codecogs.com/svg.latex?\Large&space;D = \frac{K}{\rho C}" title="Diffusivity relation" />

In order to solve this equation numerically, the strategy here usede is to apply finite difference approximations in the first equation, resulting in the following expression.

<img src="https://latex.codecogs.com/svg.latex?\Large&space;\frac{T_{i,j}^{(n+1)} - T_{i,j}^{(n)}}{\Delta t}  = D_x \frac{T_{i+1,j}^{(n)} - 2T_{i,j}^{(n)} +T_{i-1,j}^{(n)} }{(\Delta x)^2} +  D_y \frac{T_{i,j+1}^{(n)} - 2T_{i,j}^{(n)} +T_{i,j-1}^{(n)} }{(\Delta y)^2}" title="Finite difference approximation" />

Thus, the state of the system at time step n+1, is calculated from its state at time step n. The following code applies the above finite difference approximation in order to calculate the evolution of a temperature field in a domain composed by two blocks with different thermal properties. Before starting the code, it is important to highlightthat the maximun time step Δt that results in stable propagation is:

<img src="https://latex.codecogs.com/svg.latex?\Large&space;\Delta t = \frac{1}{D_{max}}\frac{(\Delta x\Delta y)^2}{(\Delta x)^2 + (\Delta y)^2}" title="Max time step" />

#### Python Code
We are ready for the source code. Before starting, the code here described was developed on python 2.7. The first step is to import necessary modules.
```python
import numpy as np
import matplotlib.pyplot as plt
from PIL import Image
import glob
import itertools
```

In sequence, it was defined the time step and set the "plot window grafical output" 

```python
#Set Time Step
dt=0.0002
# Set colour interpolation and colour map.
# You can try set it to 10, or 100 to see the difference
# You can also try: colourMap = plt.cm.coolwarm
colorinterpolation = 50
colourMap = plt.cm.jet
```

Next, it is defined 2 functions. The first one is a grid generator and the second is a finite difference approximation that will be used to compute the the equation 1 in forward steps.

```python
# Grid Generator
def do_grid(nxmin, nxmax, nymin, nymax):
    gridX, gridY = np.meshgrid(np.arange(nxmin, nxmax), np.arange(nymin, nymax))
    return gridX, gridY
    
# Finite Difference Approximation
def do_timestep(u0, u,Diffx,Diffy):
    u[1:-1, 1:-1] = u0[1:-1, 1:-1] + Diffx[1:-1, 1:-1]* dt * ((u0[2:, 1:-1] - 2*u0[1:-1, 1:-1] + u0[:-2, 1:-1])/dx2 )+ Diffy[1:-1, 1:-1]* dt * ( (u0[1:-1, 2:] - 2*u0[1:-1, 1:-1] + u0[1:-1, :-2])/dy2 )
    u0 = u.copy()
    return u0, u

    u0 = u.copy()
    return u0, u
```

Alright. Now we have aready set the 2 functions needed for this code: (I) The grid, to calculate the temperature at each element and (II) the finite difference calculation at each time-step. In the following, the total domain is defined:

```python
# Set Total Domain
lenX = lenY = 20 #we set it rectangular
# intervals in x-, y- directions, mm
dx = dy = 0.2
dx2 = dx*dx # second derivative in x
dy2 = dy*dy # second derivative in x
#number of elements 
nx = int(lenX/dx)
ny = int(lenY/dy)
```
For the current problem, the total domain comprehends 2 distinct parts, each one covering one half of the total domain. Thus, let's define the properties of the upper part (Part 1).

```python
#-------------PART 1 ------------

# Thermal diffusivity in X, mm2.s-1
Dx1 = 10.
# Thermal diffusivity in y, mm2.s-1
Dy1 = 10.
# Boundary condition
# Initial Temperature of interior grid
T1ini = 10.
nx1=nx
ny1=int(ny/2)
```

The same of the bottom part (Part 2).
```python
#-------------PART 2 ------------
# Thermal diffusivity in X, mm2.s-1
Dx2 = 20.
# Thermal diffusivity in y, mm2.s-1
Dy2 = 20.
# Boundary condition
# Initial Temperature of interior grid
T2ini = 30.
nx2=nx
ny2=ny
```

Great! All the subdomains are defined. Lets proceed creating the meshgrid of our problem. Remember that the grid generation function was previously defined.
```python
# Set meshgrid
X, Y = do_grid(0, nx, 0, ny)
X=X[1,:].copy()
Y=Y[:,1].copy()
```

Now, we will start with the initial conditions of the total domain. Remember that the initial temperature of each individual part have already been written, so now we will put this information in the Temperature Matrix of the total domain. More over, we will assume an initial higher temperature (100) at the central region (20%-80%) of the  bottom surface of the top part and the top surface of the bottom part. 



```python
# Total Diffusivity matrix in X
DiffTotalX = np.zeros((max(nx1,ny2),max(ny1,ny2)))
DiffTotalX[0:ny1, 0:nx1]=Dx1
DiffTotalX[ny1:ny2, 0:nx2]=Dx2
DiffTotalX[ny1-1,0:nx1] = 0
DiffTotalX[ny1,0:nx1] = 0

# Total Diffusivity matrix in y
DiffTotalY = np.zeros((max(nx1,ny2),max(ny1,ny2)))
DiffTotalY[0:ny1, 0:nx1]=Dy1
DiffTotalY[ny1:ny2, 0:nx2]=Dy2
DiffTotalY[ny1-1,0:nx1] = 0
DiffTotalY[ny1,0:nx1] = 0

# Initial conditions
T = np.zeros((max(nx1,ny2),max(ny1,ny2)))
T[0:ny1, 0:nx1]=T1ini # Set array size and set the interior value with Tini
T[ny1:ny2, 0:nx2]=T2ini # Set array size and set the interior value with Tini
T[int(nx/2), int(0.2*nx):int(0.8*nx+1)] = 100
T[int(nx/2-1), int(0.2*nx):int(0.8*nx+1)] = 100
T0=T.copy()
```

We are almost in the end... We will now start doing the calculation. We will define 10000 calculation steps (we had previously defined the lenght of those steps dt=0.0002 units of time), meaning that the calculation represents a total duration of 2 units of time. We will also store one figure every 500 steps, representing one figure every 0,1 unit of time.

```python
# Number of timesteps
nsteps = 10001
t=[]


# Output figures at these timesteps
mfig=[]
for i in range (0,10001,500):
    mfig.append(i)
fignum = 0
fig = plt.figure()
AllT=[]
for m in range(nsteps):
    T0, T = do_timestep(T0, T,DiffTotalX,DiffTotalY)
    T[int(nx/2), int(0.2*nx):int(0.8*nx+1)] = 100
    T0[int(nx/2), int(0.2*nx):int(0.8*nx+1)] = 100
    if m in mfig:
        plt.clf()
        fignum += 1
        print(m, fignum)
        plt.pcolormesh(X,Y,T,vmin=0, vmax=100,cmap=colourMap)
#        plt.contourf(X, Y, T0,Vmin=0, Vmax=100 colorinterpolation, cmap=colourMap)
        # Set Colorbar
        plt.colorbar()
        plt.savefig('temperature' + str("%03d" %fignum) + '.jpg')
        
#fig.subplots_adjust(right=0.85)
#cbar_ax = fig.add_axes([.9, 0.15, .03, 0.7])
#cbar_ax.set_xlabel('$T$  (C)', labelpad=20)
#fig.colorbar(im, cax=cbar_ax)
plt.show()
```

Finally, with the figures generate, lets create a .gif animation.
```python
#creating the gif
# Create the frames
frames = []
imgs = glob.glob("*.jpg")
for i in imgs:
    new_frame = Image.open(i)
    frames.append(new_frame)
    print(i)
 
# Save into a GIF file that loops forever
frames[0].save('temperature.gif', format='GIF',
               append_images=frames[1:],
               save_all=True,
               duration=200, loop=0)
```



The .gif should look like this (reload this page if no animation is shown). 

![GitHub Logo]({{ site.url }}//assets/animations/temperature.gif)

Notice that this example considers that NO HEAT EXCHANGE between Part 1 and Part 2 takes place, meaning that they are independent from each other.

That is it! You can play around with the variables and check the results!!!


