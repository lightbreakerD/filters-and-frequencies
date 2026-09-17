# Fun with Filters and Frequencies

This is a fun example of how our brain can be tricked by the frequencies of an image.

**Everything is in [`main.ipynb`](main.ipynb).** There is a `requirements.txt` for all the
libraries we need. I have saved the results of the tasks into the folder called `output`.

## 1. Fun with Filters

There is a way to detect edges by looking at the intensity differences of neighboring
pixels. We get our gradient magnitude image by taking the square root of the sum of the
squares of the two convolved dx dy images. To make our image more clear, we can threshold
it: if the gradient magnitude is above this value, we set it to 255, else to 0.

The problem here is that we still see some noise in the images in form of small white
dots, which are not edges. What we could do is to blur the image first, to get rid of the
noise. We can simplify things by using just one convolution instead of two by making a
derivative of Gaussian filter by convolving the Gaussian with D_x and D_y.

## 2. Fun with Frequencies

### Sharpening

The high frequencies often contain the image details whereas the lower frequencies
contain the overall structure of the image. We add the high frequency part to the original
image to sharpen it, using the formula `sharpened = original + alpha * high frequency part`.
If we compare the sharpened blurred image to our original image, we can see that the
sharpening does not make the image quality better than the original image.

### Hybrid images

Hybrid images are images that we interpret differently from the distance and from close
up. We choose two images that we want to combine and blur one of them with a Gaussian
filter to get the low frequencies.

If you look at it from a distance, you will see Derek, but if you look at it from close
up, you will see the cat.

I have actually tried to use color to enhance this effect, both on the high frequency
component and also on the low frequency component. From my observations, I can say that
adding color makes the hybrid image better.

### Gaussian and Laplacian stacks

Here we blend two images together using Gaussian and Laplacian stacks and also a mask. I
use a stack size of 6 images. To create the Laplacian stack I take the ith Gaussian layer
of the stack and calculate `stacked_gau[i] - stacked_gau[i + 1]`. This mask gives us
information on how strongly to blend the two images together.

Let's try it with an irregular filter and my favorite fruit, the watermelon, and create an
Oranapplewatermelon.

Having money is great, but what if we had 2 monies? Let's take 2 photos of our money in 2
different places and use a mask to fuse them together, so that it appears as if we have 2
monies. We end up with 2 monies! The result looks so real.
