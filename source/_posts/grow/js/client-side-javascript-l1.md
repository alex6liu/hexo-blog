---
title: client side javascript l1
date: 2019-05-14 15:53:26
tags: [js, l1]
---

## Events Handling

### Event Phases

- The **capture phase** comprises all the DOM elements on the trip from the Document to the parent of the target element on which an event was triggered. In other words, when everything from the Document to the target, not including the target itself.
- The **target phase** occurs when the event reaches the target. Then event fired on the target, before reversing and retracing its steps, propagating back to the outermost Document.
- The **bubbling phase** comprises all the DOM elements encountered on the return trip from the target back to the Document. Bubbling gives the freedom of handling an event on any element by its parent elements.

### Know Event phases
### Be able to explain difference between capturing and bubbling

Event bubbling and capturing are two ways of event propagation in the HTML DOM API, when an event occurs in an element inside another element, and both elements have registered a handle for that event. The event propagation mode determines in which order the elements receive the event.

- With bubbling, the event is first captured and handled by the innermost element and then propagated to outer elements.

- With capturing, the event is first captured by the outermost element and propagated to the inner elements.

We can use the `addEventListener(type, listener, useCapture)` to register event handlers for in either bubbling (default) or capturing mode. To use the capturing model pass the third argument as `true`.

### Event Listeners

```js
buttonElement.addEventListener('click', function (event) {
  alert('Element clicked through function!');
});
```

### Be able to handle events
### Be able to create custom events

```js
var event = new Event('build');

// Listen for the event.
elem.addEventListener('build', function (e) { /* ... */ }, false);

// Dispatch the event.
elem.dispatchEvent(event);
```

### Be able to trigger events (both built-in and custom)

## AJAX

### XMLHttpRequest
### Know HTTP protocol basics
### Know AJAX concept
### Know how XMLHttpRequest works
### Understand AJAX security policy
### Be able to explain difference between AJAX request and Form submit

A standard form submit sends a new HTTP request (POST or GET) and loads the new page in the browser. In Ajax, the data is sent to the server (POST or GET) in the background, without affecting the page at all, and the response is then received by javascript in the background, again without affecting the page at all.

### Be able to create AJAX request (set content type, set response type, set custom headers)

`xhr.responseType = 'json';`

`xhr.setRequestHeader('Content-Type', 'application/json');`

### Be able to process AJAX response (parse response data)

```js
function loadDoc() {
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            document.getElementById("demo").innerHTML =
            this.responseText;
       }
    };
    xhttp.open("GET", "ajax_info.txt", true);
    xhttp.send(); 
}
```

### Be able to handle AJAX errors (including error codes)

```js
let xhr = new XMLHttpRequest();

xhr.open('GET', '/article/xmlhttprequest/hello.txt', false);

try {
  xhr.send();
  if (xhr.status != 200) {
    alert(`Error ${xhr.status}: ${xhr.statusText}`);
  } else {
    alert(xhr.response);
  }
} catch(err) { // instead of onerror
  alert("Request failed");
};
```

### [fetch]
### [$.ajax]

## Cross-Domain Communication

### JSONP

The important thing to remember with jsonp is that it isn't actually a protocol or data type. Its just a way of loading a script on the fly and processing the script that is introduced to the page. In the spirit of JSONP, this means introducing a new javascript object from the server into the client application/ script.

### Know JSONP prerequisites
### Be able to create JSONP request

```js
function clickButton() {
  var s = document.createElement("script");
  s.src = "demo_jsonp.php";
  document.body.appendChild(s);
}
```

### Be able to process JSON response
### Be able to explain difference between JSONP and AJAX

By default, Ajax requests have to occur in the same domain of the page where the request originates. JSONP - "JSON with padding" - was created to allow you to request JSON resources from a different domain. (CORS is a newer and better alternative to JSONP.)

## DOM Manipulation

### Selectors
### Know various types of selectors
### Understand selectors impotency and specifity
### Know how to find and select the certain elements in DOM
### Be able to discover selectors performance issues, limitations and optimizations
### Traversing
### Know how to traverse DOM tree vertically (parent, childNodes)
### Know how to traverse DOM tree horizontally (siblings)
### Be able to discover traversing performance and optimizations
### Modification
### Be able to add/remove/update DOM elements

- add
  - `document.createElement('p');`
  - `paragraph.textContent = "I'm a brand new paragraph.";`
  - `paragraph.innerHTML = "I'm a paragraph with <strong>bold</strong> text.";`
- remove
  - `todoList.removeChild(todoList.lastElementChild);`
  - `todoList.children[1].remove();`
- update
  - `todoList.appendChild(newTodo);`
  - `parentNode.insertBefore(newNode, nextSibling);`
  - `parentNode.replaceChild(newNode, oldNode);`

