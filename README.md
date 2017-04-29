# react-resize-aware

A simple React.js component you can use to make any piece of UI aware of its size.

Each time the component changes its size (it can be due to a window resize, a CSS change, a JS action, etc...)
a `resize` event will be fired on the component itself.

You can then listen to such event to perform any kind of operation.

This component doesn't rely on intervals, loops or any other weird stuff.  
It takes advantage of the `resize` event of the `<object>` HTML element.

It requires just React.js and ReactDOM.

Install it with:

```
npm install react-resize-aware --save
```

# Usage

> **note**: `ResizeAware` needs a position different from `initial` to work!  
> Make sure to set it to `relative`, `absolute` or `fixed` using its `style` property or with CSS

## Stateless approach

If your component is stateless or you prefer to follow a functional approach
you can use ResizeAware to wrap your existing component and it will take care
to provide two property (`height` and `width`) that will get updated every time
the component sizes change.

```jsx
import React from 'react';
import ResizeAware from 'react-resize-aware';

// This component will get re-rendered every time its width or height changes
function MyComponent({width, height}) {
  return <div>{width}x{height}</div>;
}

function App() {
  return (
    <ResizeAware style={{ position: 'relative' }}>
      <MyComponent />
    </ResizeAware>
  );
}
```

## Stateful approach

If your component is stateful or you need to use ResizeAware in the middle of one
of your components you can use the `onResize` property of the component to provide
a callback that will be called on each resize of the ResizeAware component and will
provide as first argument an object with `width` and `height` properties.

```jsx
import React, { Component } from 'react';
import ResizeAware from 'react-resize-aware';

function MyComponent({width, height}) {
  return <div>{width}x{height}</div>;
}

class MyComponent extend Component {
  handleResize = ({ width, height }) => console.log(width, height);
  
  render() {
    return (
      <div>
        My app renders...
        <ResizeAware
          style={{ position: 'relative' }}
          onlyEvent
          onResize={this.handleResize}
        >
          <MyComponent />
        </ResizeAware>
      </div>
    );
  }
}
```

## Properties

- The `onlyEvent` property will prevent ResizeAware from passing the `height` and `width`
properties to its child component, in case you don't want to rely on them.
- The `tag` property allows to define the HTML tag used by ResizeAware to render.
- The `onResize` property is an optional callback called on each resize with as first
  argument an object containing `height` and `width` properties.

<!-- ## Self containing

If you need to keep your DOM structure clean and you don't want the additional
`div` added by ResizeAware, you can use the component as base for your own one.

```jsx
import React from 'react';
import ResizeAware from 'react-resize-aware';

// This component will get re-rendered every time its width or height changes
function MyComponent({width, height}) {
  return <div style={{ position: 'relative' }}>{width}x{height}</div>;
}

function App() {
  return (
    <ResizeAware component={MyComponent} />
  );
}
``` -->

# License

MIT License
Copyright 2016+, Federico Zivolo
