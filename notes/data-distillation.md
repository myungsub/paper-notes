# Data Distillation: Towards Omni-Supervised Learning
### Ilija Radosavovic, Piotr Dollar, Ross Girshick, Georgia Gkioxari and Kaiming He 
#### Facebook AI Research (FAIR)
#### arXiv:1712.04440

### Outline
This paper borrows the inspiration from the famous knowledge distillation paper by Geoffrey Hinton [[link](https://arxiv.org/abs/1503.02531)]. Instead of distilling knowledge from **models** by using soft targets to train a student model, the authors propose to utilize additional **unlabeled data** with simulated labels for training, where they coined the term **omni-supervised learning**. The authors argue that recent visual recognition models are accurate enough to be self-trained based on unlabeled data. By making use of this additional data, their model achieved higher performance on COCO dataset compared to a baseline model which was trained only on labeled data.

### Approach
![teaser](img/data-distillation/fig1.jpg)

**Model distillation** uses predictions from multiple trained models, obtains a soft target from ensembled predictions and uses this as a label to train the student model. **Data distillation** uses a single trained model while it obtains multiple predictions from multiple *transformations* of single (unlabeled) input. Predictions are ensembled to train the student model. 

Data distillation involves 4 steps- (1) Training a model with labeled data (normal supervised learning); (2) Applying trained model on multiple transformations of unlabeled data; (3) Obtain ensembled predictions; (4) Retrain a model using labeled data and auto-labled data.

To generate labels for unlabeled data, the authors use multiple transformations (scaling and horizontal flipping) of an input image. To ensemble the predictions, they used simple average of the output probability heatmap for keypoint detection task, and bounding box voting for object detection task.

### Experiments
For keypoint detection (pose) task, they used 3 datasets - (1) COCO labeled images (co-115), (2) COCO unlabled images (un-120) and (3) Sports-1M frames (s1m-180). They achieved 1.7-2.0 points of AP improvement on "Large-scale, similar-distribution data (datasets 1,2)", and achieved 1.2-1.5 points of AP improvement on "Large-scale, dissimilar-distribution data (datasets 1,3)". 

For object detection task, they used data splits of COCO dataset. For large-scale data experiment where they treated co-115 as labeled and un-120 as unlabeled, they achieved 0.8-0.9 points of AP improvement.
