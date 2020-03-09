FROM dna.qbe.com:5000/dna/python3.6-base:latest
LABEL author="Tom Porter <tom.porter@qbe.com>"

# shutuf debconf
ARG DEBIAN_FRONTEND=noninteractive

# required for python click module
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

##################################################
# Project specific lines
#

# Install cmake (required for lightgbm)
RUN apt-get update \
        && apt-get install -y --no-install-recommends cmake \
        && apt-get autoremove -y \
        && apt-get clean \
        && rm -rf /usr/local/src/*

COPY requirements.txt .
RUN pip3 install -r requirements.txt

# Create MODULE_PATH directory to store module
ARG MODULE_PATH
ADD src $MODULE_PATH
WORKDIR $MODULE_PATH

# export MODULE_PATH to import modules from anywhere
ENV PYTHONPATH=$PYTHONPATH:$MODULE_PATH
