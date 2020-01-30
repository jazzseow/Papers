
# [Paper](http://openaccess.thecvf.com/content_CVPR_2019/papers/Cui_Class-Balanced_Loss_Based_on_Effective_Number_of_Samples_CVPR_2019_paper.pdf) [[code](https://github.com/richardaecn/class-balanced-loss)]
**Title**   :   Class-Balanced Loss Based on Effective Number of Samples

**Author**  : Yin Cui<sup>1,2</sup>, Menglin Jia<sup>1</sup>, Tsung-Yi Lin<sup>3</sup>, Yang Song<sup>4</sup>, Serge Belongie<sup>1,2</sup>

**From**   :   <sup>1</sup>Cornell University, <sup>2</sup>Cornell Tech, <sup>3</sup>Google Brain, <sup>4</sup>Alphabet Inc

**Year**  :   2019



# Details
## Summary
|![fig_01](Images/Class-Balanced_Loss_Based_on_Effective_Number_of_Samples/fig_01.png)|
|:--:| 
| *Fig. 1: Two classes, one from the head and one from the tail ofa long-tailed dataset (iNaturalist 2017 [41] in this example), havedrastically different number of samples. Models trained on thesesamples are biased toward dominant classes (black solid line). Re-weighing the loss by inverse class frequency usually yields poorperformance (red dashed line) on real-world data with high classimbalance. We propose a theoretical framework to quantify theeffective number of samples by taking data overlap into consider-ation. A class-balanced term is designed to re-weight the loss byinverse effective number of samples. We show in experiments thatthe performance of a model can be improved when trained withthe proposed class-balanced loss (blue dashed line)* |
* Re-weighing the loss by inverse class frequency is not the optimal way as the feature maps from different classes might overlap each other
* Propose re-weighing the loss by using the effective number of samples
* Effective number of samples can be imagined as the actual volume that will be covered by *n* samples where the total volume *N* is represented by total samples

##  Effective Number of Samples 
* Given a class, denote the set of all possible data in thefeature space of this class as *S*. We assume the volume of *S* is *N* and *N* ≥ 1. Denote each sample as a subset of *S* that has the unit volume of 1 and may overlap with other samples
* (Effective Number) *E<sub>n</sub> = (1 - β<sup>𝑛</sup>) / (1 - β)*, where *β = (N - 1) / N*
* (Asymptotic Properties) *E<sub>n</sub> = 1 if β = 0 (N = 1); E<sub>n</sub> ⟶ n if β ⟶ 1 (N ⟶ ∞)*
    * The asymptotic property ofEnshows that when *N* islarge, the effective number of samples is same as the number of samples *n*. In this scenario, we think the numberof unique prototypes *N* is large, thus there is no data overlap and every sample is unique
    * If *N* = 1, this means that we believe there exist a single prototype so that all the data in this class can be represented by this prototype via data augmentation, transformations,etc

##  Class Balance Loss
* JCD feature is location viewpoint invariant, but it does not contain global motion information (Fig.1 (c))
* Idea is inspired by [SlowFast](https://arxiv.org/pdf/1812.03982.pdf)
* Two-scale motions can be generated by the following equation: <img src="Images/DD_Net/formula_02.PNG" height="70px">
    * where *M* denotes the slow motion and fast motion at frame *k* respectively
    * *S<sup>k+1</sup>* and *S<sup>k+2</sup>* are behind *S<sup>k</sup>* for one frame and two frames respectively
* Corresponding to *S<sup>[1,...,K]</sup>*, we have *M<sup>[1,...,K−1]</sup>* slow and *M<sup>[1,...,K/2−1]</sup>* fast
* Flatten to 1D vector
* To match JCD feature, perform linear interpolation to resize *M<sup>[1,...,K−1]</sup>* slow and *M<sup>[1,...,K/2−1]</sup>* fast to *M<sup>[1,...,K]</sup>* slow and *M<sup>[1,...,K/2]</sup>* fast

##  Modeling Joint Correlations by an Embedding
* The correlation of joints is automatically learned through the embedding as depicted in figure 2
* As another beneﬁt, the embedding process also reduces the effect of skeleton noise

## Experiments
* Train and test on 2 datasets:
    * [SHREC17](https://shapenet.cs.stanford.edu/shrec17/)
    * [JHMDB](http://jhmdb.is.tue.mpg.de/)

|![table_01](Images/DD_Net/table_01.PNG)|
|:--:| 
| *Table I: Properties of experimental datasets* |

## Training Details
* Adam (*β*<sub>1</sub> = 0.9, *β*<sub>2</sub> = 0.999)
* Annealing learning rate that drops from 1e<sup>-3</sup> to 1e<sup>−5</sup>

## SHREC17
|![table_02](Images/DD_Net/table_02.PNG)|
|:--:| 
| *TABLE II: Results on SHREC (Using 3D skeletons only)* |

## JHMDB
|![table_03](Images/DD_Net/table_03.PNG)|
|:--:| 
| *TABLE III: Results on JHMDB (Using 2D skeletons only)* |