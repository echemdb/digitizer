# SVGDigitizer — Create (x,y) Data Points from SVG files.

![Logo](./logo.svg)

The purpose of this project is to digitize plots in scientific publications, recovering the measured data visualized in such a plot.

## Command Line Interface

There's a simple command line interface.

```
$ python -m svgdigitizer
Usage: python -m svgdigitizer [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  digitize
  plot
$ python -m svgdigitizer plot test/data/Ni111_NaOH_Beden1985_Fig2c.svg
[displays a plot]
$ python -m svgdigitizer digitize test/data/Ni111_NaOH_Beden1985_Fig2c.csv.expected
[creates test/data/Ni111_NaOH_Beden1985_Fig2c.csv]
```

## API

You can also use the `svgdigitizer` package directly from Python.
 
```python
from svgdigitizer.svgdigitizer import SvgData
filename='Ni111_NaOH_Beden1985_Fig2c.svg'
svg = SvgData(filename)
svg.plot()
```

`svgdigitizer.csvcreator` should contain converters for specific data. At the moment to create CV data.   
Note that it is invoked with the SVG's and YAML's basename without extension.

```python
from csvcreator import CreateCVdata
csv = CreateCVdata('Ni111_NaOH_Beden1985_Fig2c', create_csv=False)
csv.df.head()
csv.plot_CV()
```
