# 3dhuman-groupnorm
What happens when you have to **scrupulously share** GPUs with **others in the lab** and you need to run several, say **6 programs on a single 12GB TITAN card in one day**? What happens when you are impecunious as I am with only a **single 8GB 1070 card**? 

I give you this repo featuring **group normalization** version of **3d human pose heatmap** with **batch size = 1**. Memory occupation around **4GB**.

*Still under construction, probably faster than BART extension project* Only matches the performance of **H1** (heatmap loss only) as of now. 


----
## Prelude
For data, source code and installation, see the following two repos.

[I1](https://github.com/strawberryfg/int-3dhuman-I1)

[H1](https://github.com/strawberryfg/c2f-3dhm-human-caffe)

----
## Training 
See definition of **Adaptive I1**, **Manual** in [this repo](https://github.com/strawberryfg/int-3dhuman-I1).

- **d2 = 8**
  - **Adaptive I1**
  
  
  Start from BN counterpart (model: [net_iter_381324.caffemodel](https://drive.google.com/open?id=19MIdUvYXC90u58UMtfoXCirVwCZD6dHw); solverstate: [net_iter_381324.solverstate](https://drive.google.com/open?id=1hygJdVEdwZvk5JueKtr8fZDhwIlfMqZO))
  ```
  cd ../../training/d2=8
  $CAFFE_ROOT/build/tools/caffe train --solver=solver_d8_ada_gn.prototxt --weights=net_iter_381324.caffemodel
  ```
  | d2 | lr   |  "heatmap2" init std  | loss | Caffe Model  | Solver State |
  |:-:|:-:|:-:|:-:|:-:|:-:|
  | 8     | 2.5e-5 | 0.01   | Adaptive I1 | [net_iter_128489.caffemodel](https://drive.google.com/open?id=1-HVZolMWHPO7R1B_bjjoRLm6bP-1vE-H) | [net_iter_128489.solverstate](https://drive.google.com/open?id=1g5-ogIUVplDny3e_B_mXXcl8A5_EyRqR)|