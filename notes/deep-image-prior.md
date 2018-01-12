#Deep Image Prior
### by Dmitry Ulyanov(Skoltech, Yandex), Andrea Vedaldi(Oxford), Victor Lempitsky(Skoltech)
### ArXiv:1711


This paper proposes a new method for standard inverse problems such as denoising, super-resolution, and inpainting. The method is using a randomly-initialized neural network as a handcrafted prior. They point out that natually-looking images are converged faster than noise for reconstruction tasks where the recontruction network has fixed random-noises input and the images pluse noise target. So they stop the training for before overfitting to degraded inputs.


