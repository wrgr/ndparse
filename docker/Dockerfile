FROM ubuntu:16.04
# derived from neurodata/ndio docker file
MAINTAINER Will Gray Roncal <wrgr@jhu.edu>

# Update ubuntu
RUN apt-get clean
RUN apt-get update
RUN apt-get -y upgrade

# Install commonly used packages
RUN apt-get -y install build-essential

RUN apt-get -y install \
  python-pip \
  python-all-dev \
  zlib1g-dev \
  libjpeg8-dev \
  libfreetype6-dev \
  liblcms2-dev \
  libwebp-dev \
  tcl8.5-dev \
  tk8.5-dev \
  python-tk \
  libhdf5-dev \
  ipython \
  ipython-notebook \
  git vim

# Install conda
RUN pip install conda==4.1.6
RUN conda install conda -y
RUN conda install psutil -y

# Install packages for ndparse
ADD environment.yml /environment.yml
RUN conda env create -f /environment.yml
RUN pip install jupyter notebook

ENV PYTHONPATH /usr/envs/ndp/lib/python2.7/site-packages

# Install ndparse and ilastik separately to avoid install issues
WORKDIR /usr/envs/ndp/ilastik-meta/ilastik
RUN python setup.py install

RUN useradd -ms /bin/bash ndparse
WORKDIR /home/ndparse

RUN git clone http://github.com/neurodata/ndparse
WORKDIR /home/ndparse/ndparse
RUN python setup.py install


# Always run in bash shell
RUN ln -snf /bin/bash /bin/sh

EXPOSE 8888 6006
VOLUME /notebooks
WORKDIR "/notebooks"

USER ndparse

# Add environment to boot
RUN echo 'source activate ndp' >> ~/.bashrc

# Patch keras
RUN mkdir ~/.keras
RUN echo $' \n\
  {"image_dim_ordering": "th", \n\
   "epsilon": 1e-07, \n\
   "floatx": "float32", \n\
   "backend": "theano"}' >> ~/.keras/keras.json

# Export python path
 ENV PYTHONPATH /usr/envs/ndp/lib/python2.7/site-packages
