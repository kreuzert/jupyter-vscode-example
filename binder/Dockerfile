FROM quay.io/jupyter/minimal-notebook:notebook-7.6.3

# Step 1: Switch to root for installation
USER root

# Step 2: Install dependencies and openvscode-server
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    ca-certificates \
    tar \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /opt/openvscode-server \
    && curl -L https://github.com/gitpod-io/openvscode-server/releases/download/openvscode-server-v1.109.5/openvscode-server-v1.109.5-linux-x64.tar.gz \
        | tar -xz -C /opt/openvscode-server --strip-components=1 \
    && chown -R ${NB_UID}:${NB_GID} /opt/openvscode-server

# Step 3: Install jupyter-openvscode-server (for JupyterLab integration)
RUN pip install --no-cache-dir jupyter_openvscodeserver_proxy

# Step 4: Set environment variables and switch back to user
ENV PATH="/opt/openvscode-server/bin:${PATH}"

USER ${NB_UID}
