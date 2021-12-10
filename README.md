# MELA-Challenge

Evaluation scripts for [MICCAI 2022 MELA Challenge: Mediastinal Lesion Analysis](https://mela.grand-challenge.org/).


# Content

```
MELA-Challenge/
    requirements.txt                            Required packages for evaluation
    MELA/
        evaluation_mediastinum.py               Functions for model evaluation
```

# Setup

## Install required packages

Run the following in command line to install the required packages. First create a specific Anaconda environment and activate it:
```bash
conda create -n mela python=3.7
conda activate mela
```
And then install required packages using pip:
```bash
pip install -r requirements.txt
```


# Usage

## Download the competition data

You can download the competition data by first [Join](https://mela.grand-challenge.org/participants/registration/create/) the challenge then visit the [Dataset](https://mela.grand-challenge.org/dataset/) page.

## Evaluation

We use this script to evaluate your test set submission online. You can evaluate your own prediction locally as well. The evaluation script has very specific requirements on the submission format. Please make sure that these requirements are followed or your submission won't be graded.

To evaluate your prediction locally, you need to prepare the ground-truth and prediction csv file. Take validation dataset as an example. After the train/validation data is downloaded, you should unzip it and find the following ground-truth csv file:
```
    mela-val-gt.csv
```

Your prediction should be organized to a .csv file:
```
    mela-val-pred.csv
```


The prediction info .csv should have eight columns: ```public_id``` (patient ID), ```coordX```, ```coordY```, ```coordZ``` (prediction coordinates marking the bounding boxes of lesions), ```x_length```, ```y_length```, ```z_length``` (length of the predicted bounding boxes) and ```probability``` (detection confidence), e.g.:

|public_id|coordX|coordY|coordZ|x_length|y_length|z_length|probability|
|-|-|-|-|-|-|-|-|
|mela_0771|15.1|12.54|54.22|21|22|20.2|0.75|
|mela_0771|115.1|152.54|85.16|10|32.1|15.3|0.26|
|mela_0772|24.31|10.05|100.1|21|22|20.2|0.66|
|mela_0772|105.32|52.94|55.16|16|19.88|14|0.35|
|...||||||||
|mela_0880|111|85.2|65.55|20|35|37.25|0.55|
|mela_0880|52.25|73|88.26|18|20.56|40.25|0.27|

Each row in the prediction .csv represents one predicted bounding box of lesion area. The public_id should be in the same format as in the provided .nii file names.

After setting all of the above, you can evaluate your prediction through the following command line:
```bash
python -m MELA/evaluation_mediastinum --gt_dir <ground_truth_csv> --pred_dir <prediction_csv>
```
