# VAEs-and-GANs-applied-to-cat-faces

## Variational Auto-Encoders (VAEs):

Variational Autoencoders are a type of a generative model with key differences to Autoencoders. Firstly, let's discuss why a classic Autoencoder cannot generate 
new data. The aim of Autoencoders is to minimize the reconstruction loss, this can come at the expense of the regularity of the latent space. By latent space, 
we mean a feature space where items that are similar to each other are closer together, and by regularity, we mean that that latent space should be continuous and 
complete. Therefore, the objective of minimizing the reconstruction loss can cause overfitting leading to a very irregular latent space. As a result, you can't use
the learned codings to generate new data. Variational Autoencoders differ by being a probabilistic model. Instead of producing the hidden representation directly, 
the encoder produces a gaussian distribution of the latent representation with a mean mu and a standard deviation sigma, the latent representation is then 
randomly sampled from that distribution and decoded. The cost function of VAEs consist of 2 parts: 1) the reconstruction loss and the 2) the latent loss 
(regularization term) which penalizes the latent vector if it doesn't adhere to a gaussian distribution, this is done via minimizing the Kullback–Leibler divergence
(Is a measure of the statistical distance between one distribution B and a reference distribution A). The use of a normal distribution and random sampling of the
codings results in an output that looks similar to the input, hence, generating new data. In essence, VAEs regularize the latent space to enable the generation of
new data.

The arhitecture of VAEs is illustrated in the figure below:



## Generative Adversarial Networks (GANS):
As the name suggests, Generative Adversarial Networks are also a type of a generative model. However, they work in quite a different matter than VAEs.
VAEs expand upon the idea of classic Autoencoders by regularizing the latent space, however, the basic principle of GANs is to use two networks that compete with 
each other: a generator network that generates images and a discriminator network that takes either a generated image of a real image and
discriminates whether this image is fake or real. i.e, is this a generated image or an image from the actual training data. The competition 
(hence the name Adversarial) of these 2 networks forces the networks to improve until the generator produces images that are indistinguishable from the 
real ones, i.e, until the generator successfully tricks the discriminator, and that is how we can generate new images. The network is trained in
two phases. In the first phase, we train the discriminator using a combination of real images from the training data and randomly generated images from the 
generator network. In this phase, we are basically teaching the discriminator what constitutes a real image so it can compete with the generator in the second
phase, where we train the generator. In particular, the generator never gets to deal with the real images, the input of the network is a latent representation  
. Initially this representation can be just a random Gaussian distribution, as the network competes with the discriminator, 
it learns the nature of images that can fool it, ultimately leading the generator to learn the underlying latent space of the training images.
