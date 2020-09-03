## What is React 
React is Java script UI library created and maintained as an open source by Facebook and a community of developers. It is a tool used for building UI components. 

### Prerequisites
You should be familiar with Javascript and HTML. You should be comfortable dealing with HTML as a DOM. 

### Objective
By the end of this learning, you will be able to develop a React UI with reusable components, rendering data and handling events. 

### Getting started
As mentioned at the outset, React is a Java script library. 

The most important part of React is *Component*. Component is piece of user interface. When we build a UI with React, we build many such components and bind them all together to render the complete UI. You can think of each component as a <div> container unit. But in the case of React all of the these will be within atleast one root component. This root component may have many children in a tree-like structure. But the root component represents the entire client application. To sum it up, a **React application is a tree of components.** 

 Think of Facebook app. We have the blue bar in the top, which has the home button, search bar, profile, notifications and help. And then we have the left panel which has many inner components the middle component which has all the post feeds and then the right which has the stories, birthday notifications, games etc., If you think of it, each of these are nested components inside the main application.

 React uses a special mark-up language called JSX (Javascript XML) which has an uncanny resemblance to HTML. 
 
 ```
 const element = <h1>Hello World!</h1>
 ```
 The above statement is a JSX. It is not a string literal. Note that there are no quotes. This mark-up language is embedded within our normal HTML pages. This can be compiled and interepreted as Java Script by Babble, a special in-memory tool. Babble understands and allows use of the ES6 compatible Javascript features. JSX are embedded inside special script tags where the type attribute specifies the content need to use babel. `script type="text/babel"`

### Our first React JS page

Let's build a very simple react page to start with. Since it uses external JS libraries these scripts need to be sourced inside our html. We will use 3 JS files to build our React application. 

* React - this package holds the react source for components, state, props and all the code that is react.
* ReactDOM - this is the glue between React and the DOM. 
* Babel - To compile and interpret the JSX

The reason React and ReactDOM were split into two libraries was due to the arrival of React Native, a react platform for mobile development. React-dom is used only in web apps. React library is common to both web and mobile applications.


```
<html>

<!-- Load React API -->
<script src= "https://unpkg.com/react@16/umd/react.production.min.js"></script>
<!-- Load React DOM-->
<script src= "https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>

<!-- Load Babel Compiler -->
<script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>

<body>

<!--
A container to display react DOM elements
-->
<div id="comp1">Hello World!</div>

<script type="text/babel">
    //JSX goes here
</script>

</body>
</html>

```

This is a normal HTML page. Now we will render a React Component on it. Insert the following lines of code in the above code. *ReactDOM.render* takes 2 parameters - what to render and where to render. *What to render* has to be a valid HTML component with an open and close tag. 

```
ReactDOM.render(<h1>Hello World!</h1>,document.getElementById('comp1'));

```

It might seem like we complicated an HTML to get just a <h1> displayed. This was just an easy example to get started. 

The JSX can also include expressions that need to be evaluated.

```
ReactDOM.render(<h1> 256 + 392 = {256+392} </h1>,document.getElementById('comp1'));

```



As mentioned, React component is a tree-like structure. So there can always be just one main component that is displayed. This component is immutable. You cannot change the value of the component. You can only re-render the component. For instance, if I want to display the current time, it is going to over and over re-render the component every time. 

Replace the JSX in the previous code with the following code.

```
const displayTime = () => {
    const currDate = new Date();
    ReactDOM.render(<p>{currDate.toString()}</p>, document.getElementById('comp1'));
}
setInterval(displayTime, 1000);
```

### Custom components

We know HTML has many components defined by default that we can use. But React also allows us to create custom components. 

Let's create a component named *Mycomp*

```
const Mycomp = () => {
    return <h1>This is my own component</h1>
}

ReactDOM.render(<Mycomp/>,document.getElementById('comp1'));

```

Here Mycomp is a *function* that we have defined which returns valid HTML element. 

React allows two types of components
1 Functional component
2 Class component. 

What we saw in the example above is a functional component. When the Babel encounters a tag name that is not a valid HTML tag, it recognises it to be a custom component and looks for a function or a class which is a subclass of Component, with the same name. If the same as above were to be defined as a Class component,it can be done in the following manner.

