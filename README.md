# 3dhuman-groupnorm
What happens when you have to **scrupulously share** GPUs with **others in the lab** and you need to run several, say **6 programs on a single 12GB TITAN card in one day**? What happens when you are impecunious as I am with only a **single 8GB 1070 card**? 

I give you this repo implementing **group normalization** version of **3d human pose heatmap** with **batch size = 1**.

*Under construction* Only matches the performance of **H1** (heatmap loss only) as of now. Probably working on **I1** (heatmap + integral loss). 