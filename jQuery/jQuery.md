<div align="center">
  <img src="https://img.shields.io/badge/jquery%20-%230769AD.svg?&style=for-the-badge&logo=jquery&logoColor=white"/>
<h1>jQuery</h1>
</div>

<h2>Table of contents<h2>

- [Selectors](#Selectors)
- [Manipulation](#Manipulation)

<br>

## Selectors:

This is how we used to select elements in Javascript

```javascript
window.onload = function () {
	//any js selector
	document.getElementById('Example');
}; //end of loading
```

How we select the same element using jQuery

```javascript
 jQuery(document).ready(function(){

  //executed after page loading

  )//end of loading
```

similarly

```javascript
$(document).ready(function () {}); //end loading
```

How to select an element/tag with jQuery

```javascript
  $(function () {

    $(your-css-selector-here).action()

    //for example

    $("div").css("backgroundColor", "lightgreen"); //selection by tag name ... return all div in my page and change their background to lightgreen

    $("#example").css({ //selection by id ... changing multiple css properties

    //property name:property value
    backgroundColor: "red",
    margin         : "10px auto",
    padding        : "5px",
    color          : "blue",
    "text-align"   : "center"

    });

    $(".a").css("backgroundColor", "cyan"); // selection by class name

    $("*").css({ //universal selector
      margin: "10px",
      padding: "5px",
      'text-align': 'center
    })

  });
```

##### NB:

- elements with id are unique in your page, ie. you should have only one element with id example ... you can have multiple element with the same id but then your id is no longer a unique, we use classes for that case.

- the case is different in javascript, `document.getElementById()` returns only the first element it finds with the id given.

```js
document.getElementById('example'); //returns first elem with id example
```

```js
$(function () {
	$('li ,.a,#example').css({
		//different type of selector same css style
		backgroundColor: 'yellow',
		color: 'red',
	});

	$('div a').css({
		//select a tags inside that are inside divs
		border: '1px solid green',
		color: 'red',
		backgroundColor: 'lightgreen',
	});
});
```

### attribute selector

```js
$(function () {
	$('a[name]').css({
		// select all tags with name attribute
		backgroundColor: 'yellow',
	});

	$("a[href ^='http']").css({
		// select all a tags whose href attribute value starts with http
		backgroundColor: 'yellow',
	});

	$("a[href $='eg']").css('backgroundColor', 'blue'); // select all a tags whose href attribute value ends with eg

	$("a[href *='oo']").css({
		// select all a tags whose href attribute value contains with oo
		backgroundColor: 'lightgreen',
	});

	$('input[type=text]').css({
		// select all input tags whose type attribute value equals with text
		backgroundColor: 'green',
	});

	//grouping
	$("a[href *='oo'][name='']").css({
		// select all a tags whose href attribute value contains with oo & has an input attribute of value empty string
		backgroundColor: 'yellow',
	});
});
```

### form filter

```js
  $(function () {
    $("input[type=text]").css({
        backgroundColor: "green"
    })
    // form collection ... type //text,password,checked
    $(":text").css({ //the short form for input[type=text]
        backgroundColor:"yellow"
    })

    $(":checkbox")

    $(":submit")

    $(":file")

    $(":checked") //returns checked checkboxes, radio buttons and dropdown lists elements

    $(":selected") //:selected selector works for <option> elements ONLY!

    // filtering

    $("li").css({
        backgroundColor:"green"
    })
    $("li:first").css("backgroundColor","yellow") //first list element  in my whole page
    $("li:last").css({ //last list element  in my whole page
        backgroundColor:"red"
    }
    $("li:eq(3)").css({ //third list element in my whole page
        backgroundColor:"pink"
    })
    $("li:eq(-4)").css({ //forth list element from the end
        backgroundColor:"blue"
    }
    $("tr:first").css("backgroundColor","yellow") //first tr element in my whole page

    $("tr:first-child").css({ //all the tr that are first child of the table
        backgroundColor:"red"
    })

    $("li:last-child").css("backgroundColor","green") //all the li that are last child of the ul

    $("li:nth-child(2)").css({ // 2nd li element in all the uls in my page
        backgroundColor: "cyan"
    })

    //NB numbering starts from one in this case, first li element = 1, second = 2 ...etc

    $("li:nth-child(2n)").css({ //even li elements
        backgroundColor: "cyan"
    })

    $("li:gt(2)").css({ //all the li elements in my page after the 3rd li (the 3rd is not included) .. 0 = first, 1 = second, 2 = third
        backgroundColor: "red"
    })

    $("li:lt(2)").css({ //all the li elements in my page before the 3rd li (the 3rd is not included)
        backgroundColor: "yellow"
    })
  });
```

### node tree selector

```js
$(function () {
	$('div:empty').css({
		//divs with nothing in it no text, no comments N.O.T.H.I.N.G
		width: '120px',
		color: 'green',
		padding: '5px',
		margin: '10px auto',
		height: '100px',
		backgroundColor: 'yellow',
	});

	$('div:parent'); //divs that has other node elements inside it, text, space, enter, another element,comment

	// hierarchy selector
	// direct child,all instead child ,next sibling ,all next sibling

	$('div p').css('backgroundColor', 'green'); //all paragraphs inside div
	$('div > p').css({
		//all paragraphs that are direct child of the div
		backgroundColor: 'yellow',
	});

	$('table tr:first-child').css('backgroundColor', 'green'); // same as selecting ("tr:first-child")

	$('table td:first-child').css({ backgroundColor: 'cyan' }); //first td in each tr

	$('tr:even').css({
		backgroundColor: 'orange',
	});
	$('tr:nth-child(2n)').css({
		backgroundColor: 'cyan',
	});

	/*******************************************
	 * NB:
	 *
	 *  tr:nth-child(2n) is not the same as tr:even
	 *
	 * tr:nth-child(2n) deals with every table as a separate case,
	 * ie if there are 2 tables each consists of  3 rows
	 * tr:nth-child(2n) will color only the second row in each table
	 * tr:even will color the second row from the first table, the first
	 * and the last row of the second tables
	 ************************************************/

	$('img + input').css({
		// direct next sibling, the  1 input the comes right next to an image
		backgroundColor: 'yellow',
	});

	$('img ~ input').css('backgroundColor', 'green'); // all next sibling, all inputs who belong to the same parent as the as the img will be selected

	$("h1:contains('Hierarchy')").css({
		//select h1 that has text Hierarchy
		backgroundColor: 'green',
	});

	$('div:has(p)').css({
		//select div that has child p
		backgroundColor: 'lightgreen',
		width: '250px',
		margin: '10px auto',
		color: 'red',
	});
});
```

### Attributes

```js
$(function () {
	alert($('#example').html()); //returns all the html inside #example
	alert($('#example').text()); //returns only the text inside #example

	$('#example').html(
		"<p style='background-color:red;text-align:center'>new Paragraph</p>",
	); //setting  the html inside #example

	$('#example').text(
		"<p style='background-color:red;text-align:center'>new Paragraph</p>",
	); //replacing the text inside #example (won't render and will appear as a text)

	alert($(':text:first').val()); //returns first text input value

	$(':text:first').val('new data'); //setting the first text input value

	alert($('#example').val()); //no return as the div doesn't have a value property

	//getAttribute("name of attribute")
	//setAttribute("name of attribute","value")
	$('img:first').attr('src', 'tiger.gif');
	$('img:last').attr('src', '1.jpg');

	console.log($('img').attr('src')); //returns first src value it finds

	// NB: to get a property from jQuery collection you'll need to use a loop
	$('img').each(function (i, elem) {
		console.log($(elem).attr('src')); //return values inside src attr for all the imgs in my page
	});

	//use attr with events
	$('p:first').attr('onclick', function () {
		alert('attribute handle');
	});

	//adding and removing attributes
	$('p').attr('class', 'active');
	$('p').removeAttr('class');
});
```
```javascript
//selecting element in JS vs selecting element in jQuery

//selecting element in JS
$(function () {
	var allLIO= document.getElementsByTagName("li");
		for(var i=0;i<allLIO.length;i++){
			allLIO[i].onclick=function(){
				console.log(this.innerHTML);
			}
		}

	//selecting element in jQuery
	$("li").click(function () {
		console.log($(this).text());
	});
});
```
<br>
Adding events became easier as I no longer need to loop through my HTML collection to add event

```javascript
$(function () {
	$("li").mouseover(function () {
	// $(this).addClass("active");
	//  if ($(this).hasClass("active"))
	//      $(this).removeClass("active")
	//  else
	//      $(this).addClass("active")
	$(this).toggleClass("active");
	})
 });
```
##### NB:
* this refers to the element that triggered the event

```javascript
$(function () {
	//JS >>> selector.style.display="none"
	$("li").hide(2000).show(2000)
 });
```
##### NB:

* hide and show methods in jQuery accepts an interval of time to add a css like animation on your element
---

<br>

## Manipulation:

<br>

```html
<div class='a'>
  <div class='b'>b</div>
</div>
````

```javascript
//.append() puts data inside an element at last index
$('.a').append($('.c'));
```

```html
<div class='a'>
  <div class='b'>b</div>
  <div class='c'>c</div>
</div>
```

```javascript
//.prepend() puts the prepending elem at first index
$('.a').prepend($('.c'));
```

```html
<div class='a'>
  <div class='c'>c</div>
  <div class='b'>b</div>
</div>
```

```javascript
//.after() puts the element after the element
$('.a').after($('.c'));
```

```html
<div class='a'>
  <div class='b'>b</div>
</div>
<div class='c'>c</div>
```

```javascript
//.before() puts the element before the element
$('.a').before($('.c'));
```

```html
<div class='c'>c</div>
<div class='a'>
  <div class='b'>b</div>
</div>
```

![manipulators](https://i.stack.imgur.com/KatFd.png))

##### NB:
1. insertBefore() / insertAfter() / prependTo() / appendTo() works on the child not the parent!!! for example:

```javascript
$('.c').insertBefore($('.a'));
$('.c').prependTo($('.a'));
```
2. use .clone(true) to make a copy from an element and copy/inherit the event on it as well, without it you're just making a plain new element!!

```js
var firstLI = $("li:first");
$("#example").append(firstLI.clone(true)); //if firstLI had any events on it those events will be cloned
```

```javascript
$(function () {
	$("#RemoveElement").click(function () {
	DivObj=$("#example").empty(); //.empty() will empty all the text inside #example
	});

	//NB: we made DivObj a global variable here so we could use it again in the next function

	$("#Recover").click(function () {
		$("body").append(DivObj); //adds empty texted DivObj at the end of my body
	});

});
```

```javascript
$(function () {
	$("#example").hover(function () {
		$(this).toggleClass("active");
	})

	 DivObj = $("#example").remove();//same as applying display none in css, (DivObj won't have a copy events on #example)

	});

	$("#Recover").click(function () {
		$("body").append(DivObj); //adds DivObj with all it's text at the end of my body but without any events
	});

});
```

```javascript
$(function () {

	DivObj = $("#example").detach();//remove element with a copy of the events
});
$("#Recover").click(function () {
	$("body").append(DivObj);
});

});
```

