# Build an image that can do training and inference in SageMaker
# This is a Python 3 image that uses the nginx, gunicorn, flask stack
# for serving inferences in a stable way.

FROM ubuntu:16.04

MAINTAINER Amazon AI <sage-learner@amazon.com>

RUN apt-get -y update && apt-get install -y --no-install-recommends \
         wget \
         curl \
         python-dev \
         build-essential libssl-dev libffi-dev \
         libxml2-dev libxslt1-dev zlib1g-dev \
         nginx \
         ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN curl -fSsL -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    rm get-pip.py
 
RUN pip --no-cache-dir install \
        numpy \
        scipy \
        sklearn \
        pandas \
        flask \
        gevent \
        gunicorn \
        pystan 

RUN pip --no-cache-dir install \
        fbprophet 
        
ENV PYTHONUNBUFFERED=TRUE
ENV PYTHONDONTWRITEBYTECODE=TRUE
ENV PATH="/opt/program:${PATH}"

# Set up the program in the image
COPY prophet /opt/program
WORKDIR /opt/program

