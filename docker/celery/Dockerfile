FROM olearypatrick/hpccloud:bionic-python

LABEL maintainer="patrick.oleary@kitware.com" \
      version="1.0"

RUN adduser --system celery

# Install cumulus
RUN git clone https://github.com/Kitware/cumulus.git /cumulus && \
  cd /cumulus && \
  git checkout 0.9-maintenance && \
  cd / && \
  pip install --no-cache-dir -r /cumulus/requirements.txt && \
  pip install --no-cache-dir -e /cumulus && \
  pip install --no-cache-dir girder

# Set the broker URL
RUN sed -i s/localhost/rabbitmq/g /cumulus/cumulus/celery/commonconfig.py

RUN mkdir /keys && chown -R celery  /keys

COPY ./docker/celery/config.json /cumulus/cumulus/conf/config.json

RUN chown -R celery  /cumulus

# Copy over hpccloud
COPY . /hpccloud

# Change ownership
RUN chown -R celery  /hpccloud