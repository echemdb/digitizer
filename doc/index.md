---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.13.6
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

```{raw-cell}
<!-- 
The original figure in this documentation were produced with Xournal++ (./files/others/example_plot.xopp). The content of the XOPP was exported as pdf (./files/others/example_plot.pdf). With the paginate function of svgdigitizer the page was exported as PNG and SVG.
* (./files/others/example_plot.png)
* (./files/others/example_plot.svg)

The latter was renamed and to ./files/others/example_plot_demo.svg and the curve was digitized. The digitized plot was exported as ./files/others/example_plot_demo.png
-->
```

Welcome to svgdigitizer's documentation!
========================================

The `svgdigitizer` allows recovering data from a curve in a figure, 
plotted in a 2D coordinate system.
Such plots are often found in scientific publications, where
in many cases, especially for old puplications, the source data 
is not accessible anymore. 
In some cases, the axes of the plot can be skewed, e.g., in scanned
documents. An extreme case for such a plot is depicted in the following figure.

![files/images/example_plot_p0.png](files/images/example_plot_p0.png) 

In order to recover the source data, first the plot is imported in a 
vector graphics program, such as [Inkscape](https://inkscape.org/).
The curve is traced with *regular bezier paths* and two points and text labels
are created and grouped for each axis to define the coordinate system.
The curve should be assigned a text label. Additional labels describing the data 
can be provided anywhere in the SVG file. The resulting file looks as follows.

![files/images/example_plot_p0_demo.png](files/images/example_plot_p0_demo.png)

+++

## [Command line interface](cli.md)
This SVG can be digitized from the [command line interface](cli.md), which creates a {download}`CSV <./files/others/example_plot_p0_demo.csv>` file of the x and y data (here U and v). 
The sampling of the bezier paths can be set by `--sampling-interval` which specifies the sampling interval in x units. In this specific case also indicate that the axes are `--skewed`.  


```sh .noeval
svgdigitizer digitize example_plot_p0_demo.svg --sampling-interval 0.01 --skewed
```

+++

## [API](api.md)
With the Python [API](api.md), the SVG can also be used to create an [SVGPlot instance](api/svgplot.md).

```{code-cell} ipython3
from svgdigitizer.svg import SVG
from svgdigitizer.svgplot import SVGPlot

plot = SVGPlot(SVG(open('./files/others/example_plot_p0_demo.svg', 'rb')), sampling_interval=0.01, algorithm='mark-aligned')
```

Now axis labels or any other text label in the SVG can be queried.

```{code-cell} ipython3
plot.axis_labels
```

```{code-cell} ipython3
plot.svg.get_texts()
```

The sampled data can be extracted as a [pandas](https://pandas.pydata.org/) dataframe, where the values are given the original plots units:

```{code-cell} ipython3
plot.df
```

A plot can be created via

```{code-cell} ipython3
plot.plot()
```

Installation
============

The package is hosted on [PiPY](https://pypi.org/project/svgdigitizer/) and can be installed via

```sh .noeval
pip install svgdigitizer
```

+++

Read the [installation instructions](installation.md) on further details if you want to contribute to the project.

Further information
===================

The svgdigitizer can be enhanced with other modules for specific datasets.

Currently the following datasets are supported:
* [cyclic voltammograms](api/cv.md) (*I* vs. *E* — current vs. potential curves or *j* vs. *E* — current density vs. potential curves) commonly found in electrochemistry. For further details and requirements refer to the specific instructions of the [cv module](api/cv.md) itself or the detailed description on how to [digitize cyclic voltammograms](workflow.md) for the [echemdb](https://echemdb.github.io/website/).

If you have used this project in the preparation of a publication, please cite it as described [on our zenodo page](https://zenodo.org/record/5881475).

```{toctree}
:maxdepth: 2
:caption: "Contents:"
:hidden:
installation.md
cli.md
api.md
api/cv.md
workflow.md
```
