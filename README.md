# RandomBallCover
`RandomBallCover` is an implementation of a **Nearest Neighbor** (NN) data structure in OpenCL. **Random Ball Cover** (RBC) takes up where **Brute Force** (BF) leaves off. BF search on the GPU outperforms state-of-the-art NN search algorithms on the CPU. With RBC, it's possible to get even more performance gains than BF. RBC is a two-tier BF search that explores a heavily pruned search space. The data structure was proposed by Lawrence Cayton, and it's described in depth in two of his [papers](http://www.lcayton.com/papers.html).

![cover](http://i76.photobucket.com/albums/j16/paign10/rbc_cover_zpssqehm4b0.png)

Currently, a variation of the proposed algorithms is implemented that does approximate NN search. For the RBC construction, the data structure in the **Exact Search** algorithm is built where each database point is assigned to its nearest representative. The RBC search is done according to the **One-shot Search** algorithm. The main application of the project is the handling of 6-D (3-D geometric and 3-D photometric information) point clouds. For that purpose, the algorithm is able to perform on an input of |X|=|Q|=16384 and |R|=128 with the following results:
* RBC construction in x microseconds.
* RBC search in y microseconds.
* Mean error z.

# Note
The code was developed and tested on `Ubuntu 14.04.2`, on a system with an `AMD R9 270X` GPU.

The complete `documentation` is available [here](http://random-ball-cover.paign10.me).

For more details on the implemented algorithms, take a look at the project's [wiki](#).

# Dependencies
The project has a dependency on [CLUtils](https://github.com/pAIgn10/CLUtils) (which is automatically downloaded by cmake). If you'd like to remove this dependency, you should be able to modify the kernel interface classes with minimal effort.

There are currently 2 example applications. For `rbc_2d_plot`, you'll need [PLplot](http://plplot.sourceforge.net/). For `rbc_img_segmentation`, you'll need [OpenCV](https://github.com/jayrambhia/Install-OpenCV).

# Compilation

```bash
git clone https://github.com/pAIgn10/RandomBallCover.git
cd RandomBallCover

mkdir build
cd build

cmake ..
# or to build the tests too
cmake -DBUILD_TESTS=ON ..

make

# to run the examples (from the build directory!)
./bin/rbc_2d_plot
./bin/rbc_img_segmentation

# to run the tests (e.g.)
./bin/rbc_tests_rbc
# or with profiling information
./bin/rbc_tests_rbc --profiling

# to install the libraries
sudo make install
# you'll need to copy manually the kernel 
# files into your own projects

# to build the docs
make doxygen
firefox docs/html/index.html
```