---
tags:
  - reactjs
  - frontend
  - interview
---
# React life cycle methods

React component lifecycle methods are hooks that allow you to run code at particular times in the process of a component’s creation, update, and destruction. These methods are divided into three main phases: Mounting, Updating, and Unmounting. Here's an overview of the lifecycle methods and the order in which they are called:

### Mounting Phase

These methods are called when an instance of a component is being created and inserted into the DOM:

1. **`constructor(props)`**: The constructor for a React component. Called before the component is mounted.
2. **`static getDerivedStateFromProps(props, state)`**: Invoked right before calling the render method, both on the initial mount and on subsequent updates. It should return an object to update the state, or `null` to update nothing.
3. **`render()`**: Required method in a class component that returns the JSX for the component.
4. **`componentDidMount()`**: Invoked immediately after a component is mounted. This is a good place to initiate network requests, set up subscriptions, or perform any other initialization.

### Updating Phase

These methods are called when a component is being re-rendered due to changes in props or state:

1. **`static getDerivedStateFromProps(props, state)`**: Called before every render. Can be used to update the state based on props.
2. **`shouldComponentUpdate(nextProps, nextState)`**: Invoked before rendering when new props or state are received. Return `true` to re-render, or `false` to skip updating.
3. **`render()`**: Called to re-render the component.
4. **`getSnapshotBeforeUpdate(prevProps, prevState)`**: Called right before the DOM is updated. The return value will be passed to `componentDidUpdate`.
5. **`componentDidUpdate(prevProps, prevState, snapshot)`**: Called immediately after updating. Good place to operate on the DOM when the component has been updated.

### Unmounting Phase

These methods are called when a component is being removed from the DOM:

1. **`componentWillUnmount()`**: Invoked immediately before a component is unmounted and destroyed. Use this method to clean up any subscriptions or timers.

### Error Handling

These methods are called when there is an error during rendering, in a lifecycle method, or in the constructor of any child component:

1. **`static getDerivedStateFromError(error)`**: Called when there is an error during rendering in a lifecycle method or constructor. Use this method to update the state so the next render will show an error boundary.
2. **`componentDidCatch(error, info)`**: Called when there is an error during rendering in a lifecycle method or constructor. Use this method to log error information.

### Order of Lifecycle Methods

1. **Mounting Phase**:
    
    - `constructor(props)`
    - `static getDerivedStateFromProps(props, state)`
    - `render()`
    - `componentDidMount()`
2. **Updating Phase** (when props or state change):
    
    - `static getDerivedStateFromProps(props, state)`
    - `shouldComponentUpdate(nextProps, nextState)`
    - `render()`
    - `getSnapshotBeforeUpdate(prevProps, prevState)`
    - `componentDidUpdate(prevProps, prevState, snapshot)`
3. **Unmounting Phase**:
    
    - `componentWillUnmount()`
4. **Error Handling**:
    
    - `static getDerivedStateFromError(error)`
    - `componentDidCatch(error, info)`