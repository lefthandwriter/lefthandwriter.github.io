---
layout: post
title: Visual SLAM and Deep Learning in Complementary Forms
date: 2019-03-14
categories: vision
comments: true
---
*By Esther Ling*


#### **Introduction**

Given a robot (or a camera), determining the location of an object in a scene relative to the position of the camera in real-world measurements is a fairly challenging problem. It can be thought of as 3D localization or equivalently as 3D reconstruction coupled with an object detector. This problem is typically encountered where vision through a camera is imposed as a constraint. Some examples are: mobile robots that collect trolleys at supermarkets, pick-and-place robots at a warehouse and realistic object overlay in a phone augmented reality (AR) app.

A framework for attacking this problem would be to combine an object detection module (e.g. a pre-trained convolutional neural network) and geometrical computer vision theory such as single-view metrology or multiple-view geometry. In the single-view case, one could search for vanishing points, find collinear points and apply the cross-ratio, while in the multiple-view geometry case (focus of this post), one would search for point correspondences and do the reconstruction, culminating in the structure from motion (SfM) / visual odometry pipeline.

However, as researchers have studied the combined problem of object detection and visual odometry / SLAM, new ideas have emerged: what if the two could be used in tandem not only to solve the larger 3D localization problem, but *also to improve the results of each module* in symbiotic form?

Relatedly, given recent advances in deep learning not only for object detection, but also for other vision related tasks such as monocular depth estimation, other questions have been posed, for instance, can depth maps increase the accuracy of the reconstruction?

Here are a few papers that explore these ideas.


#### **Object Detection to Improve SLAM**

*[CubeSLAM: Monocular 3D Object Detection and SLAM without Prior Models](https://arxiv.org/pdf/1806.00557.pdf).* The authors for this paper propose an approach that fuses single-view 3D object detection and multiple-view SLAM. In SLAM / SfM, point correspondences are tracked between frames, and bundle-adjustment is run to minimize the re-projection or photometric error on a subset of frames. With this observation, they suggest that the tracking step could benefit not only from tracking points in the lowest-level sense, but also thinking about the points in the context of an object, i.e. points as composing higher-level features. They argue that the 3D object cuboids could provide geometric and semantic constraints that would improve bundle-adjustment. In particular, objects may contain depth cues that constrain the location of certain points.

The authors use ORB-SLAM as the base SLAM model, and modify the bundle-adjustment formulation to jointly optimize for camera poses, points *and* objects. In their experiments, they show that in a difficult dataset with large camera rotations, the cuboids help initialize the map where the original ORB-SLAM formulation fails. They also show that the geometrical constraints provided by the objects can reduce scale drift.


*[Detect-SLAM: Making Object Detection and SLAM Mutually Beneficial](https://ieeexplore.ieee.org/document/8354219)*. In the SLAM / SfM pipeline, estimation of the essential matrix and 3D reconstruction rely on accurate point correspondence matching. One source of error for wrongly matched points is moving objects.

In this paper, the authors use a convolutional neural network (single-shot detector) to detect moving objects belonging to a set of classes at key-frame rate. They assume that certain classes are more likely to be moving than others (such as people, animals and vehicles). Each feature point is assigned a probability of being non-stationary based on being in the region of detected objects, and this probability is propagated at frame-rate. Points above a certain threshold are excluded from the optimization of camera poses.

The approach is tested on seven high-dynamic sequences, two low-dynamic sequences and one static sequence in the experiment. One question however is how to handle scenes where objects from the same class are present in static and dynamic forms. For example, assigning the same probability to moving cars and parked cars simply because they belong to the same "car" class may be an overly aggressive removal approach. The overall idea is interesting nevertheless.


#### **SLAM to Improve Object Detection**
<!-- (e.g. [Faster R-CNN](https://arxiv.org/abs/1506.01497), [Fast R-CNN](https://arxiv.org/abs/1504.08083) and [Selective Search](https://ivi.fnwi.uva.nl/isis/publications/bibtexbrowser.php?key=UijlingsIJCV2013&bib=all.bib)) -->

*[Monocular SLAM Supported Object Recognition](https://arxiv.org/pdf/1506.01732.pdf)*. A challenge in object detection is in having good object proposals. This paper points out that mobile cameras have the advantage of observing the same object from multiple views, and hypothesize that the semi-dense representations through SLAM (such as ORB-SLAM and LSD-SLAM) may improve object proposals. In their approach, they use ORB-SLAM's reconstructed map to infer object locations, and aggregate object predictions across multiple views.


#### **Depth Prediction to Complement SLAM**

*[CNN-SLAM: Real-time dense monocular SLAM with learned depth prediction](https://arxiv.org/pdf/1704.03489.pdf)*. Recently, there have been studies on deep learning to infer depth from a single image. This paper postulates that such depth maps could complement monocular SLAM in several ways. For instance, depth maps (1) can be a point of reference under pure rotational motions, (2) have been shown to perform well in texture-less regions, thus making the tracking step in SLAM more robust under these conditions, and (3) can assist with recovering the absolute scale of monocular SLAM.

For (3), the authors observe that one challenge is that if the depth prediction network has been trained on a set of images from a camera with different intrinsic parameters to the one used in SLAM, then the resulting scale of the 3D reconstruction will be inaccurate. They propose to weight the depth map produced by the CNN using the ratio of the focal lengths of the two cameras.

While depth map prediction for recovering absolute scale is an interesting idea, reliance on an actual sensor such as an inertial-measurement unit (IMU) or GPS may be a more robust solution.


#### **Conclusion**

Modules that were previously in isolation may work better if the right ones are integrated together. With separate thrusts of research on deep learning and geometrical computer vision, I think that in the coming years, finding the right components to be fused together will be one source of breakthroughs in the field.

{% include disqus.html %}
