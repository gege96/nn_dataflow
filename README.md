Neural Network Dataflow Scheduling
==================================

This Python tool allows you to explore the energy-efficient dataflow scheduling
for neural networks.

We assume an Eyeriss-style NN accelerator for the hardware, i.e., a 2D array of
processing elements, each of which has a local register file, and a global SRAM
buffer.

We decouple the scheduling problem into two subproblem, mapping and ordering.
Mapping deals with mapping one 2D convolution computation (one 2D ifmap
convolves with one 2D filter to get one 2D ofmap) onto the hardware
accelerator; ordering then decides the order between all 2D convolutions. We
currently only support row stationary mapping, and support exhaustive search
over all loop blocking and reordering schemes.

See the details in our ASPLOS'17 paper (reference below).

If you use this tool in your work, we kindly request that you reference our
ASPLOS'17 paper (see reference below), and send us a citation of your work.


Find optimal schedule
-----------------------
First, define the NN structure in `examples/`. We already defined five NNs for
you, i.e., AlexNet, ZFNet, VGG16, VGG19, and ResNet.

Then, use `tools/eyeriss_search.py` to search for the optimal schedule for the
NN. Type
```
> python ./tools/eyeriss_search.py -h
```
for detailed options. You can specify PE array size, number of parallel arrays,
NN batch size and word size, register file and global buffer capacity, and the
energy cost of all components.

Finally, the two options, `--solve-loopblocking` and `--hybrid-partition2d`,
correspond to the analytical bypass schedule solution, and the hybrid
partitioning scheme, in our ASPLOS'17 paper. See the paper for details.


Verification
------------
To verify the tool against the Eyeriss ISCA'16 paper, run the following command
at the top directory.
```
> python ./tools/reproduce_eyeriss_papers.py isca16
```
Use the output results to draw the energy breakdown and compare against Figure
10 in the Eyeriss paper.


Reference
---------
Gao, Pu, Yang, Horowitz, and Kozyrakis, *Scalable and Efficient Neural Network
Acceleration with 3D Memory*, in ASPLOS'17. April, 2017.

