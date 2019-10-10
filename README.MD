# BlndSpt Test

## **Table Of Contents:**
- [React](#REACT)
    - [Virtual Dom](#virtual-dom)
    - [JSX](jsx)
    - [React Hooks](#react-hooks)
        - [State Hook](#state-hook)
        - [Effect Hook](#effect-hook)
        - [Custom Hooks](#custom-hooks)
        - [React Portal](#react-portal)
        - [Code Splitting / Lazy Loading](#code-splitting-/-lazy-loading)
- [React w/ both Class Components and Function Components with Hooks](#React-with-both-Class-Components-and-Function-Components-with-Hooks)
    - [Class Components](#class-components)
        - [ES6 Class Component](#ES6-Class-Component-Declaration)
        - [Create Class Component](#Create-Class-Component-Declaration)
    - [Function Components w/ Hooks](#)
- [Create React App](#)
- [React Scripts w/ SASS and other compilation tools](#)
- [React Native](#)
- [React Router](#)
- [Redux and React-Redux](#)
    - [Redux](#)
    - [React-Redux](#)
- [React-Thunk and React-Saga](#)
    - [React-Thunk](#)
    - [React-Saga](#)
- [Fetch and Axios](#)
    - [Fetch](#)
    - [Axios](#)
- [React Performance Best Practices](#)
- [ES2019](#ES2019)
    - [Whats New](#)
    - [Generators](#)
- [Bootstrap and React-Boostrap](#)
    - [Bootstrap](#)
    - [React-Bootstrap](#)
- [JEST](#)
- [Webpack, NPM, and Yarn](#)
    - [Webpack](#webpack)
    - [NPM](#npm)
    - [Yarn](#yarn)
- [Docker](#A-solid-understanding-of-Docker-and-how-to-deploy-your-app-to-a-Docker-Registry-and-maintain-a-deployment-script)
- [CSS](#css)
    - [How do I create a CSS variable and then reference it in other parts of a stylesheet?](#How-do-I-create-a-CSS-variable-and-then-reference-it-in-other-parts-of-a-stylesheet?)
    - [What is the single core difference between Flexbox and CSS Grids?](#What-is-the-single-core-difference-between-Flexbox-and-CSS-Grids?)

# **React**
[reactjs.org](http://reactjs.org)

A JavaScript library for building user interfaces. It is maintained by Facebook and a community of individual developers and companies.

## **Virtual DOM**

Virtual Document Object Model, or virtual DOM. React creates an in-memory data-structure cache, computes the resulting differences, and then updates the browser's displayed DOM efficiently. This allows the programmer to write code as if the entire page is rendered on each change, while the React libraries only render subcomponents that actually change.

## **JSX**

JSX, or JavaScript XML , is an extension to the JavaScript language syntax. Similar in appearance to HTML, JSX provides a way to structure component rendering using syntax familiar to many developers. React components are typically written using JSX, although they do not have to be.

An example of JSX code:

```javascript
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

## **React Hooks**

They let you use state and other React features without writing a class.

### **State Hook**

Here, useState is a Hook. We call it inside a function component to add some local state to it. React will preserve this state between re-renders. 

`useState` returns a pair: the current state value and a function that lets you update it. You can call this function from an event handler or somewhere else. It’s similar to this.setState in a class, except it doesn’t merge the old and new state together. 

```javascript
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call 'count' and initialize it to 0
  const [count, setCount] = useState(0); // useState is our 'Hook'

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### **Effect Hook**

The Effect Hook, useEffect, adds the ability to perform side effects from a function component. It serves the same purpose as componentDidMount, componentDidUpdate, and componentWillUnmount in React classes, but unified into a single API.

For example, this component sets the document title after React updates the DOM:

```javascript
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

You can also use a return statement within useEffect to have functionality fire off on unmount.

### **Custom Hooks**

You can write custom hooks to share stateful logic between components.
This is custom logic to tell whether a friend is online or offline. The custom hook is using both useState and useEffect and takes a friendID to tell whether 
they are online or not. 

```javascript 
import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

now we can use the custom hook in different components.

```javascript
 function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}

function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```

*Custom hooks are more of a convention than feature. If a functions name starts with "use" and it calls other hooks React determines this is a custom hook.
(useFriendStatus is calling useState and useEffects)
The "useSomething" naming convention is how the hook linter plugin catchs bugs in the code using hooks. 

### **React Portal**

### **Code Splitting / Lazy Loading**

# **React with both Class Components and Function Components with Hooks**

## **Class Components**

Class components can be created using ES6 classes or using React.createClass. Facebook has suggested that in the future they would be removing React.createClass [[link](https://reactjs.org/blog/2015/03/10/react-v0.13.html)].

### **ES6 Class Component Declaration**

javascript
```javascript
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
```javascript
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

### Create Class Component Declaration
```javascript
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

## Function Components With Hooks

# Create React App

- [github](https://github.com/facebook/create-react-app)
- [npm](https://www.npmjs.com/package/create-react-app)
- [docs](https://create-react-app.dev/docs/getting-started)

# React Scripts with SASS and other compilation tools

# React Native

# React Router – _and some proficiency with an animation library like react-router-transition_

Standard routing library for React.
  - Supports both web and React Navitve
    - react-router-dom
    - react-router-native

Basic Routing example 

```javascript
  import React from "react";
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link
} from "react-router-dom";

export default function App() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
            <li>
              <Link to="/users">Users</Link>
            </li>
          </ul>
        </nav>

        {/* A <Switch> looks through its children <Route>s and
            renders the first one that matches the current URL. */}
        <Switch>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/users">
            <Users />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}

function Home() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function Users() {
  return <h2>Users</h2>;
}
```
- Route element
  - Routes have 3 props that can be used to define what should be rendered when a route's path matches. Only one should be proveded to the element.
    - component - a React component
    ```javascript
        <Route path='page' component={page} />
    ```
    - render - a function that returns a React element, useful fo inline rendering and passing extra props.
    ```javascript
        <Route path='/page' render={(props) => (
          <Page {...props} data={extraProps}/>
        )}/>
    ```
    - children - a function that returns a React like element. unlike the first 2 props this will always be rendered, whether or not the route's path matches.
    ```javascript
        <Route path='/page' children={(props) => (
        props.match
          ? <Page {...props}/>
          : <EmptyPage {...props}/>
        )}/>
    ```
    - Switch element
      - looks through all of the child routes and renders the first one that matches the current url
      ```javascript
      function Main() {
        return (
          <main>
            <Switch>
              <Route exact path='/' component={Home}/>
              <Route path='/roster' component={Roster}/>
              <Route path='/schedule' component={Schedule}/>
            </Switch>
          </main>
        );
      }
   ```
  - Link element
    - element changes the url and renders the correct component without re-loading the page. think routerLink :)
    ```javascript
      function Header() {
        return (
          <header>
            <nav>
              <ul>
                <li><Link to='/'>Home</Link></li>
                <li><Link to='/roster'>Roster</Link></li>
                <li><Link to='/schedule'>Schedule</Link></li>
              </ul>
            </nav>
          </header>
        );
      }
    ```


# Redux and react-redux

## **Redux** - [Redux Docs/API](https://redux.js.org/api/api-reference)

Redux is a predictable state container for JavaScript apps. Written by _Dan Abramov_ who also created `create-react-app`, `react-hot-loader`, and `react-dnd`.


Redux was inspired by Flux and Elm.

Facebook was facing problems with the MVC structure. The Model and View relationships can get tricky. This is especially true as your application starts to scale. You could be dealing with problems such as infinite loops.

That’s when Facebook introduced Flux. A uni-directional way of updating Views and handling user actions.
You can learn more about Flux and some of the challenges Facebook faced in this video.

Redux uses this concept of uni-directional data flow. (Redux is a modified implementation of the Flux architecture)

- The application has a central / root state.
- A state change triggers View updates.
- Only special functions can change the state.
- A user interaction triggers these special, state changing functions.
- Only one change takes place at a time.

This means that the central state cannot trigger any further actions. Only a user input can trigger another action. This makes state much more manageable. It also makes it difficult to introduce infinite loops.

## **react-redux** - [React-Redux Docs](https://react-redux.js.org/)

While Redux is framework agnostic. React-Redux are the official React bindings for Redux. It also works with React-Native `0.18+` if using React-Redux `5.x+`



# Deep understanding of react-thunk and react-saga

## react-thunk

## react-saga

# Proficiency with Axios and Fetch

## fetch
The fetch API is a JavaScript interface for accessing and manipulating parts of the HTTP pipline such as requests and responses.

  - fetch interfaces
    - Global fetch() 
      - method to gather resources async across the network.
      - returns a promise that resolves to response of the request (successful or not)
    - Headers
      - response/request headers
    - Request
      - resource request
    - Resopnse 
      - response to a request
  - fetch mixins
    - Body
      - represents the body of the request/response 
      - provides methods to decleare which content type and how to handle req/res
        - ex. res.json()

Basic fetch example
```javascript
  const response = await fetch('http://example.com/movies.json');
  const myJson = await response.json();
  console.log(JSON.stringify(myJson));
```

Example POST method
```javascript
  try {
  const data = await postData('http://example.com/answer', { answer: 42 });
  console.log(JSON.stringify(data)); // JSON-string from `response.json()` call
} catch (error) {
  console.error(error);
}

async function postData(url = '', data = {}) {
  // Default options are marked with *
  const response = await fetch(url, {
    method: 'POST', // *GET, POST, PUT, DELETE, etc.
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'same-origin', // include, *same-origin, omit
    headers: {
      'Content-Type': 'application/json'
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    redirect: 'follow', // manual, *follow, error
    referrer: 'no-referrer', // no-referrer, *client
    body: JSON.stringify(data) // body data type must match "Content-Type" header
  });
  return await response.json(); // parses JSON response into native JavaScript objects
}
```
## axios
Promise based HTTP client for the browser and node.js
  - axios is heavily inspired by the $http service provided in AngularJS.

GET request example
```javascript
  const axios = require('axios');

// Make a request for a user with a given ID
axios.get('/user?ID=12345')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .finally(function () {
    // always executed
  });

// Optionally the request above could also be done as
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
  .finally(function () {
    // always executed
  });  

// Want to use async/await? Add the `async` keyword to your outer function/method.
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```
POST reqeust example

```javascript
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

- [github](https://github.com/axios/axios)
# React performance best practices

# ES2019

## What's new in ES2019

## What's a generator?

# Intimate knowledge of Bootstrap and react-bootstrap even if there are parts of it we hate

## bootstrap

## react-bootstrap

# Working knowledge of JEST and how to use it real world scenarios

# Deep understanding of Webpack, NPM and Yarn and how to create development and production environments

## webpack

## npm

## yarn

# A solid understanding of Docker and how to deploy your app to a Docker Registry and maintain a deployment script

Docker uses containerization which is similar to virtualization (like a vm). The difference is you do not need to complete environment to run like the OS.  
Containers include the application and all of its dependencies --but share the kernel with other containers, running as isolated processes in user space on 
the host operating system. Docker containers are not tied to any specific infrastructure: they run on any computer, on any infrastructure, and in any cloud.

## deploy your app to a Docker Registry
  * Before you can deploy a registry, you need to install Docker on the host. A registry is an instance of the registry image, and runs within Docker.
  * Use a command like `docker run -d -p 5000` to start the registry container
  * Copy an image from Docker Hub to your registry
  * `docker pull ubuntu`
  * `docker tag ubuntu`
  * `docker push localhost:5000/my-ubuntu`

You can also deploy to Kubernetes

# CSS

## How do I create a CSS variable and then reference it in other parts of a stylesheet?

Setting a CSS variable

```css
element {
  --main-bg-color: brown;
}
```

Using a CSS variable
```css
element {
  background-color: var(--main-bg-color);
}
```

## What is the single core difference between Flexbox and CSS Grids?

CSS Grid is a `layout-first` approach while Flexbox is a `content-first` approach.