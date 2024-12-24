ARG UV_VERSION=0.5.11
ARG PYTHON_IMAGE_VERSION=313
ARG HADOLINT_VERSION=2.12.1-beta

# Define alias for uv and hadolint images
FROM ghcr.io/astral-sh/uv:$UV_VERSION AS uv
FROM ghcr.io/hadolint/hadolint:$HADOLINT_VERSION AS hadolint

# syntax=docker/dockerfile:1
FROM quay.io/fedora/python-$PYTHON_IMAGE_VERSION:${PYTHON_IMAGE_VERSION} AS base

# Set permissions and group ownership for use by rootless Podman and OpenShift
USER 0
RUN chown -R 1001:0 /opt/app-root/src && chmod -R g=u /opt/app-root/src
USER 1001

# Copy UV binary from the UV container into the final image
FROM base
COPY --from=uv --chown=1001:0 /uv /uvx /bin/
COPY --from=hadolint /bin/hadolint /bin/
