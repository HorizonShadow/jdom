# jdom
Very tiny layer of abstraction over the DOM API to make things more legible and obvious.

Although this tiny library extends the DOM (which is not future-safe), the added features (which are only added upon the absence of that named method) are semantic and would more than likely match the functionality of any future additions to the DOM spec.

We recommend that you do not use this in production, however. You never know if a same-named method is added and does something entirely different than what I assume it will do.

Enjoy!

---

Example usage:
===

    // Removing any children of #myID that have a class of 'foo'
    document
      .find('#myID')
      .children
      .filter(element => element.className === 'foo')
      .remove();


    // Find all a tags, and disable their default behaviour on click
    document
      .findAll('a')
      .on('click', e => e.preventDefault());


    // Get/remove children of #foo then put them back, sorted.
    document
      .find('#foo')
      .children
      .remove()
      .sort((a, b) => ...)
      .forEach(function(element) {
        element.appendTo(document.find('#foo'));
      });
    

    // Append a new hr element to #foo
    document.body.find('#foo').appendChild(Element.create('hr'));
    

API:
===

document
---

- **`document.find`** : `Element`

Find a single element (Alias for `document.querySelector`):

    document.find(cssSelector);
    
---

- **`document.findAll`** : `NodeList`

Find multiple elements (Alias for `document.querySelectorAll`):

    document.findAll(cssSelector);
    
---

Element
---

- **`Element.create`** : `Element`

Create a new element (Similar to `Object.create`, Alias for `document.createElement`):

    Element.create(tagName);

---

- **`Element.prototype.appendTo`** : `Element`

Append an element to a specific parent ([Reverse] Alias for `Element.prototype.appendChild`):

    myElement.appendTo(parentElement);

---

- **`Element.prototype.find`** : `Element`

Find a single child of an element (Alias for `Element.prototype.querySelector`):

    myElement.find(cssSelector);

---

- **`Element.prototype.findAll`** : `NodeList`

Find multiple children of an element (Alias for `Element.prototype.querySelectorAll`):

    myElement.findAll(cssSelector);

---

- **`Element.prototype.on`** : `Element`

Add an event listener to an element

    myElement.on(eventName, callback);

---

- **`Element.prototype.remove`** : `Element`

Already a feature in modern browsers; removes element from DOM
(https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove)

    myElement.remove();
    
---

Array
---

- **`Array.of`** : `Array`

ES6 feature that creates an array of ___; Used in *jdom* to transform a NodeList/HTMLCollection into an Array
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/of)

    Array.of(myNodeList);
    
---

- **`Array.prototype.filter`** : `Array`

Already a feature in modern browsers; filters an array
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

    myArray.filter(function(item, i, array) {
        ...
    }, bound);
    
---

- **`Array.prototype.forEach`** : `undefined`

Already a feature in modern browsers; iterates over Array
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

    myArray.forEach(function(item, i, array) {
        ...
    }, bound);
    
---

NodeList
---

- **`NodeList.prototype.forEach`** : `undefined`

Iterates over a NodeList
(see `Array.prototype.forEach`)

    myNodeList.forEach(function(element, i, nodelist) {
        ...
    }, bound);

---

- **`NodeList.prototype.remove`** : `NodeList`

Removes all elements in a NodeList from the DOM
(see `Element.prototype.remove`)

    myNodeList.remove();

---

- **`NodeList.prototype.appendTo`** : `NodeList`

Appends elements in the NodeList to a specified parent
(see `Element.prototype.appendTo`)

    myNodeList.appendTo(parentElement);
    
---

- **`NodeList.prototype.on`** : `NodeList`

Adds an event listener to each item in the NodeList
(see `Element.prototype.on`)

    myNodeList.on(eventName, callback);
    
---

- **`NodeList.prototype.filter`** : `NodeList`

Filters the NodeList for given rules
(see `Array.prototype.filter`)

    myNodeList.filter(filterCallback);
    
---

- **`NodeList.prototype.sort`** : `Array`

Converts NodeList to array and then sorts it
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

    myNodeList.sort(function(a, b) {
        ...
    });
    
---

HTMLCollection
---

Uses the exact same functions as NodeList. The only differences being that `remove`, `appendTo`, and `on` return an **`HTMLCollection`**. Otherwise, the return types are the same.
