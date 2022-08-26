# load usd from own container
FROM smthfor/usd:latest

WORKDIR /usr/src/ufg

# Configuration
ARG UFG_RELEASE="99fe71720917bb31e0b08723295a14b5d4ba7825"
ARG UFG_SRC="/usr/src/ufg"
ARG UFG_INSTALL="/usr/local/ufg"
ENV USD_DIR="/usr/src/app/USDinst"
ENV LD_LIBRARY_PATH="${USD_DIR}/lib:${UFG_SRC}/lib"
ENV PATH="${PATH}:${UFG_INSTALL}/bin"
ENV PYTHONPATH="${PYTHONPATH}:${UFG_INSTALL}/python"

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    build-essential \
	cmake \
	make \
	nasm
# Build + install usd_from_gltf
RUN git init && \
    git remote add origin https://github.com/google/usd_from_gltf.git && \
    git fetch --depth 1 origin "${UFG_RELEASE}" && \
    git checkout FETCH_HEAD && \
    python "${UFG_SRC}/tools/ufginstall/ufginstall.py" -v "${UFG_INSTALL}" "${USD_DIR}" && \
    cp -r "${UFG_SRC}/tools/ufgbatch" "${UFG_INSTALL}/python" && \
    rm -rf "${UFG_SRC}" "${UFG_INSTALL}/build" "${UFG_INSTALL}/src"

RUN apt update && apt -y upgrade
RUN apt-get -y install curl dirmngr apt-transport-https lsb-release ca-certificates musl-dev  
RUN ln -s /usr/lib/x86_64-linux-musl/libc.so /lib/libc.musl-x86_64.so.1

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get -y install nodejs
RUN apt autoremove -y && \
	apt-get autoclean -y

WORKDIR /usr/src/app
