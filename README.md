# Machine Learning for Image and Object Recognition (IMA205) - 2023/2024

## Course Overview

This repository contains materials and resources for the course **IMA205: Machine Learning for Image and Object Recognition**, part of the **Image-Data-Signal** curriculum. The course introduces core machine learning techniques for image analysis, covering both supervised and unsupervised learning, as well as deep learning methods like artificial neural networks (ANNs) and convolutional neural networks (CNNs).

### Key Topics:

- Unsupervised Learning: Curse of dimensionality, PCA, ICA, NNMF.
- Supervised Learning: Overfitting, OLS, Ridge, LASSO, LDA, QDA.
- Support Vector Machines: Theory and application of SVMs.
- Decision Trees and Random Forests: Classification and regression tasks.
- Ensemble Learning: Methods to combine multiple models.
- Artificial Neural Networks (ANNs): Basics of neural network architectures.
- Convolutional Neural Networks (CNNs): Advanced techniques for image recognition.

## Prerequisites

Students are expected to have knowledge of:
- Basic statistics and linear algebra (MDI103, MDI104, MDI113, MDI114, or equivalent courses).
- General programming skills.

## Course Structure

- Total Hours: 24 hours of lectures and practical sessions.
- Credits: 2.5 ECTS
- Evaluation: Attendance of the first course and mandatory labs, followed by a final project (Challenge) and practical reports.

## Instructor

- Professor Pietro Gori

## Installation and Setup

Some exercises and projects require Python and relevant image processing libraries. You can follow the instructions below to set up your environment using `conda`:

1. Anaconda/Miniconda: Download and install Python with Anaconda or Miniconda from [Conda Official Site](https://docs.conda.io/en/latest/).
2. Image Processing Libraries: Create a new conda environment with the necessary packages:
   ```bash
   conda create -n ima python matplotlib numpy scipy scikit-image ipykernel pandas scikit-learn seaborn jupyter tqdm pytorch pytorch-cuda=12.1 torchvision -c pytorch -c nvidia
   ```
3. Activate the environment:
   ```bash
   conda activate ima
   ```

4. Launch Jupyter Notebook (if required for exercises):
   ```bash
   jupyter notebook
   ```

This will set up the necessary environment for running image processing tasks and exercises for the course.

## How to Contribute

Feel free to contribute to the repository by:
- Submitting pull requests for corrections or improvements.
- Providing additional examples or extending the projects.
