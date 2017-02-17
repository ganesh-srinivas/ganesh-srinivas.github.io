---
layout: post
title: "Interesting Papers Roundup - Week 7 of 2017"
date: 2017-02-18
---
## 1. System Problem Detection by Mining Console Logs 
Xu, Wei. **"[System Problem Detection by Mining Console Logs](http://digitalassets.lib.berkeley.edu/etd/ucb/text/Xu_berkeley_0028E_10769.pdf)"**. PhD Dissertation. UC Berkeley. 2010.

Console logs contain large amounts of free text. An important insight is that system source code is a schema for the console log text. The author extract features from system state variables and message identifiers (which were extracted by parsing the text logs with help from program code). Principal Component Analysis is used to learn the normal pattern (the first few principal components capture capture much of the variance in the data). Any system event far away from this normal pattern is flagged as an anomaly. I've provided images of the entire pipeline and an intuition for how PCA detects anomalies.
<img alt="Image: 4-step console log analysis methodology" src="/assets/console-mining/methodology.jpg" width="600">
<img alt="Image: PCA intuition" src="/assets/console-mining/pca-detection-intuition.png" width="600">

## 2. FaceNet: learning embeddings for faces using deep convnets trained with triplet loss
Schroff, Florian, Dmitry Kalenichenko, and James Philbin. **"[Facenet: A unified embedding for face recognition and clustering](https://arxiv.org/abs/1503.03832)."** Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2015.

Face verification (is this the face of X?), face recognition and face clustering systems need to be scalable. A deep convolutional neural network learns an embedding for faces i.e., a mapping from face images to a Euclidean space where distances correspond to a measure of face similarity. How do they learn this embedding? Triplet loss during training: a function which minimizes the distance between an anchor and a positive, both of which have the same identity, and maximizes the distance between the anchor and a negative (of a different identity). Without embeddings, I think the only way to

I was quite excited when I came across this paper. I did not know of this triplet loss technique to learn embeddings. I only knew how to output one-hot encoding vectors (class labels) as outputs. Embeddings are fascinating (<a href="https://blog.acolyer.org/2016/04/21/the-amazing-power-of-word-vectors/">word2vec</a> word embeddings learn interesting semantic and syntactic relationships). Face embeddings could be used to study so many things! I have always found it a source of inexhaustible amusement in trying to mentally group people by their facial features. Another attractive thing about learning embeddings is that dimension reduction techniques like PCA or t-SNE can be used to visualize those high-dimensional embeddings in 2D or 3D.

<img alt="Image: Face embedding model architecture" src="/assets/triplet-loss/model-structure.jpg" width="600">
<img alt="Image: Triplet loss" src="/assets/triplet-loss/triplet-loss.jpg" width="600">
