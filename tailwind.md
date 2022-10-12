---
author: Ilia Syrtsou
title: Tailwind CSS v3 Overview
github_issue_number: 1684
tags:
- css
- tailwind
date: 2022-10-08
---

[Tailwind](https://tailwindcss.com/) is a utility styling framework (or better said, css preprocessor) designed to ease a developer's life while developing with html and css.

It does so by introducing static and dynamic classes, which cover most of css instructions.
It is compilable and produces regular css with classes matching the ones used in your markup. Isn't it handy?
So let's quickly overview what's there in Tailwind that makes it such a pleasure to use.

### Don't leave html during development!

So firstly, with Tailwind you rarely switch between html and css.
Tailwind comes with a pack of classes like [flex](https://tailwindcss.com/docs/flex), [text-center](https://tailwindcss.com/docs/text-align), [m-5](https://tailwindcss.com/docs/margin), [p-5](https://tailwindcss.com/docs/padding) or [w-100](https://tailwindcss.com/docs/width), which mimic corresponding styling instructions in css.

### Classes with arbitrary values!

Despite having variety of included classes, often you'd need finer values for padding, margin, shadow or any other.
To support this, Tailwind enables you to use css units like px, %, em/rem or vh/vw in square brackets after the class.

```html
    <div class="m-[20px] p-[1.5rem] w-[90%]">Some great content</div>
```


### Apply style to specific screen sizes

Tailwind has a way to apply style for specific screen sizes.
It comes with a default (yet overridable) set:
*tailwind.config.js*
```javascript
module.exports = {
  theme: {
    screens: {
      'sm': '640px',
      // => @media (min-width: 640px) { ... }

      'md': '768px',
      // => @media (min-width: 768px) { ... }

      'lg': '1024px',
      // => @media (min-width: 1024px) { ... }

      'xl': '1280px',
      // => @media (min-width: 1280px) { ... }

      '2xl': '1536px',
      // => @media (min-width: 1536px) { ... }
    }
  }
}
```

Which you can use by prepending style instruction with either of them like the following:

*Screen modificators*
```html
    <div class="sm:m-[20px] p-[1.5rem] xl:w-[90%] w-100">Some great content</div>
```

That means for screens wider than 640px, the margin of 20px will be applied, and screens wider than 1280 get 90% width (with 100% for smaller ones).
Isn't it expressive and easy to read?

### Hover, focus, active and other states

Just like screen modificators, Tailwind allows for various pseudo-classes, which enable you to apply style only on hover, focus etc.

```html
    <button class="hover:bg-[#D2B48C] active:bg-[#FAFAD2]">Some hoverable active content</button>
```

### Use Tailwind to create expressive component-like classes!

It's possible to use tailwind classes in css, which gives a component-like incapsulation, like single class descriptor instead of multiple, per-state ones.

```css
    .button {
      @apply p-5 mx-2 border-gray-300 bg-red hover:bg-blue disabled:bg-grey
    }
```

Lets get down to some practice!

### Installation

In order to start using Tailwind in your project, in the project root lets create the file:

*tailwind.config.js*
```javascript
module.exports = {
  content: ["./wildcart/for/your/*.{html,js}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Then add the following at the top of the root css file:

*site.css*
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

It adds a built-in pack of classes for you to use in html.
Now continuosly compile it to css in terminal, in the folder where your tailwind.config.js resides.

```Shell Session
npx tailwindcss -i ./src/site.css -o ./dist/output.css --watch
```

Then include the output.css into the html header and feel free to use all the built-in classes outlined in the [Documentation](https://tailwindcss.com/docs/flex)!

There is a catch though.
In order to use classes with arbitrary values, Tailwind needs to scan your html files to create corresponding css instructions in the output.css.
The 'content' wildcard in tailwind.config.js does just that! So make sure it covers all the html files that you use calculated classes in.

Happy coding!