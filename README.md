# Vue Style Transfer :art:
Easily use Style Transfer in your Vue Application


![Style transfer demo - Vue logo crossed with Starry Night by Vincent van Gogh](https://i.imgur.com/MPjGcOe.gif)

Style transfer demo - Vue logo crossed with Starry Night by Vincent van Gogh

![Style transfer explained](https://i.imgur.com/5CAIMbC.png)

## Philosophy
Lately, Style Transfer models have improved in their results and also decreased in size (down to a few KB).  At the same time, users' machines and devices have also become more powerful, and for the first time, able to perform style transfer computations on-the-fly. 

Vue Style Transfer was created with the goal of allowing you to seamlessly integrate state of the art style transfer neural network models in your website application.  This creates an opportunity to delight your users with new kinds of, refreshing, image graphics which are uniquely generated client-side every page visit.

Using Vue Style Transfer should be as simple as using any other HTML element like `<img>` or `<hr>`.

## Features
- Transform images with a state-of-the-art arbitrary style transfer model
- Use local images or images from direct URL's
- "loading image" screen is shown on the page until style transfer is completed
- Specify loading message text and background colors
- Set the "strength" of the style transfer
- Basic accessibility support via `aria-label`
  
## Setup/Installation :floppy_disk:
Install via NPM:
```bash
npm install --save vue-style-transfer
```

Configure your application entry point (typically `main.js`) and tell vue to use it:
```javascript
import Vue from 'vue'
import App from './App.vue'
import VueStyleTransfer from 'vue-style-transfer'

Vue.use(VueStyleTransfer)

new Vue({
  render: h => h(App),
}).$mount('#app')

```

## Usage :beginner:

**Background**

`originURL` or `local-origin-image` - the original image you want to add styling to.  Either from a URL or a local image.

`styleURL` or `local-style-image` - the image you want to copy the style from.  Either from a URL or a local image.

**Examples**

Basic example (using direct URL's only):
```html
    <style-transfer-element
      width="400"
      height="400"
      alt-text="Space Force snapshot crossed with Starry Night"
      originURL="http://i.imgur.com/Jm3bQtu.jpg"
      styleURL="http://i.imgur.com/osSv3S2.jpg"
      :strength="0.1"
      >
    </style-transfer-element>
```
Basic example (using a local origin image + URL for the style image):
```html
    <style-transfer-element
      width="400"
      height="400"
      alt-text="Vue logo crossed with Starry Night"
      :local-origin-image="require('../assets/logo.png')"
      styleURL="http://i.imgur.com/osSv3S2.jpg"
      :strength="0.1"
      >
    </style-transfer-element>
```

## Configuration Properties :wrench:

`:strength` - the strength of the style you want to apply to the origin image

`alt-text` - provide an alt text value for accessibility support.  Note: the final image is outputted in a canvas, which does not support alt tags.  Instead `aria-label` is used.

`width` and `height` - specify the dimensions of the style transfer output.  Please note, currently, larger sizes (eg. > 400px) can seriously slow down your application and even crash the user's browser.

`loading-background-color` - specify a hex value for the background (by default it's grey `#e8e8e8`)

`loading-text-message` - specify a custom string message to show to the user while the style transfer is working (by default it says, 'LOADING IMAGE')

`loading-text-color` - specify a hex value for the loading (by default it's dark grey `#666666`)

## About the Arbitrary Style Transfer Neural Network Model
Tensorflow.js Model taken from the [arbitrary-image-stylization-tfjs](https://github.com/reiinakano/arbitrary-image-stylization-tfjs) project.

Parts of the model which are called:

separableTransformNet (151 KB) - [Link](https://raw.githubusercontent.com/reiinakano/arbitrary-image-stylization-tfjs/master/saved_model_transformer_js/model.json)

mobileStyleNet (168 KB) - [Link](https://raw.githubusercontent.com/reiinakano/arbitrary-image-stylization-tfjs/master/saved_model_style_js/model.json)


## Warning :warning:
Please avoid using very large images as they have the potential to dramatically slow down your website or even crash the user's browser.  Also, please note, this library still has the potential to crash older machines (especially those without a GPU).  

It is **not recommended** to use this library in the main areas of critical, production website applications.

It is **not recommended** to use multiple style transfer elements on the same page.

## Credits
Please note the code is **very** heavily inspired from the original [Arbitrary Style Transfer code](https://github.com/reiinakano/arbitrary-image-stylization-tfjs) using Tensorflow.js by Reiichiro Nakano.  It's worth noting `vue-style-transfer` is more of a Vue wrapper for the original code by Reiichiro Nakano, than its own library.

Arbitrary Style Transfer itself would not have been possible without the following:
* Authors of the [arbitrary style transfer](https://arxiv.org/abs/1705.06830) paper.
* The Magenta repository for [arbitrary style transfer](https://github.com/tensorflow/magenta/tree/master/magenta/models/arbitrary_image_stylization).
* Authors of [the MobileNet-v2 paper](https://arxiv.org/abs/1801.04381).
* Authors of the paper describing [neural network knowledge distillation](https://arxiv.org/abs/1503.02531).
* The [TensorFlow.js library](https://js.tensorflow.org).
* [Google Colaboratory](https://colab.research.google.com/), with which I was able 
to do all necessary training using a free(!) GPU.
