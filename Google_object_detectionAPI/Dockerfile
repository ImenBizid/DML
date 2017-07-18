
FROM ubuntu

MAINTAINER Imen BIZID

# Install dependencies
RUN apt-get update && apt-get install -y \
    python-pip \
    git

RUN pip install --upgrade pip

RUN apt-get update 

RUN pip install tensorflow

RUN apt-get install -y protobuf-compiler python-pil python-lxml python-pip python-dev git
RUN pip install jupyter
RUN pip install matplotlib

WORKDIR /tensorflow

RUN git clone https://github.com/tensorflow/models.git

WORKDIR /tensorflow/models

RUN protoc object_detection/protos/*.proto --python_out=.

RUN export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim

RUN python object_detection/builders/model_builder_test.py

