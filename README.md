## Data Collection Methodology

### Variable Selection

At the beginning of the project, we considered several possible variations for the images. However, including all of them would have created too many combinations and required an impractical number of images.

Therefore, we selected three main variables that we considered relevant to the visual information available to the model:

* **Gender:** boy / girl
* **Hand side:** front / back
* **Angle:** head-on / angled left / angled right

This results in a total of:

**2 × 2 × 3 = 12 scenarios**

### Why did we include gender?

The distinction between **boy and girl** was included as a practical source of visual variation, rather than as a demographic category itself.

Visible characteristics of the hands can differ between individuals, such as **nail polish, nail length, or other hand-related features**. These characteristics can affect the pixels in an image and could potentially influence what the model learns.

By including both boys and girls, we wanted to introduce this type of visual variation and reduce the possibility that the model learns features such as painted or longer nails instead of focusing on the actual **Rock, Paper, Scissors gesture**.

### Removed Variables

Several other variables were considered but were not included in the final scenario design. They were removed because they overlapped with the selected variables, could naturally change during data collection, or would have created too many additional combinations.

| Removed variable       | Reason                                                                                             |
| ---------------------- | -------------------------------------------------------------------------------------------------- |
| Hand size              | Limited real variation with only two contributors; camera distance also affects apparent hand size |
| Background color       | Can naturally vary during data collection                                                          |
| Contrast               | Mainly influenced by lighting and background                                                       |
| Position / composition | Related to camera distance and hand positioning                                                    |
| Camera model           | Would add many combinations without a clear benefit                                                |
| Time of day            | Mainly affects lighting                                                                            |
| Room                   | Mainly affects background and lighting                                                             |

## Artificial Data Augmentation

To reduce manual data collection, the original photographs were taken using only the **right hand**.

We then used **horizontal flipping** to create left-hand examples.

We also applied artificial rotations of:

* **90°**
* **180°**
* **270°**

Starting from **216 original images**, approximately **1,728 images** were obtained after applying these transformations.

However, artificial rotations may create hand positions that are not representative of how a person would normally hold their hand in front of a camera. Therefore, we did not assume that rotations would automatically improve the model. Their effect was evaluated through model comparison.

## Data Comparison

We trained and compared two models:

1. **Real images only:** 216 images
2. **Real + augmented images:** approximately 1,728 images

The purpose of this comparison was to determine whether artificial data augmentation improved or reduced model performance.

The final model was selected based on its performance on a **separate test set** that was not used during training.

This is important because high performance on the training data alone does not necessarily mean that the model will perform well on new images. A model can perform very well on training data while still being **overfitted**.

## Testing and Improvement

After training, the models were tested using new images that were not part of the training data.

We analyzed the model's predictions and identified cases where it confused one gesture with another.

When a specific problem was identified, we added targeted images designed to address that problem and then retrained the model.

For example, if the model frequently confused **Scissors** with **Rock**, we could add more Scissors images where the fingers are more clearly separated.

This created an iterative improvement process:

**Collect → Augment → Train → Test → Improve → Retrain**

## Results After Testing

This section will be completed after the final testing stage.

* **What we observed:** ...
* **Problem identified:** ...
* **Change made:** ...
* **Result:** ...
* **Real vs. Real + Augmented:** ...
* **Which model performed better:** ...
* **Nail-variation hypothesis:** [Yes/No]
* **Explanation:** Did the swap test show any confusion pattern related specifically to nail polish or nail length?
