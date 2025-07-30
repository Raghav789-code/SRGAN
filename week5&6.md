# Weekly Project Report: Image Super-Resolution with GANs

## Week 5 Progress Report: Initial SRGAN Training

### Objective

The primary goal this week was to train our implemented SRGAN model on the preprocessed DIV2K dataset, focusing on establishing a stable training loop, saving progress, and monitoring performance.

### Activities Completed:

1.  **Model Training:** We initiated the training process for the SRGAN model. The training was configured to run for 20-30 epochs. The initial epochs are crucial for observing the learning dynamics between the Generator ($G$) and the Discriminator ($D$).
2.  **Checkpointing Implementation:** To prevent loss of progress during long training sessions, a checkpointing mechanism was implemented. After every few epochs (e.g., every 5 epochs), the current state of the Generator, Discriminator, and their respective optimizers were saved to disk. This allows us to resume training from the last saved point in case of an interruption.
3.  **Logging with TensorBoard:** We integrated TensorBoard to log key metrics during training. This provided real-time visualization of:
    * **Loss Functions:** We tracked the Generator's content loss ($L_{Content}$), adversarial loss ($L_{Gen}$), and the Discriminator's loss ($L_D$).
    * **Evaluation Metrics:** At the end of each epoch, the model's performance on a validation set was measured using PSNR and SSIM.
    * **Image Outputs:** We also logged a few sample super-resolved images from the validation set at each epoch to visually inspect the model's improvement over time.

### Initial Observations: 📈

* The Discriminator's loss ($L_D$) typically decreased faster in the beginning as it learned to distinguish between real and generated images.
* The Generator's adversarial loss ($L_{Gen}$) showed fluctuating behavior, which is expected in a GAN setup as it tries to fool the improving Discriminator.
* Visually, the initial epochs produced blurry images, but sharpness and detail gradually improved as training progressed, validating that the model was learning successfully.

---

## Week 6 Progress Report: Evaluation and Model Improvement

### Objective

This week focused on evaluating the baseline SRGAN model trained in Week 5 and implementing advanced techniques to significantly improve the quality of the super-resolved images.

### Activities Completed:

1.  **Baseline Model Testing:** The SRGAN model from Week 5 was tested on a set of new, unseen low-resolution (LR) images. The results were qualitatively analyzed and quantitatively measured using PSNR and SSIM. While the model successfully upscaled images, some outputs contained artifacts and lacked the fine, realistic textures we aimed for.
2.  **Improvement with ESRGAN:** Based on the plan, we decided to upgrade our architecture to an Enhanced Super-Resolution GAN (ESRGAN). This involved key changes:
    * **Architecture:** We replaced the Generator's standard residual blocks with the **Residual-in-Residual Dense Block (RRDB)**, which allows for deeper network architecture and improved feature extraction.
    * **Perceptual Loss:** We refined our loss function. Instead of using the VGG features from later layers (as in SRGAN's content loss), ESRGAN's perceptual loss ($L_{perceptual}$) uses features *before* activation. This has been shown to produce sharper edges and better textures. The total Generator loss becomes $L_G = L_{perceptual} + \lambda L_{Gen} + \eta L_1$, where $L_1$ is the pixel-wise L1 loss.
    * **Relativistic Discriminator:** The standard discriminator was replaced with a **Relativistic average Discriminator (RaD)**, which estimates the probability that a real image is *more realistic* than a generated one, helping the generator synthesize more realistic textures.
3.  **Fine-Tuning:** The new ESRGAN model was trained. We applied GAN training stabilization techniques ("GAN hacks"), such as using a learning rate scheduler and carefully balancing the updates between the Generator and Discriminator to ensure stable convergence.

### Results: 🎉

The ESRGAN model showed a significant improvement over the baseline SRGAN.

* **Qualitatively:** The output images were visibly sharper, with more convincing and detailed textures. The common GAN artifacts were greatly reduced.
* **Quantitatively:** While the PSNR score was comparable or sometimes slightly lower (as ESRGAN prioritizes perceptual quality over pixel-perfect accuracy), the SSIM score and perceptual similarity metrics (like LPIPS) improved, confirming that the generated images were structurally and perceptually closer to the high-resolution originals.

---

## The Final Project: Report and Deliverables

Your final project is the culmination of all the work from the previous weeks. It should be presented as a comprehensive technical report and a code repository.

### Final Report Structure:

1.  **Abstract:** A brief summary of the project: the problem (image super-resolution), the methods used (SRGAN, ESRGAN), and the key findings.
2.  **Introduction:**
    * Explain the importance of Image Super-Resolution (ISR).
    * Briefly introduce Generative Adversarial Networks (GANs) and their application to ISR.
    * State the project's objective: to implement, train, and compare SRGAN and ESRGAN models.
3.  **Methodology:**
    * **Dataset:** Describe the DIV2K dataset and the preprocessing steps you took (e.g., creating LR-HR pairs via bicubic downsampling).
    * **Models:** Detail the architectures for both the SRGAN and ESRGAN Generator and Discriminator. Highlight the key differences (e.g., RRDB blocks).
    * **Loss Functions:** Formally define all loss functions used: Perceptual Loss ($L_{Perceptual}$), Adversarial Loss ($L_{Gen}$), and Content Loss ($L_{Content}$). Explain the role of each.
    * **Evaluation Metrics:** Explain how PSNR and SSIM are calculated and what they represent. Mention any other perceptual metrics you used (e.g., LPIPS).
4.  **Experiments and Results:** This is the core of your report.
    * **Training Details:** Describe the training environment (hardware, libraries like PyTorch), hyperparameters (learning rate, batch size, optimizer), and the number of epochs.
    * **Quantitative Results:** Present a table comparing the PSNR and SSIM scores of your SRGAN and ESRGAN models against the standard Bicubic upsampling method on a test set.
    * **Qualitative Results:** This is crucial for SR. Showcase a variety of results with side-by-side image comparisons. For each example, show:
        * The original Low-Resolution (LR) input.
        * The Bicubic upscaled image (as a baseline).
        * The output from your SRGAN.
        * The output from your ESRGAN.
        * The original High-Resolution (HR) ground truth.
    * **Analysis:** Discuss the results. Which model performed better and why? Comment on the trade-off between PSNR and perceptual quality.
5.  **Conclusion:**
    * Summarize your work and key achievements.
    * Discuss challenges faced during the project (e.g., long training times, GAN instability).
    * Suggest potential future work (e.g., trying other datasets, experimenting with different GAN architectures, deploying the model).
