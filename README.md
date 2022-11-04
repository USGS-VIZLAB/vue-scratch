# vue-scratch
A vue app to for experimental viz work.

# How to use
This app is intended to provide scratch space to experiment with javascript- and web-based ideas. It is set up with some dependencies common to Vizlab (e.g. D3, gsap, svg-loader, and uswds) and a simple template to import components into and work from there. To use it:
1. Fork the repo and clone locally. 
1. Set up the repository to work locally. Run `npm install` from terminal within the repository to install dependencies.
1. If `npm install` is throwing errors, try to change your node version to `14.17.0` with `nvm`(https://github.com/nvm-sh/nvm)
1. Execute `npm run serve` in the terminal to run locally. This will allow you to view the page as you work. The default page is empty with a USGS Vizlab logo in the upper righthand corner.
1. Create and work in components. These are stored in `src/components/`. This will prevent conflicts if multiple people are working in the same repo. This is also a best practice for vue-based apps. [See this article](https://medium.com/@_shirish/thinking-in-components-with-vue-js-a35b5af12df) for an overview of working with Vue components.

To insert a component into the vue app you must register it as a component in `Visualization.vue`  like so:
```
<script>

export default {
    name: 'Visualization',
    components: {
      rain: () => import( /* webpackPreload: true */ /*webpackChunkName: "section"*/ "./../components/rain")
    },
} 
</script>
```

Once registered it can be used in the html template:
```
<template>
  <div id="visualization">
    <rain />
  </div>
</template>
```

Then you are ready to go!

# Best practices
1. Commit your components to this repository to help build a library of elements to use in future work. Components do not need to be perfect, use your discretion to decide whether or not it is worth keeping.
1. Do not commit changes to `Visualization.vue` or `App.vue` that are specific to your components. This should be kept clean for others to be able to easily step into and start working.
1. Update dependencies as needed.
1. Do not commit large data or image files. If a component depends on these, push them to the public S3 bucket and read in that way. Ideally all files be contained in AWS, but that may not be the case as we are in the early stages of development where scratch is needed. Provide comments on where files can be located if not in S3.
1. Provide documentation for reusable components stored in the repo below. This is not necessary for all scratch work, but will help us develop a collection of useful components and code examples as we continue to learn new things. 


# Component library

`ImgCarousel.vue`: A lightweight image carousel sourced from `vue-carousel`. This is used in the `Snow-to-flow` and `delaware-basin-story` visualizations to allow users to see a series of images and zoom in on selection. To use `main.js` needs to be modified to include `import VueCarousel from 'vue-carousel';` and `Vue.use(VueCarousel);`.  

`DA.vue`: An animated svg about data assimilation that demonstrates the use of `gsap` for a simple timeline animation. This depends on an external svg file `dasvg-01-01.svg`, which is imported via `svg-loader` and animated using `gsap`. The timeline animation is defined within the `initTime()` method. The final product can be seen here: https://twitter.com/USGS_DataSci/status/1431332579634991114/photo/1

`rain.vue`: A canvas-based animation of numbers falling like rain. Numeric inputs to customize the animation are annotated in the code. Uses flex positioning to fill screen.

`Sidebar.vue`: An expandable box used to define terms when clicked on. Can be seen in action in `snow-to-flow`. Useful for providing more information for those who are looking for it.

`VizSection.vue`: A template for a visualization that includes (1) a takeaway title, (2) figure(s), (3) a figure caption, and (4) slots for text explanations either above of below the figure. This was used for the repeating sections in `snow-to-flow`. Works well with `Figure.vue`. Classes `.maxWidth`, `single`, `.group`, `.two`, and `.three` can be added to figure elements to defien how they arrange within view.

`Figure.vue`: An image or figure template. Includes structure to include size and type options to fit the viewport and device type. 

`ImageZoom.vue`: A template for including a zoomable image. The image is zoomable with mouse scroll wheel, trackpad, touchscreen, or using zoom buttons. To use `main.js` needs to be modified to include `import VueZoomer from 'vue-zoomer';` and `Vue.use(VueZoomer);`:
  * <img src="https://user-images.githubusercontent.com/54007288/200002258-e21a3a77-67f6-47a7-b067-f346e1764d28.png" height="300">

`UseDialogCard.vue`: A template for including a pop-up dialog window that is triggered on click and is dynamically populated using loaded data. This component makes use of a base component `Dialog.vue` that includes placeholders for a title, description and image. The template in `UseDialogCard.vue` includes a few different examples of how to add click events to page elements to populate custom dialogs: via dynamically generated buttons, using single buttons inserted into text, and through interaction with d3-generated svg elements or text: 
  * The dialog:
    <img src="https://user-images.githubusercontent.com/54007288/200064327-a2be9d5a-7b18-4e7a-a1ee-7ba466fab10f.png" height="300">


## Disclaimer

This software is in the public domain because it contains materials that originally came from the U.S. Geological Survey, an agency of the United States Department of Interior. For more information, see the official USGS copyright policy at [http://www.usgs.gov/visual-id/credit_usgs.html#copyright](http://www.usgs.gov/visual-id/credit_usgs.html#copyright)

This information is preliminary or provisional and is subject to revision. It is being provided to meet the need for timely best science. The information has not received final approval by the U.S. Geological Survey (USGS) and is provided on the condition that neither the USGS nor the U.S. Government shall be held liable for any damages resulting from the authorized or unauthorized use of the information. Although this software program has been used by the USGS, no warranty, expressed or implied, is made by the USGS or the U.S. Government as to the accuracy and functioning of the program and related program material nor shall the fact of distribution constitute any such warranty, and no responsibility is assumed by the USGS in connection therewith.

This software is provided "AS IS."


[
  ![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png)
](http://creativecommons.org/publicdomain/zero/1.0/)
