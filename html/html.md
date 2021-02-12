<div align="center">
    <img src="https://img.icons8.com/color/96/000000/html-5.png" height="60"/>
    <h1>HTML</h1>
</div>

<h2>Table of contents<h2>

- [Element Vs Tag](#Element-VS-Tag)
- [H1-H6](#Headings)
- [Forms](#Forms)


<br>

## Element Vs Tag:

what is the difference between element and tag?

<details><summary><b>Answer</b></summary>

a tag can be opening tag like `<p>` or a closing tag like `</p>`

the combination of the opening and a closing tag is called an element

</details>

<br>

## Headings

- You should have one and only one h1 in your page
- you should have h2 in your page only if you already have h1
- you should have h3 in your page only if you already have h2 and so on ....
- you don't use headings for sizing your text this should be done with css

## Forms

we can associate a certain checkbox to it's label using ```for``` and ```id```, this doesn't just make difference in case of accessability for screenr eaders but also makes it easier to deal with forms in case you're using a smaller screen, it assigns the text to the checkbox so by clicking the text you're checking the assigned checkbox

```html
<div class="preference">
    <label for="cheese">Do you like cheese ?</label>
    <input type="checkbox" name="cheese" id ="cheese">
</div>

<div class="preference">
    <label for="peas">Do you like peas?</label>
    <input type="checkbox" name="peas" id ="peas">
</div>
```