## Data Collection Methodology

### Narrowing the variables

We initially considered 21 variation categories (hand size, background color, camera type, time of day, framing, contrast, etc.), but this would have produced far more scenarios than we could realistically capture. We narrowed it down to the ones with the most direct impact:

| Category dropped | Reason |
|---|---|
| Contrast | Emerges naturally from lighting and background — added no new information |
| Frame composition | Overlaps with camera distance |
| Background color | Already covered by background type (clean/cluttered) |
| Hand size | No real variation with only two contributors; replaced with camera distance, which we can control on purpose |
| Frame position | The model (transfer learning, MobileNet) is robust to this; gesture shape and angle matter far more |
| Camera model, time of day, room | Absorbed by background and lighting; controlling separately needed more time than we had |

**Kept:** hand identity, front/back, angle, distance, lighting, background type, and finger positioning per gesture.

### Saving work — with a limit

We photographed only the right hand and generated left-hand examples via horizontal flip, since a mirrored photo of a right hand looks exactly like a left hand making the same gesture.

We decided against artificial 90°/180°/270° rotation to multiply angle coverage: a hand held normally is never seen rotated like that by a real camera. Training on such images risked hurting the model during the swap test, not helping it.

### After self-testing

*(Fill in after Step 6)*

- Noticed: ...
- Change made: ...
- Example: "Scissors was confused with rock when fingers were close together, so we added N more images with a wider spread."
