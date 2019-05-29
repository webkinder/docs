
---
title: Umgang mit Bildern
date: 2019-05-29
publishdate: 2019-05-29
---

To improve the loading performance of our webpages we make use of responsive images. This can be done the following way.

## Guide
Include the macro at the very top of the `twig` templates.

#### `your-template.twig`
```twig
{% import 'macros/responsive-images.twig' as responsiveImage %}
```
### Use the macro
We can make use of the macro by executing its `displayResponsiveImage` function:
```twig
{{ responsiveImage.displayResponsiveImage(image) }}
```

> Notice: The above code will not work, since we haven't declared the `image` variable so far.

So let's do it!

```
{% set image = TimberImage(imageID) %}

OR

{% set image = post.thumbnail %}
```

`TimberImage` takes the image `ID` as a parameter and will take care of the data structure.

### Configuration
To gain more control over what's happening, we can create a customized configuration. To achieve this let's create the `options` object.

```twig
{% set options = {
    sizes: [
      { width: 1024 },
      { width: 768 },
    ],
    alt: 'logo',
    class: 'o-media',
    ratio: 16:9,
    dimensions: '100vw',
    webpEnabled: true,
    webpQuality: 90
} %}
```

> Notice: The above configuration is nonsense, since it holds the same values as the defaults.

Finally we can pass the `options` variable to the `displayResponsiveImage` method like this:
```
{{ responsiveImage.displayResponsiveImage(image, options) }}
```

Well done!
## API-Reference
### responsiveImage
The macros name, which is used to for the import.
#### displayResponsiveImage(image, options)
Method used to render the responsive image.

**image : number or TimberImage**

Takes the ID (from WordPress) of the image or a TimberImage to render.

**options : object**

Takes an object which holds all the customized config to render the image with.

Properties:

- sizes : array - Contains the different sizes used for the `srcset` property on the `img` element.
- alt : string - The alt attribute specifies an alternate text for an image, if the image cannot be displayed. Learn what to use right [here](https://www.w3.org/WAI/tutorials/images/decision-tree/).
- class : string - Holds a class which will be attached to the image.
- ratio : number - Holds the aspect ratio of the image. This describes the proportional relationship between its width and its height. 
- dimensions : array - The dimension array holds the value for the `sizes` attribute on the `img` element. These are just some breakpoints similar to media queries. You can learn more about them [here](https://blog.kulturbanause.de/2014/09/responsive-images-srcset-sizes-adaptive/).
- webpEnabled: boolean - Wheather webp should be enabled or not
