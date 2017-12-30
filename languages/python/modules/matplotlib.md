# matplotlib - 

Module used for Data Visualization in python.


### Installation

    $ pip install matplotlib

### Import module

    >>> import matplotlib.pyplot as plt

### Simple plot

For example, take two lists `yrs` and `pop`, if you want to plot
poplutation(`pop`) increase over the years(`yrs`) you may do:

    >>> yrs = [1990, 2000, 2010, 2020]
    >>> pop = [2.55, 3.65, 5.82, 8.21]
    >>> plt.plot(yrs, pop)
    [<matplotlib.lines.Line2D object at 0x0000000008EC87F0>]
    >>> plt.show()

![Plot Figure](/languages/python/plt.PNG )

