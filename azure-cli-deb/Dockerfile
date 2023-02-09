FROM python:3.10-slim-buster
LABEL maintainer "Matt McCright <matt.mccright@gmail.com>" 
# Another option:
# FROM python:3.10-slim-bullseye
# Use this image to issue single az commands. 
# Converted to Debian from an alpine version 
# by Jessie Frazelle <jess@linux.com>
# https://github.com/jessfraz/dockerfiles/blob/master/azure-cli/Dockerfile

RUN apt-get update \
    && apt-get install \
	   bash

RUN set -x \
	&& apt-get install -y  \
		build-essential \
		libffi-dev \
		libssl-dev \
	&& pip install --upgrade \
		--pre azure-cli \
		--extra-index-url https://azurecliprod.blob.core.windows.net/edge \
		--no-cache-dir \
	&& apt-get remove -y \
	    build-essential \
		libffi-dev \
		libssl-dev \
    && apt-get autoremove -y

ENTRYPOINT	[ "az" ]
