# [Intervertebral Disc Labeling With Learning Shape Information, A Look Once Approach](https://arxiv.org/abs/2204.02943v1)

Labeling vertebral discs from MRI scans is crucial for the proper assessment of spine-related diseases. Challenges such as complex background of MRI images, the similarity between discs and bone area to name a few, usually exacerbates the notorious problem in segmentation of vertebral discs. To overcome this
issue, we propose to incorporate shape information within the learning process. Moreover, as labelling anatomical structures such as intervertebral discs and usually produces both false positive (FP) and false negative (FN) detections, we propose a look-once approach for the post-processing step in the intervertebral disc labeling procedure.

If this code helps with your research please consider citing the following paper:
</br>
> [R. Azad](https://scholar.google.com/citations?hl=en&user=Qb5ildMAAAAJ&view_op=list_works&sortby=pubdate), [Moein Heidari](https://scholar.google.com/citations?user=mir8D5UAAAAJ&hl=en&oi=sra), [Ehsan Adeli](https://scholar.google.com/citations?user=7NX_J_cAAAAJ&hl=en), [Julien Cohen-Adad](https://scholar.google.com/citations?user=6cAZ028AAAAJ) and [Dorit Merhof
](https://scholar.google.com/citations?user=JH5HObAAAAAJ&sortby=pubdate), "Intervertebral Disc Labeling With Learning Shape Information, A Look Once Approach", download [link](https://arxiv.org/abs/2204.02943v1).



#### Please consider starring us, if you found it useful. Thanks

## Updates
- April 7, 2022: First release (Complete implemenation for [Spine Generic Dataset](https://www.nature.com/articles/s41597-021-00941-8) added)

### Prerequisties and Run

This code has been implemented in python language using Pytorch libarary and tested in ubuntu, though should be compatible with related environment. The required libraries are included in the `requiremetns.txt` file. Please follow the bellow steps to train and evaluate the model.

1- Download the [Spine Generic Public Database (Multi-Subject)](https://www.nature.com/articles/s41597-021-00941-8).

2- Run the `create_dataset.py` to gather the required data from the Spin Generic dataset.

3- Run `prepare_trainset.py` to creat the training and validation samples.

Notice: To avoid the above steps we have provided the processed data for all train, validation and test sets [here](https://drive.google.com/file/d/1z_mcIEoT_doyh_Hl53OaYWyplUel_-RT/view?usp=sharing) 

(should be around 150 MB) you can simply download it and continue with the rest steps. Please unzip the file in the `prepared_data` folder.

4- Run the `main.py` to train and evaluate the model. It only takes couple of hours to train with 5GB GPU memory. Use the following command with the related arguments to perform the required action:

A- Train and evaluate the model `python src/main.py`. You can use `--att true` to use the attention mechanisim.

B- Evaluate the model `python src/main.py --evaluate true` it will load the trained model and evalute it on the validation set.

C- You can run `make_res_gif.py` to creat a prediction video using the prediction images generated by `main.py` for the validation set.

D- You can change the number of stacked hourglass by `--stacks` argument. For more details check the arguments section in `main.py`.


5- Run the `test.py` to evaluate the model on the test set alongside with the metrics.





## Quick Overview
![Diagram of the proposed method](https://github.com/rezazad68/intervertebral-lookonce/blob/main/Images/fig1-1.png)

## Detailed structure of the proposed shape attention mechanism.
![Diagram of the proposed method](https://github.com/rezazad68/intervertebral-lookonce/blob/main/Images/fig4-1.png)

## Perceptual visualization of the proposed post-processing approach to eliminate the rate of FP / FN detections.
![Diagram of the proposed method](https://github.com/rezazad68/intervertebral-lookonce/blob/main/Images/fig2-1.png)


## Results
Our analysis was based on the publicly available [Spine Generic Dataset](https://www.nature.com/articles/s41597-021-00941-8). In bellow, results of the proposed approach illustrated.
</br>
## Table 1 : Intervertebral disc labeling results on the spine generic public dataset (T1 Modality). Note that DTT indicates Distance to target

Methods  |DTT (mm) | FNR (%)| FPR (%)
------------ | -------------|----|-----------------
Ullmann et. all [Template Matching](https://pubmed.ncbi.nlm.nih.gov/25132843/)       |1.97(±4.08)	  |8.1  |2.53
Rouhier et. all [Countception](https://openreview.net/pdf?id=ZxjnohXHCV)   |**1.03(±2.81)** |4.24     |0.9
Azad et. all [Pose Estimation](https://arxiv.org/abs/2108.06554)   |1.32(±1.33)	  |**0.32**      |**0.0**
Baseline [Proposed](https://github.com/rezazad68/TMUnet/edit/main/README.md)   |1.45(±2.70)  |7.3    |1.2	
Azad et. all [Proposed](https://github.com/rezazad68/TMUnet/edit/main/README.md)	  |1.2(±1.90) 	| 0.7	|**0.0**

## Table 2 : Intervertebral disc labeling results on the spine generic public dataset (T2 Modality). Note that DTT indicates Distance to target


Methods  |DTT (mm) | FNR (%)| FPR (%)
------------ | -------------|----|-----------------
Ullmann et. all [Template Matching](https://pubmed.ncbi.nlm.nih.gov/25132843/)       |2.05(±3.21)	  |11.1  |2.11
Rouhier et. all [Countception](https://openreview.net/pdf?id=ZxjnohXHCV)   |1.78(±2.64) |3.88    |1.5
Azad et. all [Pose Estimation](https://arxiv.org/abs/2108.06554)   |1.31(±2.79)	  |1.2      |0.6
Baseline [Proposed](https://github.com/rezazad68/TMUnet/edit/main/README.md)   |1.80(±2.80)  |5.4    |1.8	
Azad et. all [Proposed](https://github.com/rezazad68/TMUnet/edit/main/README.md)	  |**1.28(±2.61)** 	| **0.9**	|**0.0**

#### Intervertebral Disc Labeling result on test data

![Intervertebral Disc Labeling result](https://github.com/rezazad68/intervertebral-lookonce/blob/main/Images/fig3-1.png)
(a): Intervertebral labeling results of three representative T2 images. upper row: ground truth, lower row: predictions. (b): Before (left) and after (right) applying look-once approach on the T1 generated noisy prediction.


## Results of the proposed post-processing approach

#### Table 3 : Performance comparison of the proposed post-processing approach vs the SOTA approach
for eliminating FP detection.

Methods  |F1 | Accuracy| Specificity | Sensitivity | AUC
------------ | -------------|----|----------------- |----------------- |-----------------
Rouhier et. all [Condition based](https://openreview.net/pdf?id=ZxjnohXHCV)   |0.850 |0.881    |0.891 |0.902 |0.890
Azad et. all [Search tree](https://arxiv.org/abs/2108.06554)   |0.902	  |0.921      |0.925 |0.914 |0.920
Proposed [without geometrical relationship module](https://github.com/rezazad68/TMUnet/edit/main/README.md)   |0.914  |0.932    |0.941	|0.917 |0.9292
Proposed [Only look once](https://github.com/rezazad68/TMUnet/edit/main/README.md)	  |**0.942** 	| **0.958**	|**0.967** |**0.942** |**0.955**



#### Comparing inference time of the proposed method vs the search-tree based approach

![Inference time of post-processing approaches comparison](https://github.com/rezazad68/intervertebral-lookonce/blob/main/Images/supp_inference.png)

### For more results of the proposed method for intervertebral disc labeling please refer to the [paper](http://openaccess.thecvf.com/content_ICCVW_2019/papers/VRMI/Azad_Bi-Directional_ConvLSTM_U-Net_with_Densley_Connected_Convolutions_ICCVW_2019_paper.pdf)



### Query
All implementations are done by Reza Azad and Moein Heidari. For any query please contact us for more information.

```python
rezazad68@gmail.com
moeinheidari7829@gmail.com

```

