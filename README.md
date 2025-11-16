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
