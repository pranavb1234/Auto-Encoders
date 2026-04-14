<<<<<<< HEAD
# Autoencoders

An autoencoder is an unsupervised neural network that learns to compress input data into a compact representation and then reconstruct it back. The network is trained so that the output $\hat{x}$ is as close as possible to the input $x$ — it essentially learns to copy its input through a narrow bottleneck, forcing it to capture only the most important structure in the data.

---

## Architecture

An autoencoder has three parts:

- **Encoder** $f_\theta$ takes the input $x$ and maps it to a lower-dimensional latent code $z$. It is a stack of layers that progressively reduce the dimensionality.
- **Latent Space** $z$ is the bottleneck — the smallest layer in the network. Everything the model knows about the input must pass through here.
- **Decoder** $g_\phi$ takes $z$ and tries to reconstruct the original input $\hat{x}$. It mirrors the encoder, progressively increasing the dimensionality back.

---

## Math

### Forward Pass

Each layer applies a linear transformation followed by a non-linearity. For a single encoder layer:

$$z = \sigma(W_e x + b_e)$$

And for the decoder:

$$\hat{x} = \sigma(W_d z + b_d)$$

The full pipeline is just the composition of both:

$$\hat{x} = g_\phi(f_\theta(x))$$

### Loss Function

The loss measures how well the reconstruction matches the original input. For continuous data, **Mean Squared Error** is used:

$$\mathcal{L} = \frac{1}{n} \sum_{i=1}^{n} (x_i - \hat{x}_i)^2$$

For binary or image data with pixel values in $[0, 1]$, **Binary Cross-Entropy** works better:

$$\mathcal{L} = -\frac{1}{n} \sum_{i=1}^{n} \left[ x_i \log(\hat{x}_i) + (1 - x_i)\log(1 - \hat{x}_i) \right]$$

### Optimization

The goal is to minimize the loss over the entire training set with respect to both the encoder and decoder parameters:

$$\min_{\theta,\, \phi} \; \frac{1}{N} \sum_{j=1}^{N} \mathcal{L}(x_j,\, g_\phi(f_\theta(x_j)))$$

This is done via gradient descent. At each step, parameters are updated as:

$$\theta \leftarrow \theta - \alpha \cdot \frac{\partial \mathcal{L}}{\partial \theta}, \qquad \phi \leftarrow \phi - \alpha \cdot \frac{\partial \mathcal{L}}{\partial \phi}$$

where $\alpha$ is the learning rate.

---

## Key Points

- The bottleneck is what forces the model to learn — without it, the network could just learn the identity function and reconstruct perfectly without understanding anything.
- A smaller latent dimension $k$ means more compression but worse reconstruction. A larger $k$ makes it too easy and the model learns nothing useful.
- Autoencoders are unsupervised — they don't need labels, just raw data.
- The latent code $z$ can be used as a feature representation for downstream tasks like classification or clustering.

---

## Limitations

- The latent space has no structure, so you can't sample from it to generate new data.
- MSE loss tends to produce blurry reconstructions for images because it averages over all plausible outputs.
- If the model has too much capacity, it can memorize the training data instead of learning meaningful features.

---

## What's Next

Basic AE → **Denoising AE** → **Sparse AE** → **Variational AE (VAE)**
=======
# Auto-Encoders
>>>>>>> 3c1d67de62a1470fdb719fdaa5fb56e3131fb68c
