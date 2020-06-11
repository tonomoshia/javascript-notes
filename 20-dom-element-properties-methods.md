## The DOM: Element Properties and Methods

(thank you [Soumaya Ranjan Mohanty](https://www.notion.so/Beginner-JavaScript-e2ef045754d14e96b93791f638bbcaf6)) This will be the last one from him. :-(

If we do `console.dir` after selecting an element then we can see that the selected element is actually an object and we can see the object properties.

```jsx
const h2 = document.querySelector('h2');
console.dir(h2); 

//Output - We get many properties
```

We can use these properties as either *getters or setters.*

e.g *Getter:* `console.log(h2.textContent); // I am an h2.`

*Setter:* `h2.textContent = 'new h2 content';`

**Difference between *textContent* and *innerText:***

Suppose we have the following HTML:

```html
<h2>
	I am a heading.
	<style>
		h2 {
			color: red;			
		}
	</style>
</h2>
```

In JavaScript:

```jsx
const heading = document.querySelector('h2');

console.log(heading.textContent); // I am a heading. h2 {color: red; }
console.log(heading.innerText); // I am a heading.
```

Other example for above:

HTML:

```html
<h2>
	I am a heading.
	<span>
		I am hidden!
	</span>
</h2>

// We hide the span by display:none
<style>
	h2 span {
		display: none;	
	}
</style>
```

JavaScript:

```jsx
console.log(heading.textContent); // I am a heading. ↵ I am hidden!
console.log(heading.innerText); // I am a heading.
```

*innerText is aware of CSS styling.*

*innerHTML:*

```jsx
console.log(heading.innerHTML); // I am a heading. ↵ <span>I am hidden!</span>
```

*outerHTML:*

```jsx
console.log(heading.*outerHTML*); // <h2> I am a heading. <span>I am hidden!</span> <h2>
```

Example:

To add pizza(🍕) at the end:

- 

```jsx
pizzaList.textContent = `${pizzaList.textContent} 🍕`;
```

But the above method becomes slow for long text.

- Instead we can use `insertAdjacentText`:

```jsx
pizzaList.insertAdjacentText('beforeend', 🍕)
```

**Element vs node:**

Element: wrapped inside tags

Node: can be anything

```jsx
<p> //node //element
 "Hey" //node
 "there" //node
</p> //node //element
```

**Element properties & methods:** [https://developer.mozilla.org/en-US/docs/Web/API/Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)

**Node properties & methods:** [https://developer.mozilla.org/en-US/docs/Web/API/Node](https://developer.mozilla.org/en-US/docs/Web/API/Node)