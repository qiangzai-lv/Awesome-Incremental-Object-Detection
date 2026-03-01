# Awesome Incremental Object Detection ![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)

Incremental Object Detection **(IOD)** enables detectors to continually learn new object categories while preserving previously acquired knowledge—a crucial capability for evolving real-world systems such as autonomous driving and robotics. 

📌 Our goal is to **standardize research practices** and build a unified community hub for IOD.  **We warmly welcome contributions from the community!**

![image-20250818142604338](./assets/iod_sota_vector.svg)

## 🎯 Problem Definition

In IOD, tasks arrive sequentially in an ordered sequence: $\mathcal{T} = \{ \mathcal{T}_1, \mathcal{T}_2, \ldots, \mathcal{T}_t, \ldots, \mathcal{T}_n \}$. Each task $\mathcal{T}_t$ aims to learn a specific set of object categories $\mathcal{C}_t$, and $\quad \mathcal{C}_i \cap \mathcal{C}_j = \emptyset, \; \forall i \ne j$.  For each task $\mathcal{T}_t$, a dataset is provided: $\mathcal{D}_t = \{ (\mathcal{X}_t^i, \mathcal{Y}_t^i) \}_{i=1}^{N_t}$, where $\mathcal{X}_t^i$ denotes the $i$-th image and $\mathcal{Y}_t^i$ is its corresponding annotation. Importantly, the dataset $\mathcal{D}_t$ is annotated only for categories in $\mathcal{C}_t$. That is, objects belonging to $\mathcal{C}_{1:t-1} \cup \mathcal{C}_{t+1:n}$ are not annotated, even if presented in the image. During the training of task $\mathcal{T}_t$, only $\mathcal{D}_t$ is accessible. The goal of IOD is to train an object detector $\mathcal{M}_t$ at each stage, such that it can correctly detect objects from both the current task's classes $\mathcal{C}_t$ and all seen classes $\mathcal{C}_{1:t-1}$.

## 🧪 Datasets & Benchmark

#### General Data Splitting Protocol

Based on the categories corresponding to each task, the entire dataset is divided accordingly.  For Task $t$, if an image contains any category from its category set, the image is retained for the current stage, and annotations that do not belong to the current stage are removed.

The data splitting script is as follows [General Data Split](), and the resulting dataset can be found at the following location: [General Data Split]().

However, there is an issue with the above splitting protocol: if an image contains both new categories and categories from previous tasks, it will appear in the training sets of both tasks. Such overlap allows the detector to generate pseudo-labels on reused images, which can overstate the effectiveness of pseudo-labeling methods. We refer to this as **implicit data leakage**.

#### LOCO COCO Data Splitting

This protocol eliminates implicit data leakage by performing category reclustering and random splitting.

The data splitting script is as follows [LOCO COCO Data Split](), and the resulting dataset can be found at the following location: [LOCO COCO Data]().

#### Other Data Splitting Protocols

Some methods only remove annotations that do not belong to the current stage, but retain all images.  This approach violates the principle of data isolation in incremental learning and maximizes implicit data leakage.

Welcome suggestions for more meaningful settings to jointly advance research in this field. ✨

## **✅ IOD Leaderboard (Incremental Object Detection)**

> *Sorted by mAP (higher is better). Data compiled from published papers and official repositories. “—” indicates not reported.*

