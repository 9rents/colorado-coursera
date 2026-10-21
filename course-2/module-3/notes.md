# Autoencoders, Gradient Descent and GANs: Module Notes

Summary of the key concepts from the module: autoencoders, training basics (backpropagation, gradient descent, losses) and Generative Adversarial Networks.

## 1. Autoencoders

An autoencoder is a neural network trained to reconstruct its own input through a compressed intermediate representation.

**Structure**
- **Encoder**: transforms the input into a lower-dimensional latent representation.
- **Bottleneck (code) layer**: the narrowest point between encoder and decoder. It holds the most compressed form of the input.
- **Decoder**: transforms the latent representation back into the original input format (reconstruction).
- **Activation functions**: needed to make the mapping non-linear.

**Training**
- The goal is to minimize the distance (reconstruction error) between the input and the reconstructed output, which improves reconstruction accuracy.
- Backpropagation adjusts the weights to minimize this reconstruction error.

## 2. Backpropagation and Gradient Descent

- **Backpropagation** computes the gradient of the loss with respect to every weight. The initial gradient is computed at the **output layer**, based on the loss function and the prediction error, and is propagated backwards using the **chain rule**.
- **Gradient descent** updates weights as `w = w - lr * grad`. The gradient is **subtracted** because it points in the direction of steepest increase of the loss, so moving against it reduces the loss.
- **Learning rate**: controls the size of the step taken towards the minimum on each update. It does not guarantee convergence to the global minimum.
- **Numerical gradient check**: apply a small change to a parameter or input and observe the corresponding change in the loss (finite differences), then compare with the analytic gradient.

## 3. Loss Functions

- **L2 loss (MSE)**: sum (or mean) of squared differences between predictions and targets.
- **Binary cross-entropy (BCE)**: the gradient with respect to the logit simplifies to `prediction - target` (predicted probability minus the label).

## 4. Generative Adversarial Networks (GANs)

GANs were designed to train generative models without hand-crafted feedback: an automated **discriminator** replaces human judgement of how realistic the generated samples are.

**Components**
- **Generator**: transforms low-dimensional random noise into a higher-dimensional output, mapping a simple distribution into a complex one that resembles real data. Its quality improves progressively during training. It tries to produce data indistinguishable from real data.
- **Discriminator**: distinguishes real data from generated data and gives feedback to the generator through its loss and gradients.

**Training dynamics**
- The two networks play an adversarial game: the generator tries to fool the discriminator, the discriminator tries to tell real from fake.
- Training **alternates** between the generator and the discriminator in each epoch, so both improve without one overpowering the other.
- If the generator's loss goes down while the discriminator's loss goes up, the generator is getting better at fooling the discriminator.

**Significance**
- GANs enable generation of realistic synthetic data (images and more).

## Quick Reference

| Concept | Key point |
|---|---|
| Encoder | Input -> latent representation |
| Bottleneck | Narrowest layer, most compressed form |
| Decoder | Latent representation -> reconstructed input |
| Backprop | Computes gradients via the chain rule, starting at the output layer |
| Gradient step | Subtract the gradient to reduce the loss |
| Learning rate | Step size of each update |
| L2 loss | Sum of squared differences |
| BCE gradient wrt logit | `prediction - target` |
| Generator | Noise -> realistic samples |
| Discriminator | Real vs. generated classifier |
| GAN training | Alternating updates, balanced between the two networks |