### Know DOM modification performance issues and bottlenecks

DOM操作会导致一系列的重绘（repaint）、重新排版（reflow）操作。为了确保执行结果的准确性，所有的修改操作是按顺序同步执行的。大部分浏览器都不会在JavaScript的执行过程中更新DOM。相应的，这些浏览器将对对 DOM的操作放进一个队列，并在JavaScript脚本执行完毕以后按顺序一次执行完毕。也就是说，在JavaScript执行的过程，直到发生重新排版，用户一直被阻塞。

一般的浏览器中（不含IE），repaint的速度远快于reflow，所以避免reflow更重要。

### Understand DOM optimizations
### Live Collections

## Events Basics

### DOM Events
### Know Event concept
### Know basic Event types
### Mouse / Keyboard Events
### Form / Input Events

## Events Propagation / Preventing

### Know Event propagation cycle

- bubbling
- capturing

### Know how to stop Event propagation

`event.stopPropagation()`

### Know how to prevent Event default browser behavior

`event.preventDefault()`

### Delegating

事件委托 是将事件监听添加到父元素，而不是每个子元素单独设置监听器，当触发子元素时，事件会冒泡到父元素，监听器就会触发。

### Understand Event delegating concept
### Understand Event delegating benefits and drawbacks

[link](http://tgsx.github.io/2017/08/02/%E4%BA%8B%E4%BB%B6%E5%A7%94%E6%89%98%E7%9A%84%E4%BC%98%E7%BC%BA%E7%82%B9/)

优点：

1.减少事件注册，节省内存，如：

- table可以代理所有td的click事件
- ul代理所有li的click事件

2.减少了dom节点更新的操作，处理逻辑只需在委托元素上进行，如：

- 新添加的li不用绑定事件
- 删除li时，不需要进行元素与处理函数的解绑

缺点：

1.事件委托基于冒泡，对于onfoucs和onblur等事件不支持
2.层级过多，冒泡过程中，可能会被某层阻止掉（建议就近委托）

总之一切都是基于冒泡的，只要事件不支持冒泡或者中途有event.stopPropagation（）等，那么委托就会失败，所以并不适用于直接在document上进行委托。

### Be able to implement Event delegating

## Global object window

### Location

The `Window.location` read-only property returns a `Location` object with information about the current location of the document.

The `Document.location` read-only property returns a `Location` object, which contains information about the URL of the document and provides methods for changing that URL and loading another URL.

### Know browser location structure
### Be able to explain client and server side navigation concept
### History API (Global object window)
### Know browser history concept
### Be able to navigate within browser history
### Be able to use history state
### Be able to replace history state
### Navigator
### Know how to parse user agent
### Know how to discover client platform, browser
### Document
### Screen
### Cookies
### Know cookie concept and limitations
### Know how to work with cookies
### Know cookie types and security policy

## Modules

### CommonJS
### Know JavaScript modules concept
### Know CommonJS module notation
### Understand difference between module notation and implementation
### Be able to use CommonJS modules in both browser and NodeJS
### AMD, UMD
### Know AMD notation
### Know difference between CommonJS/AMD/UMD module notations
### ES2015
### Know ES2015 module notation

## Nodes Modification

Node Properties
Node Attributes
Know how to modify DOM element properties and attributes
Understand DOM element properties / attributes connection
Data Attributes
CSS Scripting
Be able to add/toggle/remove CSS classes for DOM element
Be able to modify inline styles for DOM element
Be able to explain inline styles performance issues

## Timers

[setTimeout]
[setInterval]
[clearTimeout]
[requestAnimationFrame]
Understand [requestAnimationFrame] concept
Be able to explain difference between [setTimeout] and [requestAnimationFrame]

## Web Storage

LocalStorage
SessionStorage
Know web storages limitations and security policy
IndexedDB

## optional

## Cross-Origin Requests

Know AJAX security policy
Understand cross domain request prerequisites
Be able to handle AJAX security issues
IFrame

## Events Advanced

Mobile Events
Custom Events

## Modules Advanced

RequireJS
Know how to define AMD module
Know how to define AMD module dependencies
Know how to wrap CommonJS module for AMD
Be able to configure RequireJS
Be able to use RequireJS plugins
SystemJS
Know how to define SystemJS module
Know how to define SystemJS module dependencies
Know how to wrap CommonJS/AMD modules for SystemJS
Be able to configure SystemJS
Be able to use SystemJS plugins

## Page Lifecycle

Parsing
Reflow
Repaint
Optimizations

## Web Security

CSRF
Know CSRF attack vector
Know protection methods against CSRF attack
XSS
Know XSS attack vector
Know protection methods against XSS attack
Be able to compare CSRF and XSS attacks

## WebSockets

WebSocket concept
WenSocket interface