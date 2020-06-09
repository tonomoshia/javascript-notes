# Document Object Model

(thank you [Soumaya Ranjan Mohanty](https://www.notion.so/Beginner-JavaScript-e2ef045754d14e96b93791f638bbcaf6))

## The DOM: Intro to the document

JavaScript is used in all kinds of places. The most popular way we get introduced to JS is through web browser.

When we view HTML in the browser, the browser turns the HTML into the DOM: Document Object Model. We can see the DOM in the Elements tab in Dev Tools.

We can interact with the DOM like listening for clicks, add/remove elements from the DOM, fetch new data, play music and video etc. using JavaScript.

**The *window:***

- Global scope of browser
- All global variables are stored.
- Helpful properties like `location, innerWidth` present on *window* object.
- It is everything about the currently open window including the browser bar, tabs, scrollbars etc.

**The *document:***

- Responsible for everything from `<html>` to `</html>`
- Not concerned with tabs, scrollbar, browser bar etc.

**The *navigator:***

- Higher level than window.
- gives info about the browser and the device that it's on
- things like webcam, audio access, battery level, GPS and other device specific features live on navigator.

## The DOM: Selecting elements on the page

**Where to load JavaScript if we are selecting elements on the page?**

Always load it before the closing *body* tag (`</body>`). It is because, we need to have all elements before we start selecting them in JavaScript. We get `null` if we try to grab elements placing the `<script>` tag in the *head* because the elements are not yet created when the JavaScript is run.

*Other option: (to use in `<head>` tag)*

- use defer and async
- we can listen for the `DOMContentLoaded` event and then try to select elements from the page.

*Best way:* Load the JS before the `</body>` tag.

- **querySelector:** Returns first match

    ```jsx
    const p = document.querySelector('p');
    ```

- **querySelectorAll:** Returns all matches as a *NodeList (like array but without array helper functions)*

    ```jsx
    const p = document.querySelectorAll('p');
    ```

In **querySelector and querySelectorAll,** the argument we pass is nearly similar to CSS Selectors.

We can use things like:

- `.item` (element with class of item) or `div.item` (div with class of item) etc.
- **Parent-child selector:** *e.g. to grab images inside div with class item*

    `const img = document.querySelector('.item img');`

```html
<div class="items">
	<div class="item item1">
		<img src="http://img1.com" >
	</div>
	<div class="item">
		<img src="http://img2.link" >
	</div>
</div>

```

In above HTML, suppose if we want just the first item and find the image inside of the item.

We have 2 options:

1. `document.querySelector('item img');`
2. 

```jsx
const item1 = document.querySelector('.item1');
const item1Img = item1.querySelector(img); //important
```

*Note:* We also have dated/old ways of selecting elements from DOM like `getElementById`, `getElementsByClassName`, `getElementsByTagName` etc.