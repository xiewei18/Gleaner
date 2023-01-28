# An Introduction to Making Scientific Publication Plots with Python | by Naveen Venkatesan | Towards Data Science
Save From : [An Introduction to Making Scientific Publication Plots with Python | by Naveen Venkatesan | Towards Data Science](https://towardsdatascience.com/an-introduction-to-making-scientific-publication-plots-with-python-ea19dfa7f51e) 

An introduction to how to use Python to plot data for scientific publications
-----------------------------------------------------------------------------

![](https://miro.medium.com/max/1400/1*SuY5vFBe3r1a5dbck7jYAg.jpeg)

Photo by [Isaac Smith](https://unsplash.com/@isaacmsmith?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/graph?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

I have been using Python to do scientific computations and make all of my plots for several years now. My primary motivations have been that (1) Python is open source, and (2) the amount of hard drive space taken up by MATLAB (especially on my laptop, where HD space comes at a premium). Also, never having to worry about keeping software licenses up to date has been an added plus. The flurry of trial-and-errors and Google searches I had to conduct until I found the “perfect” parameters for my plots has led me to put together this article — both as an informative tool for outside readers, and a way for me to document things for myself. Aesthetics are subjective, but I hope this tutorial can point out important settings and parameters that will allow you to customize any dataset to your personal preference. This is the first article in what I hope to be a series of tutorials — I will continue adding sections over time for different types of visualizations. I would recommend [installing Anaconda](https://www.anaconda.com/distribution/) if you don’t already have it as it contains all required packages for data analysis and visualization that you will need.

**Importing Packages**
======================

The majority of the functions used are in the `matplotlib` package (with most of the plotting functions being from `matplotlib.pyplot` subpackage). Additionally, I typically import `numpy` for any quick computations and `pylab` for quickly generating colors from any built-in colormap. Often times, when we import packages, we create a short-form alias (_i.e._ `mpl` for `matplotlib` ) so that we can refer to its functions using the alias instead of typing out `matplotlib` every single time.

```
\# Import required packages  
import matplotlib as mpl  
import matplotlib.pyplot as plt  
import numpy as np  
from pylab import cm
```

Loading Data
============

Since scientific instrument data is typically fairly simple (usually just one independent variable that we control and a measured, dependent variable), we can use `numpy.loadtxt` to import our data. For more complicated datasets, I highly recommend using `pandas` , which has incredibly sophisticated functions for loading and sanitizing data for visualizations — a comprehensive documentation can be found [here](https://pandas.pydata.org/pandas-docs/stable/reference/io.html). For this example, I have a file called `Absorbance_Data.csv` with some absorbance data for two samples collected on a spectrophotometer.

![](https://miro.medium.com/max/1400/1*GK0aB19sqrC5eBdMW-ktIg.png)

CSV file of absorbance data for two samples

We can load this data into our script with the following command:

```
\# Use numpy.loadtxt to import our datawavelength, samp\_1\_abs, samp\_2\_abs = np.loadtxt('Absorbance_Data.csv', unpack=True, delimiter=',', skiprows=1)
```

We pass our file to the `numpy.loadtxt` function along with the parameters:

`unpack`— transposes each column into an array, allowing you to unpack multiple variables at a time ( `wavelength` , `samp_1_abs` , `samp_2_abs` )

`delimiter` — delimiter character used to separate columns

`skiprows` — amount of rows to skip at the top of the file (since the first row is the column titles, we want to skip this so `skiprows=1` )

**Plotting Our Data**
=====================

Once we have loaded our absorbance data, we can quickly plot and inspect both of the datasets with the following code:

```
\# Create figure and add axes object  
fig = plt.figure()  
ax = fig.add_axes(\[0, 0, 1, 1\])\# Plot and show our data  
ax.plot(wavelength, samp\_1\_abs)  
ax.plot(wavelength, samp\_2\_abs)  
plt.show()
```

![](https://miro.medium.com/max/1400/1*ieQhbjP6bjqfOmx0Hp2V1A.png)

Initial plot of our absorbance data using default matplotlib settings

The data plots properly, but the default `matplotlib` settings just don’t give the figure that publication quality. As we change some of the parameters below, we will end up with a much better looking plot.

**Fonts**
=========

This is a setting that I spend an irrationally large amount of time on — picking the right font for my plots. Your system already comes with a long list of pre-installed fonts, and you can check which fonts are already available to `matplotlib` with the following:

```
import matplotlib.font_manager as fm\# Collect all the font names available to matplotlib  
font_names = \[f.name for f in fm.fontManager.ttflist\]  
print(font_names)
```

If you would like to install a new font to your computer and then use it for your plots, this is also possible. First, you must download and install your desired font — many options can be found [here](https://www.fontsquirrel.com/fonts/list/popular). Once installed, you must rebuild the font cache so that it will be available to `matplotlib` when you make your figure. We do this as follows:

```
import matplotlib.font_manager as fm\# Rebuild the matplotlib font cache  
fm._rebuild()
```

If you now check the list of available fonts, you should see the new font that you just installed.

**General Plot Parameters**
===========================

The three general parameters that I set at the beginning of my plot script are: (1) font, (2) font size, and (3) axis line width. These are essentially global parameters that I do not edit later so setting them at the beginning makes everything easier (_i.e._ do not have to explicitly set font/sizes for each label down the line). We must add the following code before we generate any figures, so I typically put it near the top of the script immediately after importing packages.

```
\# Edit the font, font size, and axes widthmpl.rcParams\['font.family'\] = 'Avenir'  
plt.rcParams\['font.size'\] = 18  
plt.rcParams\['axes.linewidth'\] = 2
```

Generate Set of Colors
======================

If you have a set of colors that you like to use, you are free to skip this step. In this case, since we only have two samples, it is better to manually select two high-constrast colors. But, if you want to generate a list of colors without too much effort on your end, we can use the `pylab` package we imported to generate a list of them from one of the various `matplotlib` built-in colormaps, which can be found [here](https://matplotlib.org/3.1.1/gallery/color/colormap_reference.html). This becomes very useful when you need a large number of colors, as you can generate them programatically.

For our dataset, we are just interested in easily distinguishing between our traces, so we would be best served using one of the colormaps in the qualitative section (I will use “tab10” for this example). We use the following code — the first argument is the colormap name and the second is the number of colors we want to generate:

```
\# Generate 2 colors from the 'tab10' colormap  
colors = cm.get_cmap('tab10', 2)
```

If we were, for example, measuring the temperature-dependence of a single sample and wanted to plot the spectra at different temperatures, we could use a diverging colormap such as “coolwarm”. Ultimately, the colormap you choose will be up to you and based on the type of data you are plotting.

**Create Figure and Axes**
==========================

We must create a figure, which is a blank window, and then add an axes object to it for our plot. To generate the figure, we have the following:

```
\# Create figure object and store it in a variable called 'fig'  
fig = plt.figure(figsize=(3, 3))
```

`figsize` — size of our figure (width, height) in inches, with the default being (6.4, 4.8)

Now we must add an axes object to our blank figure by specifying the bottom left coordinate and the width and height in relative coordinates (1 is the full size of the figure window). If we want it to fill our entire figure, we can specify `[0, 0, 1, 1]` which sets the bottom left corner to (0, 0) and the width and height to 1.

```
\# Add axes object to our figure that takes up entire figure  
ax = fig.add_axes(\[0, 0, 1, 1\])
```

![](https://miro.medium.com/max/778/1*eA3KdphW-IhkqKXVTjDWDw.png)

Blank figure with axes at (0, 0) with a width and height of 1

We can use this axis construction to create paneled figures and insets by making multiple axes objects as follows:

```
\# Add two axes objects to create a paneled figure  
ax1 = fig.add_axes(\[0, 0, 1, 0.4\])  
ax2 = fig.add_axes(\[0, 0.6, 1, 0.4\])
```

![](https://miro.medium.com/max/778/1*wZ27Z4TwjrVOzQ5-MYFEvA.png)

Blank figure with two paneled axes, one at (0, 0) and the other at (0, 0.6), with widths of 1 and heights of 0.4

```
\# Add two axes objects to create an inset figure  
ax1 = fig.add_axes(\[0, 0, 1, 1\])  
ax2 = fig.add_axes(\[0.5, 0.5, 0.4, 0.4\])
```

![](https://miro.medium.com/max/778/1*B29l6SBBTgILkq1m21Vsbg.png)

Blank figure with inset — first axes takes up whole figure and second is at (0.5, 0.5) with a width and height of 0.4

**Remove Spines**
=================

If we do not want our plot entirely enclosed, we can remove the top and right spines as follows:

```
\# Hide the top and right spines of the axis  
ax.spines\['right'\].set_visible(False)  
ax.spines\['top'\].set_visible(False)
```

![](https://miro.medium.com/max/778/1*7ZSAdIfrdRY-JuwdxZJZ2g.png)

Blank figure and axes with the top and right spines removed

**Tick Parameters**
===================

We can edit the tick widths and lengths to match our axis parameters with the following code. If we have minor ticks, we can also edit the properties of these:

```
\# Edit the major and minor ticks of the x and y axesax.xaxis.set\_tick\_params(which='major', size=10, width=2, direction='in', top='on')ax.xaxis.set\_tick\_params(which='minor', size=7, width=2, direction='in', top='on')ax.yaxis.set\_tick\_params(which='major', size=10, width=2, direction='in', right='on')ax.yaxis.set\_tick\_params(which='minor', size=7, width=2, direction='in', right='on')
```

`which` — whether we are editing `major` , `minor` , or `both` ticks

`size` — length of ticks in points

`width` — line width of ticks (we can set this to the same as our axis line width)

`direction` — whether ticks will face `in` , `out` , or `inout` (both)

`top` / `right` — whether there will be ticks on the secondary axes (top/right)

![](https://miro.medium.com/max/768/1*iUIelz92wRq1ytj0cffWhg.png)

Blank figure and axes with updated tick parameters

**Plotting and Adjusting Range/Ticks**
======================================

We can now again plot our data, using the colors that we generated from the colormap to distinguish the samples:

```
\# Plot the two sample absorbances, using previously generated colorsax.plot(wavelength, samp\_1\_abs, linewidth=2, color=colors(0), label='Sample 1')ax.plot(wavelength, samp\_2\_abs, linewidth=2, color=colors(1), label='Sample 2')
```

`linewidth` — line width of the line in the plot

`color` — color of the line in the plot

`label` — label for the trace (reference for the legend)

Now we can set the x and y-axis ranges with the following lines:

```
\# Set the axis limits  
ax.set_xlim(370, 930)  
ax.set_ylim(-0.2, 2.2)
```

![](https://miro.medium.com/max/718/1*OHk1sOmBSVu9bRmpZCJcDA.png)

Plot of sample absorbance using generated colors and manually set axis limits

We notice that the tick marks seem unbalanced between the two axes — we can also semi-manually edit this using a function called `MultipleLocator` which will create ticks at every multiple of a base number that we provide. We must edit the `major_locator` for the major ticks and `minor_locator` for the minor ticks. We will set major ticks every 100 nm and minor ticks every 50 nm for the x-axis and major ticks every 0.5 and minor ticks every 0.25 for the y-axis.

```
\# Edit the major and minor tick locationsax.xaxis.set\_major\_locator(mpl.ticker.MultipleLocator(100))  
ax.xaxis.set\_minor\_locator(mpl.ticker.MultipleLocator(50))  
ax.yaxis.set\_major\_locator(mpl.ticker.MultipleLocator(0.5))  
ax.yaxis.set\_minor\_locator(mpl.ticker.MultipleLocator(0.25))
```

![](https://miro.medium.com/max/728/1*0G5wh5TFGQ8t8gWjvTFjYQ.png)

Previous plot of absorbance with manually adjusted tick intervals

**Axis labels**
===============

We must add labels to the x and y-axes, which we can easily do with the following code:

```
\# Add the x and y-axis labelsax.set_xlabel('Wavelength (nm)', labelpad=10)  
ax.set_ylabel('Absorbance (O.D.)', labelpad=10)
```

`labelpad` — extra padding between the tick labels and the axis label

![](https://miro.medium.com/max/808/1*F3JN9GpLFOzSQYGGmz9OJw.png)

Absorbance plot with axis labels added

If you want to include Greek characters in your labels, you can use LaTeX syntax to do so. We create a raw string by prepending the string with `r` and enclose the LaTeX command with `$$` . However, this will use the default LaTeX font for the Greek characters — if we want to use the same font as the rest of the plot (assuming the character exists), we enclose our command with `$\mathregular{'Command goes here'}$`.

```
\# Add the x-axis label with λ for wavelengthax.set_xlabel(r'$\\mathregular{\\lambda}$ (nm)', labelpad=10)
```

![](https://miro.medium.com/max/808/1*hh9KDR6admnZm4W2wYMZtg.png)

Absorbance plot with x-axis label using LaTeX to typeset λ for wavelength

**Secondary Axis Ticks**
========================

If we want to place ticks on one of the secondary (top/right) axes to show either a different dataset or scaling, we can do so using a parasitic axis. This axes object duplicates one of the axes of the original plot, allowing you to change the scaling on the other. To illustrate this, we can use our absorbance data as an example. The current x-axis is the wavelength of absorbed light, but based on the application, the energy of this light might be the more relevant parameter.

We can create a second x-axis on the top of the plot to show the energy scaling. First, we must create a parasitic axis with either the `twinx()` or `twiny()` command to clone the x or y-axes, respectively. In this example, we want the y-axis data constant, so we will clone the y-axis. We also need to match the tick parameters of this new x-axis to the old plot’s x-axis (and remove `top='on'` from the original x-axis parameters).

```
\# Create new axes object by cloning the y-axis of the first plot  
ax2 = ax.twiny()\# Edit the tick parameters of the new x-axis  
ax2.xaxis.set\_tick\_params(which='major', size=10, width=2, direction='in')ax2.xaxis.set\_tick\_params(which='minor', size=7, width=2, direction='in')
```

To make our job of adding ticks in energy units to this axis easier, we can write a function to convert energy to wavelength (since we will place the ticks on the wavelength axis at points that energy values would correspond to). We will treat the input E as an array so we can do all the conversions at once:

```
\# Function to convert energy (eV) to wavelength (nm)  
def E\_to\_WL(E):  
    return \[1240/i for i in E\]
```

Since this is a non-linear transformation, we cannot easily use the `MultipleLocator` function, and we will add the tick marks manually, using a function called `FixedLocator` . To use `FixedLocator` we provide an array of all the locations at which we want there to be tick marks:

```
\# Add ticks manually to energy axisax2.xaxis.set\_major\_locator(mpl.ticker.FixedLocator(E\_to\_WL(np.linspace(1.5, 3.0, 4))))ax2.xaxis.set\_minor\_locator(mpl.ticker.FixedLocator(E\_to\_WL(np.linspace(1.4, 3.2, 19))))
```

Since we added the ticks manually, we must also add the major tick labels manually.

```
\# Add tick labels manually to energy axisax2.set_xticklabels(\['1.5', '2.0', '2.5', '3.0'\])
```

Finally, we also want to add an axis label to our new x-axis and make sure the axis limits are the same as the original x-axis:

```
\# Add energy axis label  
ax2.set_xlabel('Energy (eV)', labelpad=10)\# Set energy axis limits  
ax2.set_xlim(370, 930)
```

![](https://miro.medium.com/max/808/1*QIoSxREgKFq5lWzjQybW0Q.png)

Absorbance plot with secondary, non-linear energy x-axis

**Adding a Legend**
===================

The final thing we must add to our plot is a legend, so that a reader can know which trace corresponds to which sample. To do so, we can use the following code:

```
\# Add legend to plot  
ax.legend(bbox\_to\_anchor=(1, 1), loc=1, frameon=False, fontsize=16)
```

`bbox_to_anchor` — coordinate of the bounding box for our legend

`loc` — which part of the bounding box to use the coordinate of the `bbox_to_anchor` value ( `0` for automatic, `1` for top right corner, `2` for top left corner, `3` for bottom left corner, `4` for bottom right corner, `5` for right, `6` for center left, `7` for center right, `8` for lower center, `9` for upper center, and `10` for center)

`frameon` — whether to draw a frame around the legend

`fontsize` — font size for legend entries (if different from general parameter)

![](https://miro.medium.com/max/808/1*3hgnupbwTYNkWsf44a7QAw.png)

Final absorbance plot, with wavelength and energy x-axes, along with a legend

**Saving Your Plot**
====================

Lastly, saving your final plot is very simple — we can use the function `plt.savefig` to do this.

```
\# Save figure  
plt.savefig('Final\_Plot.png', dpi=300, transparent=False, bbox\_inches='tight')
```

`dpi` — resolution for a rastered image file format (in this case we are saving as `.png` file so this means that we are saving with a resolution of 300 dots per inch. The other possible file formats you can save are `.ps` , `.pdf` , and `.svg` which are all vector graphics formats, in which case you do not need to specify a `dpi` value)

`transparent` — whether to make the figure transparent, or with a white background

`bbox_inches` — defines the bounding box around the figure ( `tight` ensures that there is no extra whitespace around the figure)

To actually view our final plot in a figure window, we must add a `plt.show()` command after saving the figure.

```
\# Show figure  
plt.show()
```

**Conclusion**
==============

That’s it! We have successfully made a publication quality plot using Python! This example and all subsequent examples will be freely available online at this [Github repository](https://github.com/venkatesannaveen/python-science-tutorial).

Thanks for reading and I will continue to keep this series up to date with new examples and tutorials! You can follow me on [Twitter](https://twitter.com/naveenv_92) or connect with me on [LinkedIn](https://www.linkedin.com/in/naveenvenkatesan/) for more articles and updates.
## Note