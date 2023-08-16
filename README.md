# One Step Ahead - Detecting unusual human motions for QualityMinds

# Project Log
========================

## Introduction
The "One Step Ahead" project focuses on detecting unusual human motions to enhance the human motion prediction models used by QualityMinds. Accurate human motion prediction is essential for the development and deployment of autonomous systems, including autonomous vehicles and industrial robots. This repository contains the code and tools developed by our team during the collaboration with QualityMinds.

## Understanding Human Motion Prediction
Human motion prediction involves forecasting future human movements based on their current body position and recent motions. QualityMinds leverages advanced Deep Neural Networks to predict a person's actions, looking one second ahead into the future. However, occasionally, these predictions fail due to unusual and anomalous human motions. Our project aims to address this issue.

## Key Task and Approach
The primary objective of our project was to quantify anomalies in human motions and establish a connection between outliers and failed motion predictions. To accomplish this, we used the Human 3.6m public dataset, which contains 3.6 million human poses. We restructured the dataset into 180,000 motion sequences, each consisting of 35 frames, with the position of 32 joints represented in 3D space. To prepare the dataset for our models, we performed dimensionality reduction and scaling.

Next, we employed four distinct outlier detection models, each providing a unique perspective on identifying outlying motions. To validate our findings, we compared the prediction errors from QualityMinds' human motion prediction models with the outliers we identified. This allowed us to demonstrate the direct relationship between outliers and unsuccessful motion predictions.

## Results and Tools

### Four anomaly detection models
We provide four unsupervised learning models, namely CBLOF, IFOREST, HDBSCAN, LOF, to produce a learning representation for each sequence.
All the models were trained on a training set of four different subjects from the H3.6M dataset.
We developed three versions for each model:
- 1st version trained on the whole sequence (35 frames)
- 2nd version trained on the time input sequence (10 frames)
- 3rd version trained on the time output sequence (25 frames)

Each model provides us with a decision/OOD score. The higher the score, the more abnormal a sequence is. Out of distribution sequences tend to have higher scores than in distribution sequences.


In the Data_analysis_H36M.ipynb and presentation.ipynb notebook, we provided Analysis ToolKit to help analyze our findings.


### Analysis Toolkit: Metric Comparison
To validate our results we used the MPJPE errors from two motion prediction models STSGCN and motionmixer as a ground truth. We define two different thresholds to turn the unsupervised learning problem into a classification problem. This enables us to compute artificial versions of known metrics to measure ‘precision’ and ‘recall’. We provided three functions to help QM compare the performance of different OOD models and MP models.

### Analysis Toolkit: Generate two interactive apps
#### Outlier Detection App
This interactive tool presents motion sequences as data points on a scatter plot, with outliers represented as green triangles and inliers as gray circles. Users can explore specific data points and access detailed information, such as the motion's index and underlying action, for further analysis. The app offers flexible analysis scenarios, enabling users to adjust the decision score threshold to define outliers. It also facilitates comparisons of outliers and inliers across different actions, providing comprehensive insights into unusual motions.

#### Outlier Validation App
Our second interactive plot demonstrates the correlation between a motion sequence's anomaly degree (precision score) and its prediction error. The positive correlation confirms that motions with higher decision scores are more likely to have higher prediction errors. This validation supports the notion that the identified outliers indeed contribute to higher prediction errors. The app allows QualityMinds to explore specific outliers, choose different analysis scenarios, and efficiently compare precision and recall metrics.

### Analysis Toolkit: Kinematic Comparison Toolkit
The toolkit enables QualityMinds to compare and visualize inliers and outliers for specific actions, such as walking, based on kinematic key characteristics, like joint velocity and acceleration. Understanding these nuances offers valuable insights for comprehending why observations are detected as outliers.

### Blogpost and Report
A detailed report and a short BlogPost was delivered to QM as well. 


## Conclusion and Outlook

In conclusion, our collaboration with QualityMinds has equipped them with valuable tools to improve human motion prediction for autonomous driving and other applications. Going forward, we plan to generalize our insights to other public datasets, further enhancing QualityMinds' motion prediction models for human-robot interaction and autonomous systems. This will ensure a safer and more efficient future for everyone. We are proud to have been part of this project and are excited to witness the impact of our work in the field of autonomous technology.
How to Use This Repository

This repository contains the code for the outlier detection models, the outlier detection app, the outlier validation app, and the kinematic comparison toolkit. To get started, follow these steps:

Clone the repository to your local machine using the following command:

    bash

    git clone git@gitlab.propulsion-home.ch:datascience/bootcamp/final-projects/ds-2023-05/qualityminds.git

Set up the necessary dependencies by referring to the "requirements.txt" file in the repository.

Use the provided Jupyter notebooks and Python scripts to run the outlier detection models and generate the outlier detection and validation apps:

### Notebooks contained in this project:
* Data Analysis H3.6M: Main notebook, you can run all functions from here
* presentation: Slim version of the main notebook used to create visuals
* outlier detection app 1 & 2: Notebook to create web apps for the outlier detection and validation app. 

**Refer to the "How to run" section of the main notebook to know more about the workflow, and which sections of the notebook to run in which order.**

# License

This project is released under the MIT License. Please refer to the "LICENSE" file for more information.

# Acknowledgments

We would like to thank QualityMinds and Constructor Learning for the opportunity to collaborate on this project and contribute to advancing the field of human motion prediction for autonomous systems.