```
class Mycomp extends React.Component {
    //override the render method
    render() {
        return <h1>This is my own component</h1>;
    }
}
ReactDOM.render(<Mycomp/>,document.getElementById('comp1'));

```
Notice that the function and the class' render method both return an element. This has to be an element and can only be one element. The element can have as many children as possible.

The instances of these custom made React components can have properties and state. Properties are more like public attributes which can be set from outside. Whereas the state is more private to the component. Functional components have properties but they don't have state. We will look at this in detail with examples later. 

Let's define a property name and display the name property and the of the component in the render. 

```
class Mycomp extends React.Component {
    //override the render method
    render() {
        return <h1>This is my own component named 
                {this.props.name}
                </h1>;
    }
}

ReactDOM.render(<Mycomp name="myBrandNewComp"/>,document.getElementById('comp1'));

```

Let get into a little more detail. Let's create a page, where we will have a root or Main component inside which we will have a component named "ReactPanel" which will inturn have three button components. Each of the button will display whatever is set as their child element in the respective container. We will see how we can set the properties from the container components. 

```
<script type="text/babel">

class MyComp extends React.Component {    
    render() {
        return <div>
                    The react Panel is in here
                    <ReactPanel name="The First Panel"/>
                </div>
            }
}

class ReactPanel extends React.Component {
    render() {
        return  <div>    
                {this.props.name}
                <Button>1</Button>
                <Button>2</Button>
                <Button>3</Button>
                </div>
    }
}

class Button extends React.Component {
    render() {
        return  <div>{this.props.children}</div>
    }
}

ReactDOM.render(<MyComp/>,document.getElementById("root"));

</script>

```

Let's now define some styling for the buttons as without styling they are just plain texts. In production environment, we will define a style sheet and link it to this html. But for now, we will define the styles in the html document. 
```
<style>

.buttons {
    display:flex;
    height:1em;
    width: 1em;
    justify-content: center;
    flex: 1;
    align-items: center;
    font-weight: lighter;
    font-size: 1.4em;
    background-color: #e0e1e6;
    color: black;
    outline: 1px solid #888;
}
</style>

```

We will pass the styles from the container ReactPanel. Rewrite the Button and ReactPanel class with the following code.

```
class ReactPanel extends React.Component {
    render() {
        return  <div>    
                {this.props.name}
                <Button className="buttons">1</Button>
                <Button className="buttons">2</Button>
                <Button className="buttons">3</Button>
                </div>
    }
}

class Button extends React.Component {
    render() {
        return  <div className={this.props.className}>{this.props.children}</div>
    }
}
```

Reload your HTML to see if the changes are reflecting. 

We will now maintain a counter state in the React Panel which will increment every time a button is clicked. As mentioned earlier state can only be had for class components. To maintain *state* the componennt class needs a constructor. A constructor is a method that’s called by default during the creation of an object from a class. It handles the initial setup like defaulting some properties of the object. In simple words, the constructor aids in constructing things.

To contain and maintain the counter state in ReactPanel we need to have a constructor. 

We take a props value from the constructor() and pass it to the super(). super call has to be the first statement in the ReactComponent's constructor. When the super() method, it calls the constructor of the parent class. 


```
class ReactPanel extends React.Component {
    constructor(props) {
        super(props);
    }

    //Here we are defining the state we want to maintain. 
    state = {
        counter : "0"
    };

    //A function to increment the counter every time a button is clicked
    incrementCounter = () => {
        this.setState({counter:parseInt(this.state.counter)+1});
    }

    render() {
        return  <div>    
                {this.props.name}<br/>
                {this.state.counter}
                
                //onClick is a property of the Component super class. 

                <Button className="buttons" onClick={this.incrementCounter}>1</Button>
                <Button className="buttons" onClick={this.incrementCounter}>2</Button>
                <Button className="buttons" onClick={this.incrementCounter}>3</Button>
                
                </div>
    }
}

class Button extends React.Component {
    render() {
        return  <div className={this.props.className} onClick={this.props.onClick}>{this.props.children}</div>
    }
}
```

Since the counter is maintained as one of the states of the ReactPanel, the function increments the counter in ReactPanel every time the button is clicked. For the button to call this function, we need to pass this function as a value to the button's *onClick* property. 


We just created a functional React Page. Congratulations.
