# DermKaggle
---

### **👥 Team Members**

| Name | GitHub Handle | Contribution |
| ----- | ----- | ----- |
| Dakota Chang | @dakotacsk |  |
| Sarah Cadet | @SarahCadet | Created a branched, multi-input model that was used for the initial submission with 5% accuracy.|
| Blair Kuzniarek | @bkuzniarek |  |
| Khushi Rajoria | @krajoria |  |
| Michaela Fox | @mfox0914 |  |
| Sevinch Noori | @sevinchnoori | Building + training of ExCeption model, parts of ReadMe |

---

## **🎯 Project Highlights**

**Example:**

* Built a \[insert model type\] using \[techniques used\] to solve \[Kaggle competition task\]
* Achieved an F1 score of \[insert score\] and a ranking of \[insert ranking out of participating teams\] on the final Kaggle Leaderboard
* Used \[explainability tool\] to interpret model decisions
* Implemented \[data preprocessing method\] to optimize results within compute constraints

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
* How to set up the environment
* How to access the dataset(s)

Access the data through this link: https://www.kaggle.com/competitions/bttai-ajl-2025/data
* How to run the notebook or scripts

---

## **🏗️ Project Overview**

This Kaggle competition was presented through a collaboration between Break Through Tech and the Algorithmic Justice League for students to build a machine learning model that classifies skin conditions across various skin tones in order to “advance equity by centering those historically excluded in AI” and avoid diagnostic errors, late treatments, and health disparities for underserved groups. The Algorithmic Justice League is “an organization that combines art and research to illuminate the social implications and harms of artificial intelligence”. Their mission to increase public awareness about the effects of AI, provide advocates with resources to run campaigns, strengthen the voice and chose of impacted groups, and excite researchers, policymakers, and industry practitioners to work against the harms of AI.

---

## **📊 Data Exploration**

The dataset used is a subset of the FitzPatrick17k dataset, a labeled set of ~17,000 images of various serious and cosmetically dermatological conditions across a variety of of skin tones that are scored through the FitzPatrick skin tone scale (FST). This set contains around 4,500 images from the dataset and represents 21 skin conditions (out of over 100). The subset is used in order to have a more manageable and satisfying classification problem while maintaining appropriate amount of representation issues.

* Data exploration and preprocessing approaches

* Challenges and assumptions when working with the dataset(s)

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

Using this configuration, we improved our final model’s accuracy to [TODO final accuracy]%, a significant boost from our initial baseline. We used an 80/20 train-validation split and relied on top-1 accuracy as our primary evaluation metric throughout the tuning process.

---

## **📈 Results & Key Findings**

**Describe (as applicable):**

* Performance metrics (e.g., Kaggle Leaderboard score, F1-score)
* How your model performed overall
* How your model performed across different skin tones (AJL)
* Insights from evaluating model fairness (AJL)

**Potential visualizations to include:**

* Confusion matrix, precision-recall curve, feature importance plot, prediction distribution, outputs from fairness or explainability tools

---

## **🖼️ Impact Narrative**

**AJL challenge:**

As Dr. Randi mentioned in her challenge overview, “Through poetry, art, and storytelling, you can reach others who might not know enough to understand what’s happening with the machine learning model or data visualizations, but might still be heavily impacted by this kind of work.”
As you answer the questions below, consider using not only text, but also illustrations, annotated visualizations, poetry, or other creative techniques to make your work accessible to a wider audience.
Check out [this guide](https://drive.google.com/file/d/1kYKaVNR\_l7Abx2kebs3AdDi6TlPviC3q/view) from the Algorithmic Justice League for inspiration!

1. What steps did you take to address [model fairness](https://haas.berkeley.edu/wp-content/uploads/What-is-fairness_-EGAL2.pdf)? (e.g., leveraging data augmentation techniques to account for training dataset imbalances; using a validation set to assess model performance across different skin tones)
2. What broader impact could your work have?

---

## **🚀 Next Steps & Future Improvements**

**Address the following:**

* What are some of the limitations of your model?
* What would you do differently with more time/resources?
* What additional datasets or techniques would you explore?

---

## **📄 References & Additional Resources**

* Cite any relevant papers, articles, or tools used in your project

---

