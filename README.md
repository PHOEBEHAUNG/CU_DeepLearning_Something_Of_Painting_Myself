# CU_DeepLearning_Something_Of_Painting_Myself

# Something of a Painter Myself

I implements a **CycleGAN** model to convert real photos into Monet-style 
paintings. The model uses unpaired image-to-image translation, it can learn 
the mapping without requiring paired training examples.

## Model Architecture

The CycleGAN consists of Two Generators and Two Discriminators :
- **Two Generators (U-Net)**: G_photo2monet and G_monet2photo
  - Encoder-decoder structure with skip connections
  - Input/Output: 256×256×3 images normalized to [-1, 1]
  
- **Two Discriminators (PatchGAN)**: D_photo and D_monet
  - Classify 32×32 patches as real or fake
  - Helps maintain local texture consistency

## Training Process

The model is trained with three types of losses:
1. **Adversarial Loss**: Encourages generated images to fool discriminators
2. **Cycle Consistency Loss** (weight=10.0）
3. **Identity Loss** (weight=0.5): Preserves color composition

Training parameters:
- Batch size: 8
- Learning rate: 2e-3 

## Data Processing

- Input: 300 Monet TFRecords + 7038 Photo TFRecords
- Preprocessing: Resize to 256×256, normalize to [-1, 1]
- Augmentation: Shuffling with buffer size 1000

## Output
<img width="649" height="367" alt="image" src="https://github.com/user-attachments/assets/c9b0d62f-7953-4a57-998d-0a5661ba3a1f" />


Finally, I generates 8000 Monet-style images from the photo dataset, saved as JPEG files in a ZIP archive for submission.

# Conclusion

This project implemented a **CycleGAN model** for photo-to-Monet style transfer using unpaired image translation.

This project shows how **deep learning can effectively learn artistic style transformations** from unpaired datasets, opening possibilities for various creative applications.

## Key Results
I train 300 Monet paintings + 7,038 photos processed via efficient TFRecord pipeline. 8,000 Monet-style images are saved as JPEGs.

## Training Progress

| Step | G Loss | D Loss |
|------|--------|--------|
| 0    | 12.64  | 1.64   |
| 100  | 6.66   | 1.37   |
| 200  | 6.68   | 1.39   |
| 300  | 6.08   | 1.34   |
| 400  | 6.18   | 1.31   |

**Key Finding**: Generator loss decreased steadily.
G Loss decreased from 12.64 → 6.18 shows the model is learning to generate realistic Monet-style images.


## Future Improvements
- Extend training to 10,000+ steps for better quality
- Add evaluation metrics (FID score, perceptual loss)
- Implement data augmentation (flips, rotations)
- Experiment with attention mechanisms
