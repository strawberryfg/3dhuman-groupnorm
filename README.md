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
  | 8     | 2.5e-5 to 5e-6 after 30000 | 0.01   | Adaptive I1 | [net_iter_128489.caffemodel](https://drive.google.com/open?id=1-HVZolMWHPO7R1B_bjjoRLm6bP-1vE-H) | [net_iter_128489.solverstate](https://drive.google.com/open?id=1g5-ogIUVplDny3e_B_mXXcl8A5_EyRqR)|
  
  Train around **72 *mm***, test around **88 *mm***.
  
  - **Manual**
  
  ```
  $CAFFE_ROOT/build/tools/caffe train --solver=solver_d8_ada_gn_startgn_manual.prototxt --snapshot=net_iter_128489.solverstate
  ```
  | d2 | lr   |  loss ratio of 2D HM:3D HM:integral   | loss | Caffe Model  | Solver State |
  |:-:|:-:|:-:|:-:|:-:|:-:|
  | 8     | **1e-6** to 2e-7 after 37000 | 1:0.1:1   | Manual | [net_iter_121531.caffemodel](https://drive.google.com/open?id=1fgjHg0v2zzdlP9FD3wObwGtmITl7-0Lo)| [net_iter_121531.solverstate](https://drive.google.com/open?id=1YPGEiuNRXC54tn7a960v8ijq0mrAr5_R)|
  
  Train around **65 *mm***, test around **84 *mm***.
  
- **d2 = 16**
  - **Adaptive I1**
  ```
  cd ../../training/d2=16
  $CAFFE_ROOT/build/tools/caffe train --solver=solver_d16_ada_gn_startgn.prototxt --snapshot=net_iter_121531.solverstate
  ```
  
  | d2 | lr   |  "heatmap2" init std  | loss | Caffe Model  | Solver State |
  |:-:|:-:|:-:|:-:|:-:|:-:|
  | 16     | 2.5e-5 to 5e-6 after 180000 | 0.01   | Adaptive I1 | [net_iter_277648.caffemodel](https://drive.google.com/open?id=1tP-jrr2P5ksvO18dct4mt-6A2WElTuF0) | [net_iter_277648.solverstate](https://drive.google.com/open?id=1ujcBNVjBuzkTd7mZGIN8UzA1etzRvtg1) |
  
  Train around **47 *mm***, test around **66 *mm***.
  
- **d2 = 32**
  - **Adaptive I1**
  ```
  cd ../../training/d2=32
  $CAFFE_ROOT/build/tools/caffe train --solver=solver_d32_ada_gn_startgn.prototxt --snapshot=net_iter_277648.solverstate
  ```
  
  | d2 | lr   |  "heatmap2" init std  | loss | Caffe Model  | Solver State |
  |:-:|:-:|:-:|:-:|:-:|:-:|
  | 32     | 2.5e-5 to 5e-6 after 350000 | 0.01   | Adaptive I1 | [net_iter_350104.caffemodel](https://drive.google.com/open?id=1EwjC6AdpT4aGK8DQ1BRaFGTQBTv-FtZp) | [net_iter_350104.solverstate](https://drive.google.com/open?id=1adHTI0E3UPrz8BXRa4ecu70dCVim9pl1) |
  
  Train around **42 *mm***, test around **56 *mm***.
  
- **d2 = 64**
  - **Adaptive I1**
  ```
  cd ../../training/d2=64
  $CAFFE_ROOT/build/tools/caffe train --solver=solver_d64_ada_gn_startgn.prototxt --snapshot=net_iter_350104.solverstate
  ```
  
  | d2 | lr   |  "heatmap2" init std  | loss | Caffe Model  | Solver State |
  |:-:|:-:|:-:|:-:|:-:|:-:|
  | 32     | 2.5e-5 to 5e-6 after 460000 | 0.01   | Adaptive I1 | [net_iter_516722.caffemodel](https://drive.google.com/open?id=1DEHRDTBcK_7Sp33MHB2evmMzHqofTAW3) | [net_iter_516722.solverstate](https://drive.google.com/open?id=1HZwcDQoGcszNPBrwBUGnoEzRjJ7v89oC) |
  