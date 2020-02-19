# LR B-splines for matlab


## Introduction

LR B-splines is a technology which enables users to perform local refinement on B-spline surfaces or volumes, which traditionally have been limited to tensor products. This has a wide variety of applications within computer-aided design (CAD) and computer-aided engineering (CAE). While this library was written with the latter in mind, it is also possible to take use of it in a design environment.

## About the code

This is a matlab wrapper over the core c++ library. You will have to compile the c++ library first, followed by linking the `.mex` files provided here to this library. This will in turn allow give you the full power of a fast c++ library with the convenient matlab syntax on top.

## Compiling on Windows

1. Make sure the eigen library is properly included in the file `MatlabLR/src/Basisfunction.cpp``, e.g.

    #include "eigen3\Eigen\Dense"

and make sure the library is found.

2. Next, run the following command in matlab (when standing in the MatlabLR folder):

mex -outdir lib src\lrsplinesurface_interface.cpp src\LRSplineSurface.cpp src\Basisfunction.cpp src\Element.cpp src\LRSplineVolume.cpp src\Meshline.cpp src\MeshRectangle.cpp src/LRspline.cpp -Iinclude

3. Copy everything from MatlabLR/src/matlab to MatlabLR/lib

4. Test the code by running the following commands:

    addpath('lib/')
    lr = LRSplineSurface([3,3], [4,4])
    lr.refine()
    lr.raiseOrder(2,2)
    lr.refine(44)
    lr.refine(64)
    lr.plot('enumerate', 'basis')