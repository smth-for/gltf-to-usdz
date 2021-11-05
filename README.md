# GLTF to USDZ Service

## What's this repository about?

If you want to convert a `.gltf` file to an `.usdz` file you need a quite complex setup. This repository aims to simplify the whole conversion process by using a docker container.

We use the *usd_from_gltf* repository from Google [google/usd_from_gltf](https://github.com/google/usd_from_gltf) in conjunction with the *USD* repository from PixarAnimationStudios [PixarAnimationStudios/USD](https://github.com/PixarAnimationStudios/USD).

Since *USD* takes a long time to build, it has its own docker image (see `\usd`). You can find it on Docker Hub. https://hub.docker.com/r/smthfor/usdz

The *usd_from_gltf* tool can be found in `gltf-to-usdz` and is online at https://hub.docker.com/r/smthfor/gltf-to-usdz

There is also a version build with node installed, can be found in `gltf-to-usdz-node` and is online at https://hub.docker.com/r/smthfor/gltf-to-usdz-node


## How to run?

### CLI

Run the docker command:

`docker run -it --rm -v $(PWD):/usr/app smthfor/gltf-to-usdz:latest inputfile.glb outputfile.usdz`

