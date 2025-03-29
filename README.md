# DermKaggle
---

### **👥 Team Members**

| Name | GitHub Handle | Contribution |
| ----- | ----- | ----- |
| Dakota Chang | @dakotacsk | Created YOLO model, performed parameter sweep, achieved 68% accuracy with submissions. |
| Sarah Cadet | @SarahCadet | Created a branched, multi-input model that was used for the initial submission with 5% accuracy.|
| Blair Kuzniarek | @bkuzniarek | Helped with data preprocessing, ExCeption model, and parts of ReadMe |
| Khushi Rajoria | @krajoria |  |
| Michaela Fox | @mfox0914 |  |
| Sevinch Noori | @sevinchnoori | Building + training of ExCeption model, parts of ReadMe |

---

## **🎯 Project Highlights**

* Built a YOLO model, achieving 68% accuracy
* Achieved a ranking of 8th place on the final Kaggle Leaderboard
* Visualized performance metrics

🔗 [Equitable AI for Dermatology | Kaggle Competition Page](https://www.kaggle.com/competitions/bttai-ajl-2025/overview)
---

## **👩🏽‍💻 Setup & Execution**

**Provide step-by-step instructions so someone else can run your code and reproduce your results. Depending on your setup, include:**

* How to clone the repository

1. Within the DermKaggle repository, in the Code tab, click of the green Code button
2. When you see a pop-up, ensure that you are within the Local tab
3. Copy the HTTPS link
4. Run git clone <link> on your preferred IDE terminal

* How to install dependencies

  !pip install ultralytics

* How to access the dataset(s)

Access the data through this link: https://www.kaggle.com/competitions/bttai-ajl-2025/data

* How to run the notebook

Run yolo-model-ajl.ipynb to run data preprocessing, yolo model training, and prediction creation.

---

## **🏗️ Project Overview**

This Kaggle competition was presented through a collaboration between Break Through Tech and the Algorithmic Justice League for students to build a machine learning model that classifies skin conditions across various skin tones in order to “advance equity by centering those historically excluded in AI” and avoid diagnostic errors, late treatments, and health disparities for underserved groups. The Algorithmic Justice League is “an organization that combines art and research to illuminate the social implications and harms of artificial intelligence”. Their mission to increase public awareness about the effects of AI, provide advocates with resources to run campaigns, strengthen the voice and chose of impacted groups, and excite researchers, policymakers, and industry practitioners to work against the harms of AI.

---

## **📊 Data Exploration**

The dataset used is a subset of the FitzPatrick17k dataset, a labeled set of ~17,000 images of various serious and cosmetically dermatological conditions across a variety of of skin tones that are scored through the FitzPatrick skin tone scale (FST). This set contains around 4,500 images from the dataset and represents 21 skin conditions (out of over 100). The subset is used in order to have a more manageable and satisfying classification problem while maintaining appropriate amount of representation issues.

* Data exploration and preprocessing approaches

  1. Explored first few rows and their types
  2. Checked classes of dataset
  3. CHecked and dropped missing values
  4. Plotted label (name of skin conditions) distribution
  5. Visualized numerical features through histogram (fitzpatrick_scale, fitzpatrick_centaur, ddi_scale)
  6. Visualized numerical features through correlation heatmap
  7. Ensured data compatibility with YOLO model

* Challenges and assumptions when working with the dataset(s)

We discovered that there were values of -1 in 'fitzpatrick_centaur' and 'fitzpatrick_scale' which we were unable to determine its significane. In the end, we decided to drop rows with this value. The column 'qc' had 2770 missing values, which we ended up concluding this column as irrelevant.

**Potential visualizations to include:**
![New Note](https://github.com/user-attachments/assets/319728a6-5720-45b7-8e92-5101f7694dbf)
![New Note](https://github.com/user-attachments/assets/0e6f1cd0-d284-4516-a5a6-4d6054905dfd)
![New Note](https://github.com/user-attachments/assets/c91b875a-d98c-4fc5-a3d6-0677d7c86274)



---

## **🧠 Model Development**

We initially experimented with a branched, multi-input model architecture, forming our first submission's basis. However, this approach yielded a low accuracy of approximately 5%. In response, we pivoted to a single-input image classification model using Ultralytics’ YOLOv8 classification pipeline.
YOLO (You Only Look Once) is a real-time, deep learning-based object detection and classification algorithm that processes an entire image in a single forward pass to simultaneously predict class labels and bounding boxes with high speed and accuracy.
Since YOLO operates directly on image inputs, our feature selection strategy focused exclusively on visual data, ignoring any auxiliary metadata. We began with the default Ultralytics hyperparameters and achieved a baseline accuracy of 67%.
To improve performance, we conducted a structured hyperparameter sweep across the following parameters:
```{python}
model_sizes = ["yolo11n-cls.pt", "yolo11s-cls.pt", "yolo11m-cls.pt", “yolo11x-cls.pt”]
epoch_list = [30, 50]
img_sizes = [128, 224]
```

Each model was evaluated using metrics such as top-1 accuracy, precision, recall, and validation loss curves. Based on the analysis, we selected the best-performing configuration:

```{python}
model_sizes = [“yolo11x-cls.pt”]
epoch_list = [45]
img_sizes = [224]
```

Using this configuration, we improved our final model’s accuracy to 68%, a significant boost from our initial baseline. We used an 80/20 train-validation split and relied on top-1 accuracy as our primary evaluation metric throughout the tuning process.

---

## **📈 Results & Key Findings**

Our final model, trained with `yolov11x-cls.pt`, achieved significant improvements over the baseline. Below are key performance visualizations and outputs used during evaluation.

### Performance Metrics

![Confusion Matrix](img/confusion_matrix.png)  
![Normalized Confusion Matrix](img/confusion_matrix_normalized.png)  
![Final Results Summary](img/results_final.png)

### Training Batch Visualizations

<div align="center"> <img src="img/train_batch0.jpg" width="200"/> <img src="img/train_batch1.jpg" width="200"/> <img src="img/train_batch2.jpg" width="200"/> </div> <div align="center"> <img src="img/train_batch5005.jpg" width="200"/> <img src="img/train_batch5006.jpg" width="200"/> <img src="img/train_batch5007.jpg" width="200"/> </div>

### Validation Ground Truth

<div align="center"> <img src="img/val_batch0_labels.jpg" width="200"/> <img src="img/val_batch1_labels.jpg" width="200"/> <img src="img/val_batch2_labels.jpg" width="200"/> </div>

### Validation Predictions

<div align="center"> <img src="img/val_batch0_pred.jpg" width="200"/> <img src="img/val_batch1_pred.jpg" width="200"/> <img src="img/val_batch2_pred.jpg" width="200"/> </div>

---

## **🖼️ Impact Narrative**

**AJL challenge:**

As Dr. Randi mentioned in her challenge overview, “Through poetry, art, and storytelling, you can reach others who might not know enough to understand what’s happening with the machine learning model or data visualizations, but might still be heavily impacted by this kind of work.”
As you answer the questions below, consider using not only text, but also illustrations, annotated visualizations, poetry, or other creative techniques to make your work accessible to a wider audience.
Check out [this guide](https://drive.google.com/file/d/1kYKaVNR\_l7Abx2kebs3AdDi6TlPviC3q/view) from the Algorithmic Justice League for inspiration!

1. What steps did you take to address [model fairness](https://haas.berkeley.edu/wp-content/uploads/What-is-fairness_-EGAL2.pdf)? (e.g., leveraging data augmentation techniques to account for training dataset imbalances; using a validation set to assess model performance across different skin tones): We kept fairness top-of-mind by first analyzing the distribution of skin tones in the dataset to understand which groups were underrepresented. To help balance this, we applied targeted data augmentation—especially on images with darker skin tones—to ensure the model saw diverse examples during training. We also evaluated model performance across different Fitzpatrick skin types to detect any disparities in accuracy. In the future, we plan to use explainability tools like SHAP to visualize which image regions influenced the model’s decisions and check for potential bias in how skin conditions are interpreted across skin tones.

2. What broader impact could your work have? This work has the potential to improve diagnostic accuracy for communities that have historically been overlooked in dermatology AI. By designing a model that performs more equitably across all skin types, we aim to reduce healthcare disparities and foster greater trust in medical technologies. 

---

## **🚀 Next Steps & Future Improvements**

**Address the following:**

* What are some of the limitations of your model? One limitation of our model is that it relies solely on visual data and does not incorporate metadata like patient age, lesion location, or Fitzpatrick skin type, which could provide helpful clinical context. Additionally, while we applied data augmentation to improve class balance, we are still limited by the inherent imbalance and underrepresentation of certain skin tones and conditions in the training dataset.
* What would you do differently with more time/resources? With more time and resources, we would fine-tune the model using skin-tone-specific performance metrics to ensure equitable accuracy across groups. We would also explore ensemble models or hybrid architectures that combine image and metadata inputs for a more holistic understanding of each case.
* What additional datasets or techniques would you explore? We’d seek out additional dermatology datasets that include high-quality images of darker skin tones to improve representation and robustness. Exploring synthetic data generation through tools like GANs could also help fill gaps in underrepresented conditions or tones. 

---

