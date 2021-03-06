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