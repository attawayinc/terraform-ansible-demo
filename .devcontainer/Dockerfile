# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.145.1/containers/codespaces-linux/.devcontainer/base.Dockerfile

FROM mcr.microsoft.com/vscode/devcontainers/universal:0-linux

USER root

# [Option] Install Docker CLI
ARG INSTALL_DOCKER="false"
COPY library-scripts/docker-debian.sh /tmp/library-scripts/
RUN if [ "${INSTALL_DOCKER}" = "true" ]; then \
        rm -f /usr/local/share/docker-init.sh \
        && bash /tmp/library-scripts/docker-debian.sh "true" "/var/run/docker-host.sock" "/var/run/docker.sock" "codespace"; \
    fi \
    && rm -rf /var/lib/apt/lists/* /tmp/library-scripts/

# [Option] Install Terraform CLI & TFLint
COPY library-scripts/terraform-debian.sh /tmp/library-scripts/
RUN apt-get update && bash /tmp/library-scripts/terraform-debian.sh

# ** [Optional] Uncomment this section to install additional packages. **
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends ansible jq
    
USER codespace



