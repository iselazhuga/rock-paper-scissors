## Data Collection Methodology

### Variable Selection

Initially, we considered many possible variations, but including all of them would have created too many scenarios and required an unmanageable number of images. Therefore, we focused on three main variables that have a direct impact on what the model can learn:

* **Gender:** boy / girl
* **Hand side:** front / back
* **Angle:** head-on / angled left / angled right

This gives us a total of **2 × 2 × 3 = 12 scenarios**.

The other variables were removed because they overlapped with the selected variables, were naturally affected by other conditions, or would have required too much additional data.

| **Removed variable** | **Reason**                                                                                                           |
| -------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Hand size            | Limited real variation with only two contributors; camera distance also affects the apparent hand size in the image. |
| Background color     | Can naturally vary during data collection.                                                                           |
| Contrast             | Mainly affected by lighting and background.                                                                          |
| Position/composition | Related to camera distance and hand positioning.                                                                     |
| Camera model         | Would add many combinations without a clear benefit.                                                                 |
| Time of day          | Mainly affects lighting.                                                                                             |
| Room                 | Mainly affects background and lighting.                                                                              |

### Artificial Data Augmentation

To reduce manual work, the original photos were taken using only the **right hand**. We then used a **horizontal flip** to create left-hand examples.

We also used artificial rotations of **90°, 180°, and 270°** to create additional examples.

Starting from **216 original images**, approximately **1,728 images** were created after these transformations.

Unlike the horizontal flip, artificial rotations can create positions that do not represent how a hand would typically be held in front of a camera. Therefore, their impact was tested rather than assumed to improve the model.

### Data Comparison

We trained and compared two models:

1. **Real images only** — 216
2. **Real + augmented images** — 1,728

This allowed us to evaluate whether augmentation improves or reduces the model's performance.

The final model will be selected based on its performance on a **separate test set** that was not used during training. This is more important than performance on the training data alone, since very high training performance can be a sign of **overfitting**.

### Testing and Improvement

After training, the model was tested with new images. We analyzed its errors and, when we identified a specific problem, added targeted images to address it.

For example, if the model confuses **scissors with rock**, we can add more scissors images with the fingers spread further apart.

**Cycle:** Collect → Augment → Train → Test → Improve → Retrain

### Results After Testing

*To be completed after Step 6.*

* **What we observed:** ...
* **Problem identified:** ...
* **Change made:** ...
* **Result:** ...
* **Real vs. Real + Augmented — which performed better:** ...
