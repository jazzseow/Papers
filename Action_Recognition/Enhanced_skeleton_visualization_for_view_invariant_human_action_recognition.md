
# [Paper](https://webpages.uncc.edu/cchen62/PR_2017.pdf)
**Title**   :  Enhanced Skeleton Visualization for View Invariant human action recognition  

**Author**  : Mengyuan Liu, Hong Liu, Chen Chen

**From**   :   Key Laboratory of Machine Perception, Shenzhen Graduate School, Peking University, Beijing 100871, China    
&emsp;&emsp;&emsp;&nbsp;Center for Research in Computer Vision, University of Central Florida, Orlando, FL 32816, USA 

**Year**  :   2016  

**Journal** : Pattern Recognition 2017  

# Details
## Summary
|![Block diagram of the proposed architecture](Images/Enhanced_skeleton_visualization_for_view_invariant_human_action_recognition/Method_pipeline.png)|
|:--:| 
| *Pipeline of the method* |
* Sequence-based transform is applied on a skeleton sequence to make the transformed
  sequence invariant to the absolute body position and the initial body orientation
    * To eliminate the effect of noise on skeletons, we jointly use all torso joints
      from the sequence to formulate the transform matrix
* Transformed sequence is visualized as a series of color images which encode both
  spatial and temporal distributions of the skeleton joints
    * Skeleton joints are represented in 5D space [x, y, z, time_label, joint label]
    * 2 elements are used to construct the line, 3 elements are used for colours
* To enhance the local patterns of color images, we apply the mathematical
  morphology method to highlight the colored pixels
* To make color images more sensitive to motions, we develop a weighting scheme to 
  emphasize skeleton joints with salient motions

### Main Contributions
* Sequence-based view invariant transform
* Enchanced skeleton visualization method
* Weighted fusion method for multi-stream CNN fusion model

## Sequence-based View Invariant Transform