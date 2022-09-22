# [Choice] Node.js version (use -bullseye variants on local arm64/Apple Silicon): 18, 16, 14, 18-bullseye, 16-bullseye, 14-bullseye, 18-buster, 16-buster, 14-buster
ARG VARIANT=16-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/typescript-node:${VARIANT}

ARG GO_VERSION=1.19
# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends imagemagick graphviz inkscape curl fontconfig \
# Install gvm and go
    && curl -O https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer \
    && chmod +x gvm-installer \
    && GVM_NO_UPDATE_PROFILE=true ./gvm-installer master /usr/local \
    && echo "[[ -s /usr/local/gvm/scripts/gvm ]] && source /usr/local/gvm/scripts/gvm" > /etc/profile.d/gvm.sh \
    && source /usr/local/gvm/scripts/gvm \
    && gvm install go${GO_VERSION} \
    && gvm use go${GO_VERSION} --default \
    && rm gvm-isntaller
# install pyenv and pythong 3
    && curl -O curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer \
    && chmod +x pyenv-installer \
    && PYENV_ROOT=/usr/local/pyenv ./pyenv-installer
# Install a required font
    && curl -O https://noto-website.storage.googleapis.com/pkgs/NotoSansCJKjp-hinted.zip \
    && mkdir -p /usr/share/fonts/NotoSansCJKjp \
    && unzip NotoSansCJKjp-hinted.zip -d /usr/share/fonts/NotoSansCJKjp/ \
    && rm NotoSansCJKjp-hinted.zip \
    && fc-cache -fv



# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "source /usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node packages
# RUN su node -c "npm install -g <your-package-list -here>"