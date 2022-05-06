When you are measuring the dependence of a property on multiple independent variables, you now need to plot data in three dimensions. Examples of this typically occur with spatial measurements, where there is an intensity associated with each (x, y) point, like in a rastered microscopy measurement or spatial diffraction pattern. To visualize this data, we have a few options at our disposal — we will explore creating heatmaps, contour plots (unfilled and filled), and a 3D plot.

The dataset I will use for this example is a 2 µm x 2 µm micrograph from an atomic force microscope (AFM). First, we import packages — the two new packages we are adding this time are make_axes_locatable, which will help us with managing the colorbar for our plots, and Axes3D, which we need for our 3D plot:

# Import packages
%matplotlib inline
import matplotlib as mpl
import matplotlib.pyplot as plt
from mpl_toolkits.axes_grid1.axes_divider import make_axes_locatable
from mpl_toolkits.mplot3d import Axes3D
import numpy as np
We will now load our AFM data, again using numpy.loadtxt which will directly load our data into a 2D numpy array.

# Import AFM data
afm_data = np.loadtxt('./afm.txt')
We can then inspect a few rows our loaded data:

# Print some of the AFM data
print(afm_data[0:5])
>>> [[4.8379e-08 4.7485e-08 4.6752e-08 ... 6.0293e-08 5.7804e-08 5.4779e-08]
 [5.0034e-08 4.9139e-08 4.7975e-08 ... 5.7221e-08 5.4744e-08 5.1316e-08]
 [5.2966e-08 5.2099e-08 5.1076e-08 ... 5.4061e-08 5.0873e-08 4.7128e-08]
 [5.7146e-08 5.6070e-08 5.4871e-08 ... 5.1104e-08 4.6898e-08 4.1961e-08]
 [6.2167e-08 6.0804e-08 5.9588e-08 ... 4.7038e-08 4.2115e-08 3.7258e-08]]
We have a 256 x 256 array of points with each value corresponding to the measured height (in meters) at that position. Since we know that our data would be more meaningful if presented in nanometers, we can scale all our values by this constant parameter:

# Convert data to nanometers (nm)
afm_data *= (10**9)
Now we can go ahead and start visualizing our data. We start with setting some global parameters (edit these as you like, but these are settings I use):

# Edit overall plot parameters
# Font parameters
mpl.rcParams['font.family'] = 'Avenir'
mpl.rcParams['font.size'] = 18
# Edit axes parameters
mpl.rcParams['axes.linewidth'] = 2
# Tick properties
mpl.rcParams['xtick.major.size'] = 10
mpl.rcParams['xtick.major.width'] = 2
mpl.rcParams['xtick.direction'] = 'out'
mpl.rcParams['ytick.major.size'] = 10
mpl.rcParams['ytick.major.width'] = 2
mpl.rcParams['ytick.direction'] = 'ou
