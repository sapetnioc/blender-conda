# blender-conda
Compile Blender and create a Conda package.

## Disclaimer

I have a minimum experience with Blender compilation. There are several things that should be improved in the way it is compiled in the `recipe.yaml` file.

For now, only Linux is supported but I may add a support for Windows one day. I cannot do it for Mac beacause I do not have one.

## Package creation instructions

I highly recommend to use [Pixi](https://pixi.sh) instead of Conda to setup a build environment. Therefore, the first thing to do is to [install Pixi](https://pixi.sh/latest/installation/).

Then clone this project and use Pixi to enter the environement
```
git clone https://github.com/sapetnioc/blender-conda
cd blender-conda
pixi shell
```

To build the package, I use [rattler-build](https://rallter-build.prefix.dev) which is already install in the environment:
```
rattler-build build
```

This will compile Blender (the compilation step is quite long) and create the package in the directory `output/linux-64`.

## Test package

Create a brain new environment:
```
pixi init /tmp/test
```

Adds the previously created `output` directory in the list of channels (i.e. in the list of package repositories):
```
cd /tmp/test
pixi workspace channel add file:///path/to/blender-conda/output
```

Then activate the environment, install blender and launch it:
```
cd /tmp/test
pixi shell
pixi add blender
blender
```
