This is a patatap.com clone for practice purpose ONLY.

Press any key from A-Z to enjoy different sounds and the amazing visual effects that are provided by paper.js.

It's a clone of patatap website. It is built with howler.js and paper.js.

Some notes that I have taken while I was built this web sites:

Query Selector

In place of common selectors like class, id or attribute we can use document.querySelector or document.querySelectorAll as the substitution. The differences lie in:

  document.querySelector returns the first matched element
  document.querySelectorAll returns all matched elements as NodeList. It can be converted to Array using          Array.prototype.slice.call(document.querySelectorAll(selector));

If there are no elements matched, jQuery and document.querySelectorAll will return [] document.querySelector and null respectively.

Notice: document.querySelector and document.querySelectorAll are quite SLOW  use document.getElementById, document.getElementsByClassName or document.getElementsByTagName if you want to get a performance bonus.
```
1.0 Query by selector

// jQuery
$('selector');

// Native
document.querySelectorAll('selector');
1.1 Query by class

// jQuery
$('.class');

// Native
document.querySelectorAll('.class');

// or
document.getElementsByClassName('class');
1.2 Query by id

// jQuery
$('#id');

// Native
document.querySelector('#id');

// or
document.getElementById('id');
1.3 Query by attribute

// jQuery
$('a[target=_blank]');

// Native
document.querySelectorAll('a[target=_blank]');
1.4 Query in descendants

// jQuery
$el.find('li');

// Native
el.querySelectorAll('li');
1.5 Sibling/Previous/Next Elements

Sibling elements

// jQuery
$el.siblings();

// Native
Array.prototype.filter.call(el.parentNode.children, (child) =>
  child !== el
);
Previous elements

// jQuery
$el.prev();

// Native
el.previousElementSibling;
Next elements

// jQuery
$el.next();

// Native
el.nextElementSibling;
1.6 Closest

Return the first matched element by provided selector, traversing from current element to document.

// jQuery
$el.closest(selector);

// Native - Only latest, NO IE
el.closest(selector);

// Native - IE10+
function closest(el, selector) {
  const matchesSelector = el.matches || el.webkitMatchesSelector || el.mozMatchesSelector || el.msMatchesSelector;

  while (el) {
    if (matchesSelector.call(el, selector)) {
      return el;
    } else {
      el = el.parentElement;
    }
  }
  return null;
}
1.7 Parents Until

Get the ancestors of each element in the current set of matched elements, up to but not including the element matched by the selector, DOM node, or jQuery object.

// jQuery
$el.parentsUntil(selector, filter);

// Native
function parentsUntil(el, selector, filter) {
  const result = [];
  const matchesSelector = el.matches || el.webkitMatchesSelector || el.mozMatchesSelector || el.msMatchesSelector;

  // match start from parent
  el = el.parentElement;
  while (el && !matchesSelector.call(el, selector)) {
    if (!filter) {
      result.push(el);
    } else {
      if (matchesSelector.call(el, filter)) {
        result.push(el);
      }
    }
    el = el.parentElement;
  }
  return result;
}
1.8 Form

Input/Textarea

// jQuery
$('#my-input').val();

// Native
document.querySelector('#my-input').value;
Get index of e.currentTarget between .radio

// jQuery
$('.radio').index(e.currentTarget);

// Native
Array.prototype.indexOf.call(document.querySelectorAll('.radio'), e.currentTarget);
1.9 Iframe Contents

$('iframe').contents() returns contentDocument for this specific iframe

Iframe contents

// jQuery
$iframe.contents();

// Native
iframe.contentDocument;
Iframe Query

// jQuery
$iframe.contents().find('.css');

// Native
iframe.contentDocument.querySelectorAll('.css');
1.10 Get body

// jQuery
$('body');

// Native
document.body;
1.11 Attribute getter and setter

Get an attribute

// jQuery
$el.attr('foo');

// Native
el.getAttribute('foo');
Set an attribute

// jQuery, note that this works in memory without change the DOM
$el.attr('foo', 'bar');

// Native
el.setAttribute('foo', 'bar');
Get a data- attribute

// jQuery
$el.data('foo');

// Native (use `getAttribute`)
el.getAttribute('data-foo');

// Native (use `dataset` if only need to support IE 11+)
el.dataset['foo'];
```
