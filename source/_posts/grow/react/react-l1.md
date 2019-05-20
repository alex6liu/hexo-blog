---
title: react l1
date: 2019-05-14 09:49:30
tags: [react, l1]
---

## Create basic components

### Using JSX

`const element = <h1>Hello, {name}!</h1>;` It is called JSX, and it is a syntax extension to JavaScript.

### Understanding component specs

#### Function Components

The simplest way to define a component is to write a JavaScript function:

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

#### Class Components

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### Understanding basic lifecycle events

image from `http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/`

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/react/react-lifecycle.png)

Another image:

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/react/react-lifecycle-1.png)

### Using state and props

```js
constructor(props) {
  super(props);
  this.state = {date: new Date()};
}
```

### Understanding react event system

- React events are named using camelCase, rather than lowercase.
- With JSX you pass a function as the event handler, rather than a string.

## Create reusable components

### Validating props

```js
/**
 * FUNCTIONAL COMPONENTS
 */
function ReactComponent(props) {
  // ...implement render logic here
}

ReactComponent.propTypes = {
  // ...prop type definitions here
}


/**
 * CLASS COMPONENTS: METHOD 1
 */
class ReactComponent extends React.Component {
  // ...component class body here
}

ReactComponent.propTypes = {
  // ...prop type definitions here
}


/**
 * CLASS COMPONENTS: METHOD 2
 * Using the `static` class properties syntax
 */
class ReactComponent extends React.Component {
  // ...component class body here
  
  static propTypes = {
    // ...prop type definitions here
  }
}
```

### Transferring props between components

`<Component {...this.props} more="values" />`

Example:

```js
function FancyCheckbox(props) {
  var fancyClass = props.checked ? 'FancyChecked' : 'FancyUnchecked';
  return (
    <div className={fancyClass} onClick={props.onClick}>
      {props.children}
    </div>
  );
}
ReactDOM.render(
  <FancyCheckbox checked={true} onClick={console.log.bind(console)}>
    Hello world!
  </FancyCheckbox>,
  document.getElementById('example')
);
```

### Creating mixins

[React Mixins入门指南](https://github.com/MrErHu/blog/issues/5)

### Using refs

[Refs and the DOM](https://reactjs.org/docs/refs-and-the-dom.html)

There are a few good use cases for refs:

- Managing focus, text selection, or media playback.
- Triggering imperative animations.
- Integrating with third-party DOM libraries.

Avoid using refs for anything that can be done declaratively.

For example, instead of exposing `open()` and `close()` methods on a `Dialog` component, pass an `isOpen` prop to it.

```js
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    // create a ref to store the textInput DOM element
    this.textInput = React.createRef();
    this.focusTextInput = this.focusTextInput.bind(this);
  }

  focusTextInput() {
    // Explicitly focus the text input using the raw DOM API
    // Note: we're accessing "current" to get the DOM node
    this.textInput.current.focus();
  }

  render() {
    // tell React that we want to associate the <input> ref
    // with the `textInput` that we created in the constructor
    return (
      <div>
        <input
          type="text"
          ref={this.textInput} />

        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}
```

## Create complex components

### Understanding full component lifecycle
### Understanding React top-level API

[React Top-Level API](https://reactjs.org/docs/react-api.html)

### Using raw HTML in React components

```jsx
<div dangerouslySetInnerHTML={{__html: this.props.html}} />
```

### Adding animation

[Animation Add-Ons](https://reactjs.org/docs/animation.html)

High-level API: ReactCSSTransitionGroup

### Using ES2015

## Performance

### Understanding components rendering system
### Using PureRenderMixin
### Using immutable data structures (ImmutableJS)

## SPA

### Creating SPA using React Router

## Testing

### Unit testing using Jest and/or other testing frameworks
### Using React testing utilities
### Using JSDom for testing

## Tools

### Using React Devtools
### Building and deploying React apps
### Using React Hot Loader

## Understand Flux

### Understanding unidirectional data flow
### Using dispatcher
### Creating stores
### Creating actions
### Experience with any library (Redux, Mobx, Reflux, Alt, etc.)

## Advanced React usage

### Designing app architecture using React
### Profiling and optimizing react components
### Understanding virtual DOM
### Using server side rendering
### Integrating React into other frameworks (e.g. Backbone)
### Two-way binding
### Creating E2E tests