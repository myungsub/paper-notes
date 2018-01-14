# Deep Image Prior
### by Dmitry Ulyanov(Skoltech, Yandex), Andrea Vedaldi(Oxford), Victor Lempitsky(Skoltech)
### ArXiv:1711


This paper proposes a new method for standard inverse problems such as denoising, super-resolution, and inpainting. Surprisingly, the proposed networks do not learn any knowledge for image restoration from image database. They only train the network with a single degraded image, which is wanted to be restored.

Before reading this paper, skimming the network architecture and training concept in [supmat](https://box.skoltech.ru/index.php/s/ib52BOoV58ztuPM) are recommended for faster understanding. They use *generator networks* which have fixed random-noise(inputs) and degraded images(targets). This is against conventional restoration networks which have degraded images(inputs) and ground truth images(targets).

## Approach

### Image Prior

Image restoration problems, which aim to recover original image $x$ having corrupted image $x_0$, are open formulated as an optimization tasks:

![eq1](../img/deep_image_prior/eq1.png)

where $E(x;x_0)$ is *data term* and $R(x)$ is an *image prior*.
They model the prior $R(x)$ with a ConvNet $f_theta(z) = x$ where $theta$ is parameters of the ConvNet and $z$ is a fixed input. They assert that the prior term can be removed by selecting a good mapping $f_theta$, so the formulation changes to

![eq3](../img/deep_image_prior/eq3.png)

They said, this means "instead of searching for the answer in the image space we now search for it in the space of neural network's parameters".


### High Noise Impedance

The proposed method is using a randomly-initialized neural network as a handcrafted prior. 
Here is a key experiment from the [paper](https://sites.skoltech.ru/app/data/uploads/sites/25/2017/12/deep_image_prior.pdf) to catch the meaning of the method.

![fig1](../img/deep_image_prior/fig1.png)

The experiment points out that natually-looking images are converged faster than the image plus noise for reconstruction tasks. So they could stop training the network before overfiting to noise.
This means that the generator network is sufficient to capture low-level image statistics prior. In contrast, previous restoration networks learn realistic image priors from a large number of example images.


## Experiment
For key image restoration tasks(blind denoising, super-resolution, and inpainting), they used GCF-BM3D, Set5, Set14, and some other images for comparison. Empathize again, they do not use database to train, but use only a single degraded image to restore.

For each task, they handcrafted networks and energy functions to find efficient image prior. All results are impressive but PSNR is higher than learning based ConvNets at only inpainting applications.



## My Toughts
* The first equation, which they assert conventional image restration problem, is wrong. They used original image $x$ as a variable of the minimization.

* So their objective function is not for an image restoration, but for an image generation. I'm not fully understanding why they removed the image prior term $R(x)$. By the final objective function, they perpose to generate degraded images.

* I think that they want to focus on the implicit regularization which has low impedance to naturally-looking images. However, the term *impedance* is also rethinkable. This is because *early stopping*, which they used for the results exactly, is a conventional term for implicit regularization in Machine Learning.

* In short, deep neural networks can have image restoration priors depend on the architectures which can be shown by degraded image generation with early stopping.
