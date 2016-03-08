**ndparse** is the NeuroData Parse parent repository

ndparse:  NeuroData Parse
=========================

Installation
------------

You can either clone this repository and use it locally, or install from pypi:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
pip install ndparse #not yet!
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use this Python library to easily interface with NeuroData algorithms to
manually annotate data, use computer vision algorithms and deploy
across large neuroscience datasets.

This repo contains the code needed to train, evaluate, and deploy code for parsing volumes of NeuroData images. 

It contains the legacy code for manno and macho.  The current version of ndod is divided into the three major components required to parse neuroscience data at scale:

- **mana**: manual annotation protocols and tools
- **maca**: big-data research algorithms to inform neuroscience
- **mad**: machine annotation for deployment and scaling.

To just use one of these, say **mana**, in python you can (and should) type the following: `from ndparse import mana`

*This repo is under extremely active development during the first quarter of 2016.  The previous version of mano, macho and ndod code may be found in [ndod](https://github.com/neurodata/ndod).  The core code that is used for computer vision by the neurodata team will be transitioned to a pip installable python package in the next few weeks.  Stay tuned.*

~~~
pip install conda
conda create -n ndparse2 -c ilastik ilastik-everything-but-tracking
source activate ndparse2
conda install ipython notebook
conda install requests gcc
pip install blosc
pip install ndio
~~~


For ilastik processing:

~~~

~~~

To plot an ndio obtained (RAMON or numpy array):

~~~
import ndparse as ndp
import ndio.remote.neurodata as ND
nd = ND()
token = 'kasthuri11cc'
channel = 'image'
im2 = nd.get_volume('ac3ac4','ac4_synapse_truth', 4400,5400, 5440, 6440, 1100, 1102, resolution=1)
im = nd.get_volume(token, channel, 4400, 5400, 5440, 6440, 1100, 1102, resolution=1)
ndp.plt(im,im2,slice=1, alpha=0.5)
~~~
