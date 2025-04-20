# Captcha Recognition Tasks for Precog Recruitment by Sarthak Jain

## Task 0: Dataset Generation (Image-Text Pairs)

### Easy Set
- **Background:** `Image.new()` – plain white background.
- **Text rendering:** `ImageDraw.Draw().text()` to place the word on the image.
- **Font:** Single consistent font using `ImageFont.truetype()` (e.g., Arial).
- **Case:** All **uppercase** words.
![Easy Task Example](https://github.com/SarthakJaindebugger/captcha_recognition_preceogtasks/blob/main/Easy.png)

---

### Hard Set
- **Multiple Fonts:** Fonts randomly picked from a directory using `ImageFont.truetype()`.
- ** Per-Character Styling:**
  - Each character is drawn in a separate loop.
  - Casing varies: `random.choice([ch.upper(), ch.lower()])`.
  - Fonts vary: different `ttf` file per character.
- **Backgrounds:**
  - Noisy or textured using `cv2` and `NumPy`.
  - Random shapes: lines, rectangles, or patterns via `cv2.line()`, `cv2.rectangle()`.
- **Effects:**
  - Random **rotations**, **jitter**, or **offsets** for realism.
  - Simulates distortions found in CAPTCHAs.
   ![Bonus Task Example](https://github.com/SarthakJaindebugger/captcha_recognition_preceogtasks/blob/main/Hard.png)
---

### Bonus Set 
- Note: I've made 2 types of Bonus sets. One which is similar to what has been asked in the Precog tasks and second a much difficult one for the Machine to understand.
- **Red background:** Word is rendered **reversed** (e.g., “hello” shown as “olleh”).
- **Green background:** Normal word.
- **Logic:** Word is reversed with `[::-1]` before rendering **only** if background is red.
  ![Bonus Task Example](https://github.com/SarthakJaindebugger/captcha_recognition_preceogtasks/raw/main/Bonus1.png)
  ![Bonus Task Example](https://github.com/SarthakJaindebugger/captcha_recognition_preceogtasks/raw/main/Bonus2.png)


---

## Task 1: Classification (100 Words)
### Dataset: Subset from the Easy and Hard sets combined is used.

### Model:
- **CNN-based Classifier** (PyTorch).
  - Conv2d → ReLU → MaxPool → FC → Softmax.
- **Loss:** `nn.CrossEntropyLoss()`.
- **Optimizer:** `torch.optim.Adam`.
- Used **Dropout** and **data augmentation** to reduce overfitting.
# Test Accuracy achived is ~71% 

---

## Task 2: Generation (OCR/Text Recognition)

### Model: **CRNN (Convolutional Recurrent Neural Network)**

#### Architecture:
1. **CNN (Conv2D + Pool)** – Extract spatial features.
2. **Reshape:** Output turned into a **sequence** (Width as time steps).
3. **BiLSTM:** Captures sequential character patterns.
4. **Linear Layer:** One for each time step.
5. **Softmax:** Predicts characters + blank.
6. **CTC Loss:** For aligning predictions to true text without needing per-character position.
# Test Accuracy achived is ~53%   

---

## Task 3: Bonus Generation

- Background = Reversed word (e.g., “hello” → “olleh”)  
- Background = Normal word  

- Output label **always remains “hello”**.
- Model must **implicitly learn** the background → reversal pattern.
- No explicit cue given — it just sees image + label mismatch and learns.
---

## Libraries Used

| Purpose                    | Library                     |
|----------------------------|-----------------------------|
| Image Creation/Rendering   | `PIL` (Pillow)              |
| Noise/Textures             | `NumPy`, `cv2`              |
| Machine Learning Framework | `PyTorch`                   |
| Sequence Loss              | `CTCLoss`                   |
| Visualization              | `matplotlib`                |
| Fonts & Randomization      | `ImageFont`, `random`       |

