This documentation of how to make a basic article using Sveltekit! A little disclaimer though, I am NOT an expert by any means, I only just learned about how to use Sveltekit and I wanted to document it for other people's use. I am trying to make this tutorial as *beginner friendly as possible*, but I won't really be explaining everything that I am doing. If you want more information on some parts of the tutorial, parts of how to reconfigure svelte is directly from [philkruft's article](https://www.philkruft.dev/blog/how-to-build-a-static-sveltekit-site/) and later I will be using sadgrl's [layout generator](https://sadgrl.online/projects/layout-builder/) to show you how I repurposed a template into Sveltekit

## Why use Sveltekit?

Sveltekit has a very useful tool called a "Static Site Generator." This tool **automates** the process of coding individual HTML pages. For example, when making a static website, if you want to change the navigation bar of 1 place, you would have to change the navigation bar **everywhere**, which can get pretty tiresome! With a Static Site Generator, you don't need to do that!

The only other reason why I'm using Sveltekit and not any of the other Static Site Generators is because it was the first name I saw when looking up how to make a web site. Fortunately, I have found using Sveltekit *pretty easy* to get used to. If I hadn't, I probably would have given up and not made this tutorial.

## How to install Sveltekit

First, you're going to want an IDE to make this website! I use Visual Studio Code. https://code.visualstudio.com/

Also, you're going to need to install Node.js (current version) https://nodejs.org/en
### Creating a new site

Once you created that, it's time to open up the terminal.

![Pasted image 20231208043756](https://github.com/CrocScore/neocities-sveltekit/assets/126017457/22ae29d0-fb3b-494c-874e-2dd87f282d67)
Write this into the terminal
```
npm create svelte@latest my-first-site
```

Use arrow keys to select "Skeleton project." I'm not personally proficient in typescript, so this tutorial will all be using javascript. Select "no" for the second option. All the other options are optional for this tutorial, and I encourage you to read about their use cases, but it doesn't matter what you pick here.

![Pasted image 20231208044536](https://github.com/CrocScore/neocities-sveltekit/assets/126017457/9cd03ce6-3389-4f17-877d-ff2f0ce7532b)
Now that the folder has been created with your project, type these commands one after another
```terminal
cd my-first-site
npm install
npm run dev -- --open
```
After doing these steps, a webpage should open with your new website!
### Creating subpages

To create subpages, we are going to go into the basics of sveltekit's routing. 

Going into the files, your src file should look like this:

```
📂 src
┣ 📂 routes
┃ ┗ 📄 +page.svelte
┗ 📄 app.html
```
To create subpages ( ./ endings), all you need to do is to make folders under the routes folder, and put a +page.svelte file under each subpage folder.

For example:

```
📂 src
┣ 📂 routes
┃ ┣ 📂 example1
┃ ┃ ┗ 📄 +page.svelte
┃ ┣ 📂 example2
┃ ┃ ┗ 📄 +page.svelte
┃ ┣ 📂 example3
┃ ┃ ┗ 📄 +page.svelte
┃ ┗ 📄 +page.svelte
┗ 📄 app.html
```

will give you these routes:
```
/
/example1
/example2
/example3
```

Under the routes folder, create a +layout.svelte file. What you put in this file will persist in all your websites. For now, I am going to be using basic navigation as an example:
```html
<!-- in +layout.svelte -->
<nav>
    <a href="/">Home</a>
    <a href="example1">example1</a>
    <a href="example2">example2</a>
    <a href="example3">example3</a>
</nav>

<slot/>
```

By putting
```<slot/>```
In the +layout.svelte, you're now able to have unique content placed under the navigation for each page! 

For example, you can add this to the +page.svelte in under the "example1" folder
```html
<h1>Hello world!<h1>
```

Navigate over to example1, and now you see the "hello world" there. Neat!

By using the tools the Sveltekit gives you, It becomes simple to repurpose layouts without having to make changes to every layout.
### Repurposing a layout
Go ahead and use sadgrl's layout builder and make your own layout. https://sadgrl.online/projects/layout-builder/

I just did the default presets, but this tutorial should work with any layouts (even others you find on the internet!)

First things first, we will want to separate that is under the "style" html tag.

Copy everything that is enclosed in these: 
```<style></style>```


Then in src, make a "global.css" file, and paste everything inside of the ```<style></style>``` into it.

![Pasted image 20231208053327](https://github.com/CrocScore/neocities-sveltekit/assets/126017457/a5f8cd02-00be-492d-b96c-ad8f3b5e625f)

now got into routes/+layout.svelte and put only the html in there (no style/css).

![Pasted image 20231208053706](https://github.com/CrocScore/neocities-sveltekit/assets/126017457/67532603-dc8a-4d79-a96b-730dcec345cf)

We are going to change the navbar back to what it was before, so change

```html
<nav id="navbar">
	<ul>
		 <li><a href="#">Home</a></li>
		 <li><a href="#">Link</a></li>
		 <li><a href="#">Link</a></li>
		 <li><a href="#">Link</a></li>
		 <li><a href="#">Link</a></li>
		 <li><a href="#">Link</a></li>
	</ul>
</nav>
```
to
```html
<nav id="navbar">
	<ul>
		 <li><a href="/">Home</a></li>
		 <li><a href="/example1">Example1</a></li>
		 <li><a href="/example2">Example2</a></li>
		 <li><a href="/example3">Example3</a></li>
	</ul>
</nav>
```

Another important thing is that at the top of the page, we need to tell the webpage to load in the css!

```
<!--At the top of routes/+layout.svelte->
<script>
    import "../global.css";
</script>
```

Now the layout should display like this

![Pasted image 20231208055727](https://github.com/CrocScore/neocities-sveltekit/assets/126017457/6cfa656d-531d-4188-b777-00c1054a5a97)

Now in order to change the contents of what's inside of the main (middle of the layout), we can ```<slot/>``` again. 
Remove all of the contents of main
```html
<main>
	<h1>Welcome to my Layout Maker!</h1>
	<p><strong>Please read this first!</strong></p>
	<p>This tool generates a layout that is responsive, which means it looks great on phones! Use dropdowns above to customize your layout's general features. Click the button to generate your HTML and CSS, and paste it into a file on Neocities.</p>
	!--.. the rest of the main-!
</main>
```

and then replace main with ```<slot/>```.

```html
<main>
	<slot/>
</main>
```

Now anything you put in any of the +page.svelte files, will display in the main! For example, if you put "Hello world!" in example1...

![Pasted image 20231208060834](https://github.com/CrocScore/neocities-sveltekit/assets/126017457/ebd48b9e-03f0-4e4d-9129-99b6cfa7adba)

There it is!

Now, how about having persisting sidebars? Luckily, that's easy to do as well!

back in +layout.svelte, take a look at
```html
<aside id="leftSidebar">
            <h2>Updates</h2>
            <div class="box">
                <p>I have recently updated this tool as of August 2022!</p>
                <ul style="padding-left:10px;">
                    <li>Rewrote the JS to generate cleaner code</li>
                    <li>Rewrote the CSS in a way that hopefully makes much more sense to edit</li>
                    <li>Added a couple of new features!</li>
                    <li>Old version is still available <a href="old.html" target="_blank">here</a></li>
                </ul>
            </div>
            <h2>Hi there!</h2>
            <p>Do you have a suggestion for a feature? Some criticism about the tool or something that confused you? Let me know! sadgrl[at]riseup.net</p>
            <h3>Other Tools</h3>
            <ul>
                <li><a href="https://sadgrlonline.github.io/html-cheatsheet/" target="_blank">HTML Cheatsheet</a>
                </li><li><a href="https://sadgrl.online/webmastery/webmaster-links.html" target="_blank">Webmaster Links</a></li>
                <li><a href="https://sadgrl.online/webmastery/downloads/tiledbgs.html" target="_blank">Tiled BGs</a></li>
                <li><a href="https://sadgrl.online/webmastery/downloads/fonts.html" target="_blank">Fonts</a></li>
                <li><a href="https://sadgrl.online/projects/ideas/" target="_blank">Site Ideas</a></li>
            </ul>
</aside>
```

under the routes folder, make a new file called "leftSidebar.svelte", and copy over everything between
```
<aside id="leftSidebar">
</aside>
```

Your website should look like this
![Pasted image 20231208135031](https://github.com/CrocScore/neocities-sveltekit/assets/126017457/66402900-027c-491f-8be6-5371b720d139)

now go to the top of +layout.svelte and add ```import LeftSidebar from "./leftSidebar.svelte";``` to the script.


```html
<script>
	import "../global.css";
	import LeftSidebar from "./leftSidebar.svelte";
</script>
```

Then go back to the leftSidebar area and add ```<LeftSidebar />```
```html
<aside id="leftSidebar">
	<LeftSidebar />
</aside>
```

And now the left side bar is back! (if you copied over the contents from before, if you want you can change it now) Let's go ahead do the same the rightSidebar as well. Copy all the contents from rightSidebar into a newly made routes/rightSidebar.svelte


```html
!--Top of +layout.svelte-!
<script>
	import "../global.css";
	import LeftSidebar from "./leftSidebar.svelte";
	import RightSidebar from "./rightSidebar.svelte";
</script>
```

```html
<aside id="rightSidebar">
	<RightSidebar />
</aside>
```

And now, +layout.svelte should just look like this
```html
<script>
    import "../global.css";
    import LeftSidebar from "./leftSidebar.svelte";
    import RightSidebar from "./rightSidebar.svelte";
</script>

<div id="container">
    <div id="headerArea">
        <div id="header"></div>
        <nav id="navbar">
            <ul>
                 <li><a href="/">Home</a></li>
                 <li><a href="/example1">Example1</a></li>
                 <li><a href="/example2">Example2</a></li>
                 <li><a href="/example3">Example3</a></li>
            </ul>
        </nav>
    </div>

    <div id="flex">
        <aside id="leftSidebar">
            <LeftSidebar />
        </aside>
        <main>
            <slot></slot>
        </main>
        <aside id="rightSidebar">
            <RightSidebar />
        </aside>
    </div>
    <footer id="footer">CC0 Public Domain, 2022</footer>
</div>
```

### Settings needed for making the site fully static

We are going to need some dependencies to make a completely static site (which is required for Neocities!) Go back to your terminal (ctrl+c to close the site) and type this command:
```
npm install -D @sveltejs/adapter-static
```

now go to your /svelte.config.js file (under the original name file) and change the adapter.
```js
// change this part of the code
import adapter from '@sveltejs/adapter-auto';
// to this
import adapter from '@sveltejs/adapter-static';
```

Go back to your routes file and make a file called "+layout.js". Inside of that file, put this piece of code in:
```js
export const prerender = true;
export const trailingSlash = 'always';
```

You're now able to build your website for Neocities! In your terminal again, you can use
```
npm run build
```
The files will show up in the "build" folder, and now you can just directly upload those files into neocities!

I hope you enjoyed this tutorial. Everything that was shown will be on my github here. Feel free to ask question or let me know if anything breaks. You can also ask ChatGPT and it can generally point you in the right direction. If you found this tutorial at all helpful, consider supporting me financially. You can't exactly right now, but I'll be setting up a Ko-fi eventually. Thank you for reading, and have a nice rest of your day 😁
