# 2D Conduction Heat Transfer utilizing Parallel Processing

In this project, we implement a conduction heat transfer simulation on a 2D plate, utilizing [parallel processing](https://en.wikipedia.org/wiki/Parallel_computing) with the use of [MPI](https://en.wikipedia.org/wiki/Message_Passing_Interface), [OpenMP](https://en.wikipedia.org/wiki/OpenMP) and [CUDA](https://en.wikipedia.org/wiki/CUDA).

## MPI
We split the computations accross multiple compute nodes, so each node is assigned a part of the computations. If fact, we split the 2D plate in subplates and each node computes conduction heat transfer on its own plate. Then, every node exchanges temperature information in their plate's boundaries with is neighbors, which are other nodes whose plates are adjacent to the node's.<br>
As a simplification, we assume every subplate is constantly heated in its central area, instead of only the center of the whole plate.<br>
* If we have N nodes, since the plates are squared, the number of nodes utilized must be a perfect square in order to have a perfectly balanced split. E.g. N can be one of {1,4,9,16,25,36,49,...}
* Since the plates are squared, the number of cells of the plate must be a perfect square, which must be chosen to be evenly split accross the N nodes. So, we must select the number of cells C as C=LCM(all possible number of nodes)<img src="https://render.githubusercontent.com/render/math?math={}^2 \cdot \text{M}^2"> where M is a positive integer. E.g. if <img src="https://render.githubusercontent.com/render/math?math=\text{N} \leq 25"> then LCM(1,4,9,16,25)=420 so the number of cells can be of the form <img src="https://render.githubusercontent.com/render/math?math=420^2 \cdot \text{M}^2"> where M=1,2,3,4,...
