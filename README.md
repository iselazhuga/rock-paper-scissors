# Rock, Paper, Scissors — Project 1

**Holberton School · Build with AI Summer Program**

An image classifier built with **Teachable Machine** that recognises three hand gestures: **rock, paper, and scissors**.

The main goal of the project was not only to build a classifier, but also to investigate **what the model actually learns** and whether it relies on the hand gesture or on other visual features such as backgrounds, lighting, or the person.

---

## 1. Data Statement

### What we collected

Photographs of hands showing three gestures:

* Rock
* Paper
* Scissors

### Whose data?

* **Our own photographs:** Two of the three group members contributed hand photographs. The third member participated in planning, training, and evaluation but chose not to be photographed.
* **Kaggle dataset:** A public Rock, Paper, Scissors hand dataset with white backgrounds, used under its published licence.
* **Webcam images:** Additional images collected by our group using a webcam and cluttered backgrounds.

### Storage and publication

The project repository is public on GitHub. Our raw personal training photographs remain private within the group. Only the exported model, screenshots, and results are published.

The contributing members agreed to the use of their photographs. The published material contains only hand gestures, with no faces or other identifying information.

---

## 2. Data Collection Methodology

### Variable Selection

We considered many possible variations, but using all of them would have created too many combinations.

We selected three main variables:

* **Gender:** boy / girl
* **Hand side:** front / back
* **Angle:** head-on / angled left / angled right

This produced:

**2 × 2 × 3 = 12 scenarios**

For each scenario, we collected:

* 6 Rock images
* 6 Paper images
* 6 Scissors images

Therefore:

**12 × 18 = 216 original images**

This gives **72 original images per gesture**.

### Why include gender?

Gender was not used as a prediction target. It was included as a practical source of visual variation.

Hands can differ in features such as **nail polish and nail length**, which affect the pixels in an image. Including both a boy and a girl helped introduce additional visual variation and reduce the chance of the model relying on a single person's hand characteristics.

### Removed Variables

| Variable               | Reason for removal                                                                                 |
| ---------------------- | -------------------------------------------------------------------------------------------------- |
| Hand size              | Limited real variation with only two contributors; camera distance also changes apparent hand size |
| Background colour      | Changes naturally with the environment                                                             |
| Contrast               | Mainly affected by lighting and background                                                         |
| Position / composition | Related to camera distance and hand positioning                                                    |
| Camera model           | Would create many additional combinations without a clear benefit                                  |
| Time of day            | Mainly affects lighting                                                                            |
| Room                   | Mainly affects background and lighting                                                             |

---

## 3. Artificial Data Augmentation

We originally photographed only the **right hand**.

To create additional examples, we used:

* **Horizontal flipping** to create left-hand-like examples
* **90°, 180°, and 270° rotations**

For each gesture:

**72 original images → 144 with flipping → 576 with rotations**

Overall:

**216 → approximately 1,728 images**

We did not assume that rotations would automatically improve the model. Some rotated images may represent hand positions that would not normally appear in front of a camera, so we treated rotation as an experiment and compared the resulting models.

---

## 4. Models Trained

### Stage 1

We trained five different models using different combinations of our images, the Kaggle dataset, and artificial augmentation.

| Model                              | Data                                                                                                                            |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **RPS Kaggle only**                | Kaggle dataset with white backgrounds. Around 1,200 poor Rock samples were removed, and Rock was rebalanced with webcam images. |
| **RPS Joined**                     | Our images + horizontal flipping                                                                                                |
| **RPS Joined - Kaggle**            | Our images + Kaggle images + horizontal flipping                                                                                |
| **RPS Joined Artificial**          | Our images + horizontal flipping + rotations                                                                                    |
| **RPS Joined Artificial - Kaggle** | Our images + horizontal flipping + rotations + Kaggle images                                                                    |

We compared all five models using Teachable Machine's live preview.

**RPS Joined Artificial - Kaggle** performed best during the initial comparison, especially on white backgrounds.

However, all five models struggled with **cluttered backgrounds**.

This suggested that the models were not generalising well beyond the visual conditions represented in the training data.

---

## 5. Stage 2 — Final Model

To improve performance on different environments, we added webcam images taken against **cluttered and varied backgrounds**.

Our final model was:

**RPS Joined Artificial - Kaggle - Webcam**

The final dataset contained:

| Class     |    Images |
| --------- | --------: |
| Paper     |     2,898 |
| Rock      |     2,851 |
| Scissors  |     2,864 |
| **Total** | **8,613** |

### Training settings

* **Epochs:** 50
* **Batch size:** 16
* **Learning rate:** 0.001

---

## 6. Results

### Internal Teachable Machine Test

Teachable Machine held out approximately 15% of the images for testing.

|                     | Predicted Paper | Predicted Rock | Predicted Scissors |
| ------------------- | --------------: | -------------: | -----------------: |
| **Actual Paper**    |             434 |              0 |                  1 |
| **Actual Rock**     |               0 |            428 |                  0 |
| **Actual Scissors** |               0 |              1 |                429 |

The model correctly classified:

**1,291 out of 1,293 images = approximately 99.8% accuracy**

### Why we do not treat 99.8% as the final result

Most of our dataset contains flipped or rotated versions of the same original photographs.

Therefore, very similar images may appear in both the training and test sets. This creates a risk of **data leakage**, meaning the test set may not represent truly unseen examples.

For this reason, the internal 99.8% accuracy should not be interpreted as the model's real-world performance.

The more meaningful evaluation is the **swap test using new hands and images that the model has never seen**.

---

## 7. Confusion Matrix

The confusion matrix shows which gestures the model classified correctly and which ones it confused.

In the internal test, the model made only two mistakes:

* One **Paper** image was predicted as **Scissors**
* One **Scissors** image was predicted as **Rock**

These mistakes are visually understandable because some Paper and Scissors poses can have similar outlines, while certain Scissors poses can resemble a closed hand.

---

## 8. What Did the Model Actually Learn?

This was one of the main questions of our project.

Our Stage 1 models performed well on **plain white backgrounds** but struggled with **cluttered backgrounds**.

This suggests that the models may have learned some background-related features instead of relying only on the hand gesture. The Kaggle dataset, in particular, contained predominantly white backgrounds.

To address this, we added webcam images with cluttered backgrounds in Stage 2.

However, we have not yet directly tested whether the model relies on a specific person's hand or on nail characteristics.

The internal 99.8% accuracy cannot answer these questions because of the risk of data leakage.

The swap test is therefore important for evaluating how well the model actually generalises to new hands and environments.

---

## 9. Limitations and Next Steps

### Limitations

* Only two group members contributed personal hand photographs.
* The internal test may contain images very similar to training images.
* The model may still rely on background or person-specific visual features.
* Nail-related variation was not tested separately.

### Next Steps

* Create a clean train/test split **before augmentation**.
* Evaluate models using a completely separate test set.
* Collect images from more people and different hands.
* Test the effect of nail polish and nail length separately.
* Compare performance across different backgrounds and cameras.

---

## 10. Key Takeaway

This project showed us that building an image classifier is not only about achieving a high accuracy score.

The more important question is:

> **What did the model actually learn?**

Through data collection, augmentation, model comparison, testing, and error analysis, we learned that **the quality and diversity of the data are just as important as the model itself**.

