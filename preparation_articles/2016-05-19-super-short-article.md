---
layout: post
title: "Getting the dimensions right when using Fast Fourier Transforms to simulate Fourier Optics"
categories: misc
---

The action of a focusing lens on an electromagnetic field is described by a Fourier Transform. That makes it very easy to simulate via the [Fast Fourier Transform algorithm](https://en.wikipedia.org/wiki/Fast_Fourier_transform), which is implemented in many important programming languages. Here I show how 

$$ U_f(u,v) = \frac{A}{i \lambda f} \iint_{-\infty}^\infty t_A (\xi, \eta) \exp\left( -i\frac{2\pi}{\lambda f} (\xi u + \eta v)\right) d\xi d\eta$$
$$ \tilde{U}_f(\tilde{u}, \tilde{v}) = \frac{A}{i} \iint_{-\infty}^\infty \tilde{t}_A(\tilde{\xi}, \tilde{\eta}) \exp\left( -i 2\pi (\tilde{\xi} \tilde{u} + \tilde{\eta} \tilde{v})\right) d\tilde{\xi} d\tilde{\eta}$$
