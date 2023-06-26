# Files for the SPEX hands-on session

This repository contains the files for the SPEX
hands-on sessions. The session consists of three
parts:

- First, we look at the SPEX introduction notebook (`/intro`). This notebook explains step-by-step 
  how to do a spectral fit with SPEX.
- Then we do exercise #1 (`/ex1`) and fit a power law using what we learned before.
- In Exercise #2 (`/ex2`), we fit a power-law plus a Gaussian line. 

# Software installation

## Sciserver setup (recommended)

Create a HEASOFT image on Sciserver as explained on [the HEASOFT
Sciserver documentation
page](https://heasarc.gsfc.nasa.gov/docs/sciserver/). We have tested the
exercises with HEASOFT 6.31.1.

### Creating a conda environment for SPEX on Sciserver

Once you have the Jupyterlab environment running on Sciserver, write the
following commands in the terminal:
```
    (heasoft) idies@aaaa:~$ conda activate base
    (base) idies@aaaa:~$ conda create -n spex python=3.9 astropy matplotlib ipykernel
    (base) idies@aaaa:~$ conda activate spex
    (spex) idies@aaaa:~$ conda install -c spexxray spex pyspextools
    (spex) idies@aaaa:~$ python -m ipykernel install --user --name spex --display-name "(spex)"
```
Next we have add the following line
`"conda", "run", "--no-capture-output", "-n", "spex",` to this file
`~/.local/share/jupyter/kernels/spex/kernel.json` to try to make sure
that conda starts the spex conda environment:
```
    (spex) idies@aaaa:~$ vi ~/.local/share/jupyter/kernels/spex/kernel.json
```
In vi, get into edit mode by typing `i`. Now, you have a cursor to edit
the text file. Add the line
`"conda", "run", "--no-capture-output", "-n", "spex",` after the
`"argv": [` line.

In the end, the contents of
`~/.local/share/jupyter/kernels/spex/kernel.json` should look like this:
```
    {
     "argv": [
      "conda", "run", "--no-capture-output", "-n", "spex",
      "/home/idies/miniconda3/envs/spex/bin/python",
      "-m",
      "ipykernel_launcher",
      "-f",
      "{connection_file}"
     ],
     "display_name": "(spex)",
     "language": "python",
     "metadata": {
      "debugger": true
     }
    }
```
When the contents of the file look OK, press the `<Esc>` key on your
keyboard, and then type `:x` followed by the `<return>` key. The file
should be saved now.

It is necessary to restart the Jupyter session on Sciserver to load the
new SPEX environment into Jupyter properly. To do that, execute the
following steps:

-   Close the Jupyter window and go back to the page on Sciserver with
    the list of your images.
-   On this page, you can stop running the image by clicking the red
    square after the image name. Wait until the image is stopped.
-   When the image is fully stopped and the page reloaded, you can click
    the green triangle to start the image again.
-   Click on the name of the image to start Jupyter again. In this new
    session, SPEX should work in Jupyter.

## Alternative: Renkulab

We also have a [Jupyterlab environment with SPEX at
Renkulab.io](https://renkulab.io/projects/j.de.plaa/ahead2020-school-spex/sessions/).
Unfortuntately, HEASOFT is not (yet) working well in Jupyter Lab on
Renkulab. The XRISM hands-on session is best done on Sciserver.

## Laptop setup (advanced)

It is also possible to install the needed software on your own laptop.
This takes a bit more work and problems can occur. Therefore, we
recommend to use the Sciserver environment if you do not have a lot of
experience with installing software.

For these exercises, we use the following software packages:
-   [SPEX (version 3.07.03)](https://spex-xray.github.io/spex-help/index.html)

### Install SPEX through Anaconda

If you do not have conda yet, please install it using [these
instructions](https://docs.conda.io/en/latest/miniconda.html).

Once your conda installation is set up, you can create a spex
environment:
```
    (base) user@unix:~> conda create -n spex python=3.9 numpy scipy astropy pytest jupyterlab matplotlib pip mkl=2021.4
    (base) user@unix:~> conda activate spex
```
Now that we have a spex conda environment, you can install SPEX through
conda:
```
    (spex) user@unix:~> conda install -c spexxray spex pyspextools
```
And create a ipykernel for the (spex) environment to work in Jupyter:
```
    (spex) user@unix:~> python -m ipykernel install --user --name spex --display-name "(spex)"
```
## Troubleshooting

### Importing SPEX in Jupyter fails

When you have Jupyter installed in multiple places, it sometimes happens
that the wrong Jupyter executable is called. If you have trouble
importing SPEX, then try to run Jupyterlab like this to force it to use
Jupyter from the SPEX environment:
```
    (spex) user@unix:~> $CONDA_PREFIX/bin/jupyter-lab &
```
See also [this
discussion](https://github.com/spex-xray/spex-help/issues/32) for more
hints.

