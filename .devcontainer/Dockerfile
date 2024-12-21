ARG UV_VERSION=0.5.11
ARG PYTHON_IMAGE_VERSION=312

# Use the argument to pull the UV binary image
FROM ghcr.io/astral-sh/uv:$UV_VERSION AS uv

# syntax=docker/dockerfile:1
FROM registry.access.redhat.com/ubi9/python-$PYTHON_IMAGE_VERSION AS base

WORKDIR /opt/app-root/src/

# Set permissions and group ownership for use by rootless Podman and OpenShift
USER 0
RUN chown -R 1001:0 /opt/app-root/src
RUN chmod -R g=u /opt/app-root/src
USER 1001

# Copy UV binary from the UV container into the final image
FROM base
COPY --from=uv --chown=1001:0 /uv /uvx /bin/

