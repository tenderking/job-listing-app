# Frontend Mentor - Job listings with filtering solution

This is a solution to the [Job listings with filtering challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/job-listings-with-filtering-ivstIPCt). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

**Note: Delete this note and update the table of contents based on what sections you keep.**

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the site depending on their device's screen size
- See hover states for all interactive elements on the page
- Filter job listings based on the categories

### Screenshot

![](./screenshot.jpg)

<!-- Add a screenshot of your solution. The easiest way to do this is to use Firefox to view your project, right-click the page and select "Take a Screenshot". You can choose either a full-height screenshot or a cropped one based on how long the page is. If it's very long, it might be best to crop it.

Alternatively, you can use a tool like [FireShot](https://getfireshot.com/) to take the screenshot. FireShot has a free option, so you don't need to purchase it.

Then crop/optimize/edit your image however you like, add it to your project, and update the file path in the image above.

**Note: Delete this note and the paragraphs above when you add your screenshot. If you prefer not to add a screenshot, feel free to remove this entire section.** -->

### Links

- Solution URL: [Add solution URL here](https://github.com/tenderking/job-listing-app)
- Live Site URL: [Live site URL](https://tenderking.github.io/job-listing-app/)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- CSS Grid
- Mobile-first workflow
- [Vuejs](https://vuejs.org/) - JS library
- [Quasar](https://quasar.dev/) - Vue framework

### What I learned

I learned to use a vue framework, use typescript, using json data file, learned about reactive components.

This code filtered the data, but the logic was faulty. It filtered by objects containing a filter word or another. But the goal was filtering objects by a filter word and then another. The difference becomes that the if the filter words were, html and css, the algorithm would show objects the word html, or css or both. The desired was to only show the objects with both html and css.

```js
let filteredResult = () => {
      const result3 = props.rows.filter((item) =>
        selected.value.some((val) => item.languages.includes(val))
      );
      const result1 = props.rows.filter((item) =>
        selected.value.some((val) => item.tools.includes(val))
      );
      const result2 = props.rows.filter((item) =>
        selected.value.some((val) => item.level.includes(val))
      );
      const result4 = props.rows.filter((item) =>
        selected.value.some((val) => item.role.includes(val))
      );
      const resultList = [result1, result2, result3, result4];
      //some arrays will be empty so we remove them here.
      let filteredResult = resultList.find((a) => a.length > 1);

      return filteredResult;
    };
}
```

<!-- ### Useful resources

- [Example resource 1](https://www.example.com) - This helped me for XYZ reason. I really liked this pattern and will use it going forward.
- [Example resource 2](https://www.example.com) - This is an amazing article which helped me finally understand XYZ. I'd recommend it to anyone still learning this concept.

**Note: Delete this note and replace the list above with resources that helped you during the challenge. These could come in handy for anyone viewing your solution or for yourself when you look back on this project in the future.** -->

<!-- ## Author

- Website - [Add your name here](https://www.your-site.com)
- Frontend Mentor - [@yourusername](https://www.frontendmentor.io/profile/yourusername)
- Twitter - [@yourusername](https://www.twitter.com/yourusername)

**Note: Delete this note and add/remove/edit lines above based on what links you'd like to share.** -->

<!-- ## Acknowledgments

This is where you can give a hat tip to anyone who helped you out on this project. Perhaps you worked in a team or got some inspiration from someone else's solution. This is the perfect place to give them some credit.

**Note: Delete this note and edit this section's content as necessary. If you completed this challenge by yourself, feel free to delete this section entirely.** -->

## Install the dependencies

```
npm install
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)

```
npx quasar dev
```

### Lint the files

```
npx run lint
```

### Build the app for production

```
npx quasar build
```

### Customize the configuration

See [Configuring quasar.conf.js](https://quasar.dev/quasar-cli/quasar-conf-js).
