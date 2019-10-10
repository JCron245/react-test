# BlndSpt Test

## React - [reactjs.org](http://reactjs.org)

A JavaScript library for building user interfaces. It is maintained by Facebook and a community of individual developers and companies.

### Virtual DOM

Virtual Document Object Model, or virtual DOM. React creates an in-memory data-structure cache, computes the resulting differences, and then updates the browser's displayed DOM efficiently. This allows the programmer to write code as if the entire page is rendered on each change, while the React libraries only render subcomponents that actually change.

### JSX

JSX, or JavaScript XML , is an extension to the JavaScript language syntax. Similar in appearance to HTML, JSX provides a way to structure component rendering using syntax familiar to many developers. React components are typically written using JSX, although they do not have to be.

An example of JSX code:

```js
class App extends Component {
  render() {
    const msg = 'hello world';
    return (
      <div>
        <p>{ msg }</p>
      </div>
    );
  }
}
```

### React Hooks

## React with both Class Components and Function Components with Hooks

### Class Components

Class components can be created using ES6 classes or using React.createClass. Facebook has suggested that in the future they would be removing React.createClass [[link](https://reactjs.org/blog/2015/03/10/react-v0.13.html)].

#### ES6 Class Component Declaration

javascript
```js
import React from 'react';

class MyComponent extends React.Component {
    constructor(props) {
        super(props);
        this.state = {

        };
    }

    render() {
        return <p>I am a component!</p>;
    }
}


MyComponent.propTypes = {

};

MyComponent.defaultProps = {

};

export default MyComponent;
```
typescript
```js
import React, { ReactElement, Component} from 'react';

interface MyComponentProps {

}

interface MyComponentState {
    msg: string;
}


export class MyComponent extends Component<MyComponentProps, MyComponentState> {
	constructor(props: MyComponentProps) {
		super(props);
        this.state = {
            msg = 'Hello world';
        }
    }
    
    render = (): ReactElement => {
        return (
            <p>{this.state.msg}, I am a component!</p>
        );
    }
}
```

#### Create Class Component Declaration
```js
import React from 'react';

const ImAMixin = {
    doThing()  {
        // does thing
    }
};

const MyComponent = React.createClass({   
    mixins: [ImAMixin], 
    getInitialState () {
        return {
            
        };
    },

    propTypes: {

    },

    getDefaultProps() {
        return {

        };
    },

    doSomethingWithAMixin() {
        this.doThing(); // mixin is used
    }

    render() {
        return <p>I am a component!</p>;
    }
});

export default MyComponent;
```

### Function Components With Hooks

## Create React App

- [github](https://github.com/facebook/create-react-app)
- [npm](https://www.npmjs.com/package/create-react-app)
- [docs](https://create-react-app.dev/docs/getting-started)

## React Scripts with SASS and other compilation tools

## React Native

## React Router – _and some proficiency with an animation library like react-router-transition_

## Redux and react-redux

### Redux

### react-redux

## Deep understanding of react-thunk and react-saga

### react-thunk

### react-saga

## Proficiency with Axios and Fetch

### fetch

### axios

## React performance best practices

## Very deep understanding of all things ES2019 – ask yourself if you know what a Generator is

### new in ES2019

### What's a generator?

## Intimate knowledge of Bootstrap and react-bootstrap even if there are parts of it we hate

### bootstrap

### react-bootstrap

## Working knowledge of JEST and how to use it real world scenarios

## Deep understanding of Webpack, NPM and Yarn and how to create development and production environments

### webpack

### npm

### yarn

## A solid understanding of Docker and how to deploy your app to a Docker Registry and maintain a deployment script

## CSS

### How do I create a CSS variable and then reference it in other parts of a stylesheet?

### What is the single core difference between Flexbox and CSS Grids?