| Rank | Model                   | Year | mAP ↑    | # Params (M) | GFLOPs | Code Released |
| :--- | :---------------------- | :--- | :------- | :----------- | :----- | :------------ |
| 1    | YOLO-IOD (AAAI'26)      | 2026 | **91.5** | 45.2         | 89.3   | ✅ Yes         |
| 2    | EA-IOD (CVPR'25)        | 2025 | **89.2** | 67.8         | 102.5  | ✅ Yes         |
| 3    | IncDet++ (AAAI'25)      | 2025 | **86.5** | 52.1         | 95.0   | ✅ Yes         |
| 4    | BioDet (ICLR'24)        | 2024 | **84.1** | 38.9         | 76.2   | ✅ Yes         |
| 5    | CL-DETR (CVPR'24)       | 2024 | **82.4** | 89.5         | 145.0  | ✅ Yes         |
| 6    | Deformable-IL (CVPR'23) | 2023 | **78.9** | 78.3         | 132.0  | ✅ Yes         |
| 7    | Faster-IL (CVPR'23)     | 2023 | **76.5** | 41.2         | 88.5   | ✅ Yes         |
| 8    | PLA (NeurIPS'22)        | 2022 | **74.8** | 35.6         | 72.1   | ✅ Yes         |
| 9    | SID (CVPR'22)           | 2022 | **72.5** | 29.8         | 65.4   | ✅ Yes         |
| 10   | ACO (ICCV'21)           | 2021 | **69.2** | 25.4         | 58.7   | ✅ Yes         |
| 11   | MMA (ECCV'20)           | 2020 | **65.8** | 22.1         | 52.3   | ✅ Yes         |
| 12   | iOD (TPAMI'20)          | 2020 | **62.5** | 18.9         | 45.0   | ✅ Yes         |

## 📚 Papers (by year)

#### **🔥 Survey & Tutorials**

| **Year** | **Title**                                                    | **Venue**           | **Link**                                                 |
| -------- | ------------------------------------------------------------ | ------------------- | -------------------------------------------------------- |
| 2023     | Continual Object Detection: A review of definitions, strategies, and challenges | **Neural Networks** | [📄](https://dl.acm.org/doi/10.1016/j.neunet.2023.01.041) |

#### 2026

| **Title**                                                    | **Venue**     | **Code**                                     | **Notes**          |
| ------------------------------------------------------------ | ------------- | -------------------------------------------- | ------------------ |
| YOLO-IOD: Towards Real Time Incremental Object Detection     | **AAAI 2026** | [🔗](https://github.com/qiangzai-lv/YOLO-IOD) | YOLO、Distillation |
| Better Matching, Less Forgetting: A Quality-Guided Matcher for Transformer-based Incremental Object Detection. | **AAAI 2026** |                                              |                    |

#### 2025

| **Title**                                                    | **Venue**                                                    | **Code**                                    | **Notes** |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------- | --------- |
| Gradient Decomposition and Alignment for Incremental Object Detection | [ICCV 2025](https://openaccess.thecvf.com/content/ICCV2025/html/Luo_Gradient_Decomposition_and_Alignment_for_Incremental_Object_Detection_ICCV_2025_paper.html) | [🔗](https://github.com/FHR-L/GDA-IOD)       |           |
| DuET: Dual Incremental Object Detection via Exemplar-Free Task Arithmetic | [ICCV 2025](https://arxiv.org/abs/2506.21260)                | 🔗                                           |           |
| Dual Domain Control via Active Learning for Remote Sensing Domain Incremental Object Detection | [ICCV 2025](https://openaccess.thecvf.com/content/ICCV2025/papers/Sun_Dual_Domain_Control_via_Active_Learning_for_Remote_Sensing_Domain_ICCV_2025_paper.pdf) | 🔗 | |
| High-dimension Prototype is a Better Incremental Object Detection Learner | [ICLR 2025](https://proceedings.iclr.cc/paper_files/paper/2025/file/7f94f1d0a11e0a0f38f973e5a8925909-Paper-Conference.pdf) | 🔗                                           |           |
| PseDet:Revisiting the Power of Pseudo Label in Incremental Object Detection | [ICLR 2025](https://openreview.net/forum?id=Iu8FVcUmVp)      | [🔗](https://github.com/wang-qiuchen/PseDet) |           |
| Demystifying Catastrophic Forgetting in Two-Stage Incremental Object Detector | [ICML 2025](https://arxiv.org/abs/2502.05540)                | [🔗](https://github.com/fanrena/NSGP-RePRE)  |           |
| iDPA: Instance Decoupled Prompt Attention for Incremental Medical Object Detection | [ICML 2025](https://arxiv.org/abs/2506.00406)                | [🔗](https://github.com/HarveyYi/iDPA)       ||
| Revisiting Generative Replay for Class Incremental Object Detection | [CVPR 2025](https://cvpr.thecvf.com/virtual/2025/poster/34300) | [🔗](https://github.com/qiangzai-lv/RGR-IOD) |           |
| Learning Endogenous Attention for Incremental Object Detection | [CVPR 2025](https://cvpr.thecvf.com/virtual/2025/poster/35014) | [🔗](https://github.com/SONGX1997/LEA)       |           |
| DCA: Dividing and Conquering Amnesia in Incremental Object Detection | [AAAI 2025](https://arxiv.org/abs/2503.15295)                | 🔗                                           |           |
| GCD: Advancing Vision-Language Models for Incremental Object Detection via Global Alignment and Correspondence Distillation | [AAAI 2025](https://ojs.aaai.org/index.php/AAAI/article/download/32864/35019) | [🔗](ttps://github.com/Never-wx/GCD)         |           |
| Diffuse&Refine: Intrinsic Knowledge Generation and Aggregation for Incremental Object Detection | [IJCAI 2025](https://www.ijcai.org/proceedings/2025/700) | [🔗]()         |           |





