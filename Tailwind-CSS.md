# Tailwind-CSS

> See [Tailwind official documentation](https://tailwindcss.com/docs/installation)
## Index

[Introduction](##Introduction)

[How-to-use-it-in-your-code](##How-to-use-it-in-your-code)
- [Link-in-your-HTML](###Link-in-your-HTML)
- [Tailwind-Cli](###Tailwind-Cli)
## Introduction

If you are looking for a "CSS framework" to simplify your styling, but you want to have the same control over your CSS that you'd have in vanilla CSS, you'll need to use [Tailwind](https://tailwindcss.com/).

Tailwind is a CSS "framework" which provides utility classes, and some "shortcuts" to style quickly and maintaining things consistent and clean through your website.

With "utility classes" we are indicating classes that modify only few (but mostly just one) parameter of the element (E.g. the background color, the width etc...).

## How-to-use-it-in-your-code

These methods are independents from the back-end/front-end technology that you are using. Check the documentation of the framework that you are using, or take a look of [this list](https://tailwindcss.com/docs/installation/framework-guides) and use the method specified for that if it is present.

### Link-in-your-HTML

>[!Important]
>Avoid this method if possible

just copy this line in your page:
```html
<script src="https://cdn.tailwindcss.com"></script>
```

### Tailwind-Cli

> you need to install [npm](https://nodejs.org/en/download/package-manager) 
> if you are on windows and not using WSL use [this link](https://nodejs.org/en/download/prebuilt-installer) instead

Run the following commands in your terminal:
```
npm install -D tailwindcss
npx tailwindcss init
```

Then edit your config based on your project structure:
![[###Basic-config]]

And add this to the end of your CSS file:
``` css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Now from your IDE run this command when you start programming (It automatically "senses" the changes in your files and compiles them):
```
npx tailwindcss -i <pathToInput>/<filename>.css -o <pathToOutput>/<fileName>.css --watch     
```


## Config.js

### Basic-config

Inside `content` you need to put the paths to the files that have tailwind classes inside.
ReEx are supported and should be used.

Generic configuration used in the official documentation:
```js

/** @type {import('tailwindcss').Config} */ 

module.exports = { 

	content: [
		"./src/**/*.{html,js}",
		/*
		others,
		...,
		others
		*/
	], 
	
	theme: { 
		extend: {}, 
		}, 
		plugins: [], 
	}
```