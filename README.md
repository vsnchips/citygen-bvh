#  Agglomerative BVH Demo App

This is a demo built by Dan Aston https://danaston.nz

It builds a bounding volume heirarchy using agglomerative techniques.
Building is currently single threaded.
Traversal of the BVH is implemented as an intersection function in glsl, called for rays in the fragment shader.

![](journal/ghostbunny_normal.png)

## How to build it

The root source directory is srctree. 

Run:
```
cmake path/to/srctree
```
and then
```
make -j <cores>
```

Built on Arch Linux. I might jump over to Visual Studio and make some project files to build it on windows if someone really wants me to, and asks nicely :)

## How it works

The executable is "bin/BVH_Renderer". It requires no arguments.

The working directory must be a direct sibling of the srctree directory for example "BVHDemo/build".

Upon loading, you will have a black screen. You must choose a mesh or set of meshes to load into the bvh builder.

After loading meshes, click "Build the BVH".

This is a very slow BVH builder. If you are loading a mesh with more than 2 - 3000 triangles, its time to make a cup of tea.

If you want, you can build a BVH containing only a subset of the total amount of primitives by decrementing the "maximum primitives" slider before clicking build.

When it is built, the background will turn white due to the fragment shader's escape condition for a null BVH.

Now, click "Send the BVH to the GPU".

## Interaction

You can fly around with w a s d.\
You can orient the view while holding the left mouse button.\
You can x/y pan with the middle mouse.\
You can x/z pan with the right mouse.\
You can toggle rendering of either traversed primitives or brute forced primitives.\
You can slide the head node pointer around to highlight subtrees to observe the agglomeration pattern.

## What do the colors mean?

Ray -> primitive intersection events return the color of their normal.

The BVH is integrated like a participating medium.

White tinting counts the valid intersections and subsequent visitation of BVH nodes, and red tinting counts the iterations of the trace loop, which is finitely rolled out.

Red tinting indicates that the occluding geometry is deep in the bvh from the perspective of the testing ray. It indicates sequential occluded bounding hull tests while "climbing out" from "behind" the occluder.


## Roadmap

TODO: 
  > implement single-dispatch parallel build in a compute shader.\
  > ????\
  > Make it better!
