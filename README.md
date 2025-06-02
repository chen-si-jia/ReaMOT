# 🚀 ReaMOT: A Benchmark and Framework for Reasoning-based Multi-Object Tracking

> [**ReaMOT: A Benchmark and Framework for Reasoning-based Multi-Object Tracking**](https://arxiv.org/abs/2505.20381)              
> Sijia Chen *, Yanqiu Yu *, En Yu *, Wenbing Tao   
> Huazhong University of Science and Technology                       
> *[ArXiv] Paper ([https://arxiv.org/abs/2505.20381](https://arxiv.org/abs/2505.20381))*

**Note:** We will fully open-source our **ReaMOT Challenge benchmark** (including its dataset and evaluation metrics code) and **ReaTrack framework** (including its code and model weights) **after the paper is accepted**, just like our [**CRMOT**](https://github.com/chen-si-jia/CRMOT)  project.


Thanks for your attention! If you are interested in our work, please give us a star ⭐️.


## 🔍 ReaMOT vs RMOT

![](asset/ReaMOT.jpg)

As shown in the above Figure (a), for the language instruction "The cars on the right.", the models of the RMOT task only need to track the cars on the right, as referred to by the language instruction, without going through a series of complex reasoning processes. 

**In contrast**, as shown in the above Figure (b), for the language instruction "The players of that team with clear tactics and high organization.", the ReaMOT task requires the models to engage in a deep reasoning process, analyzing aspects such as offensive strategies, tactical execution, defensive positioning, and reaction speed of both teams, to accurately deduce the players of the target team that match the language instruction and track their trajectories.


## ✨ Abstract
Referring Multi-object tracking (RMOT) is an important research field in computer vision. Its task form is to guide the models to track the objects that conform to the language instruction. However, the RMOT task commonly requires clear language instructions, such methods often fail to work when complex language instructions with reasoning characteristics appear. 

In this work, we propose a new task, called **Rea**soning-based **M**ulti-**O**bject **T**racking (**ReaMOT**). ReaMOT is a more challenging task that requires accurate reasoning about objects that match the language instruction with reasoning characteristic and tracking the objects' trajectories. 

To advance the ReaMOT task and evaluate the reasoning capabilities of tracking models, we construct **ReaMOT Challenge**, a reasoning-based multi-object tracking benchmark built upon 12 datasets. Specifically, it comprises 1,156 language instructions with reasoning characteristic, 423,359 image-language pairs, and 869 diverse scenes, which is divided into three levels of reasoning difficulty. 

In addition, we propose a set of evaluation metrics tailored for the ReaMOT task. Furthermore, we propose **ReaTrack**, a training-free framework for reasoning-based multi-object tracking based on large vision-language models (LVLM) and SAM2, as a baseline for the ReaMOT task. Extensive experiments on the ReaMOT Challenge benchmark demonstrate the effectiveness of our ReaTrack framework.


## ⚡️ Pipeline of ReaTrack

![](asset/pipeline.jpg)


## 😮 Experimental Results
### Table: Performance of many methods on the test set of the ReaMOT Challenge benchmark under zero-shot conditions. ↑ indicates that higher score is better. The best results are marked in **bold**.

| Method              | Published     | Easy RIDF1↑   | Easy RMOTA↑    | Easy RRcll↑    | Easy RPrcn↑    | Medium RIDF1↑  | Medium RMOTA↑  | Medium RRcll↑  | Medium RPrcn↑  | Hard RIDF1↑      | Hard RMOTA↑      | Hard RRcll↑      | Hard RPrcn↑      |
|---------------------|---------------|---------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|------------------|------------------|------------------|------------------|
| TransRMOT[1]        | CVPR2023      | 3.08          | 1.28           | 2.89           | 11.08          | 2.55           | 0.70           | 2.18           | 12.19          | 1.55             | 0.09             | 1.67             | 8.27             |
| TempRMOT[2]         | ArXiv2024     | 5.20          | 2.17           | 4.56           | 15.22          | 4.75           | 2.01           | 3.94           | 15.57          | 2.13             | 0.76             | 1.72             | 8.43             |
| **ReaTrack(Ours)** | -             | **40.18**     | **13.45**      | **60.18**      | **37.36**      | **39.63**      | **14.24**      | **58.11**      | **37.50**      | **39.63**        | **13.29**        | **57.02**        | **36.30**        |


### Table: Ablation study results of our ReaTrack framework on the test set of the ReaMOT Challenge benchmark under zero-shot conditions. ↑ indicates that higher score is better.

| LVLM Name             | LVLM Size | Online SAM2 | Easy RIDF1↑ | Easy RMOTA↑ | Easy RRcll↑ | Easy RPrcn↑ | Medium RIDF1↑ | Medium RMOTA↑ | Medium RRcll↑ | Medium RPrcn↑ | Hard RIDF1↑ | Hard RMOTA↑ | Hard RRcll↑ | Hard RPrcn↑ |
|----------------------|-----------|---------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|------------------|------------------|------------------|------------------|
| LLaVA-1.5 [3]        | 7B        | ✓             | 6.13           | 0.43           | 17.01          | 5.56           | 6.68           | 0.69           | 17.07          | 5.89           | 5.24             | 0.31             | 16.39            | 4.84             |
| InternVL2.5 [4]      | 8B        | ✓             | 10.80          | 1.79           | 35.20          | 8.99           | 9.91           | 1.09           | 32.24          | 7.79           | 9.64             | 2.36             | 27.65            | 8.41             |
| LLaVA-NEXT [5]       | 8B        | ✓             | 25.90          | 5.76           | 40.60          | 24.18          | 23.88          | 5.60           | 32.14          | 23.93          | 24.17            | 7.72             | 30.68            | 26.01            |
| Qwen-VL-Chat [6]     | 7B        | ✗             | 13.11          | 6.71           | 13.25          | 30.70          | 10.63          | 5.04           | 10.13          | 25.17          | 14.70            | 6.07             | 14.75            | **29.61**         |
| Qwen-VL-Chat [6]     | 7B        | ✓             | **22.34**      | **8.88**       | **25.42**      | **28.17**      | **21.52**      | **7.12**       | **25.51**      | **26.63**      | **23.22**        | **7.89**         | **28.07**        | 25.85            |
| Qwen2.5-VL [7]       | 7B        | ✗             | **46.59**      | **30.42**      | 51.46          | **60.42**      | 37.90          | **21.67**      | 40.21          | **53.78**      | 37.33            | **20.49**        | 39.62            | **53.51**        |
| Qwen2.5-VL [7]       | 7B        | ✓             | 40.18          | 13.45          | **60.18**      | 37.36          | **39.63**      | 14.24          | **58.11**      | 37.50          | **39.63**        | 13.29            | **57.02**        | 36.30            |


References:

[1] Dongming Wu, Wencheng Han, Tiancai Wang, Xingping Dong, Xiangyu Zhang, Jianbing Shen. Referring multi-object tracking[C]//Proceedings of the IEEE/CVF conference on computer vision and pattern recognition. 2023: 14633-14642.

[2] Yani Zhang, Dongming Wu, Wencheng Han, Xingping Dong. Bootstrapping Referring Multi-Object Tracking[J]. arXiv preprint arXiv:2406.05039, 2024.

[3] Haotian Liu, Chunyuan Li, Qingyang Wu, Yong Jae Lee. Visual instruction tuning[J]. Advances in neural information processing systems, 2023, 36: 34892-34916.

[4] Zhe Chen, Jiannan Wu, Wenhai Wang, Weijie Su, Guo Chen, Sen Xing, Muyan Zhong, Qinglong Zhang, Xizhou Zhu, Lewei Lu, Bin Li, Ping Luo, Tong Lu, Yu Qiao, Jifeng Dai. Internvl: Scaling up vision foundation models and aligning for generic visual-linguistic tasks[C]//Proceedings of the IEEE/CVF conference on computer vision and pattern recognition. 2024: 24185-24198.

[5] Haotian Liu, Chunyuan Li, Yuheng Li, Bo Li, Yuanhan Zhang, Sheng Shen, Yong Jae Lee. LLaVA-NeXT: Improved reasoning, OCR, and world knowledge[J]. https://llava-vl.github.io/blog/2024-01-30-llava-next/. 2024.

[6] Jinze Bai, Shuai Bai, Shusheng Yang, Shijie Wang, Sinan Tan, Peng Wang, Junyang Lin, Chang Zhou, Jingren Zhou. Qwen-VL: A Versatile Vision-Language Model for Understanding, Localization, Text Reading, and Beyond.[J] arXiv preprint arXiv:2308.12966. 2023.

[7] Shuai Bai, Keqin Chen, Xuejing Liu, Jialin Wang, Wenbin Ge, Sibo Song, Kai Dang, Peng Wang, Shijie Wang, Jun Tang, Humen Zhong, Yuanzhi Zhu, Mingkun Yang, Zhaohai Li, Jianqiang Wan, Pengfei Wang, Wei Ding, Zheren Fu, Yiheng Xu, Jiabo Ye, Xi Zhang, Tianbao Xie, Zesen Cheng, Hang Zhang, Zhibo Yang, Haiyang Xu, Junyang Lin and others. Qwen2. 5-vl technical report[J]. arXiv preprint arXiv:2502.13923. 2025.


## ✏️ Citation
```
@article{chen2025reamot,
  title={ReaMOT: A Benchmark and Framework for Reasoning-based Multi-Object Tracking},
  author={Chen, Sijia and Yu, Yanqiu and Yu, En and Tao, Wenbing},
  journal={arXiv preprint arXiv:2505.20381},
  year={2025}
}
```
