plotk
=====

A two-dimensional plotting library written in pure Python using Tkinter.

To set things up to be able to plot using the vanilla Python shell, copy 
plotk.py and vector.py to somewhere in your Python path (e.g. using the 
PYTHONPATH environment vairable) and set pythonrc.py as your Python start-up 
script (e.g. by setting the PYTHONSTARTUP environment vairable).  To add new 
functions to the environment so they can modify the global workspace, use 
execfile() to import them.  For example, we might create a python script called 
loadtxt.py containing a simple function to import a tab-delimited text file:

    loadtxt.py:

    import string
    from vector import *

    def loadtxt(filename):
        file = open(filename, 'r')
        line = file.readline()
        names = line.rstrip().split('\t')
        for name in names:
            (globals()[name]) = vector()
        for line in file:
            values = line.lstrip().rstrip().split('\t')
            for i in range(len(names)):
                (globals()[names[i]]).append(str2num(values[i]))
        file.close()

By typing execfile('loadtxt.py') from the Python prompt, you would gain access 
to loadtxt() and could use it to import data in a tab-delimeted text file into 
the workspace and plot it.
