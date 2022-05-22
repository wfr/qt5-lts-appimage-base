# qt5-lts-appimage-base
Docker/Podman build environment for Qt 5 applications, aimed at maximum
compatibility with current Linux desktop distributions.

Based on:

* Ubuntu 18.04 LTS
* GCC 8
* Qt 5.15 with [KDE's LTS patches](https://community.kde.org/Qt5PatchCollection)
* [appimage-builder](https://github.com/AppImageCrafters/appimage-builder)
* [linuxdeployqt](https://github.com/probonopd/linuxdeployqt)

## Building
```
podman build -t qt5-lts-appimage-base -f Dockerfile.qt5-lts-appimage-base
```

## Example usage
Example Dockerfile for a CMake project mounted at `/host/repo`.
```
FROM localhost/qt5-lts-appimage-base
ARG QT_PREFIX=/opt/Qt/5.15-kde/

RUN mkdir /work
WORKDIR /work

RUN set -eux && \
	git clone /host/repo /work/repo && \
	mkdir -p repo/build && \
	cd repo/build/ && \
	cmake -DCMAKE_PREFIX_PATH=${QT_PREFIX} ../src/ && \
	make -j$(nproc)
```
