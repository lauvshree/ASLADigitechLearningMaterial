
We have so far been creating an HTML and using normal Java script which imports the React scripts to render the React UI. But we have a handy `create-react-app` from Facebook which builds everything you require to build a complete React app.

To create a react app named calculator, run the following code in your terminal. It will install all the packages you need for the app to run.

`npx create-react-app calculator`

You will notice that in the directory you ran the code from, a new directory name *calculator* would have been created, along with all the files required. 
Navigate to that directory and run `npm start`.

This will automatically start the server on localhost at port number 3000 (Or 300X if the port 3000 is in use) and also open the default browser with the default app. What you see here on the browser is *index.html*. We shall now develop our calculator with React. Open the directory *Calculator* in VSCode work space. Under the calculator directory, navigate to *public/index.html*

The index.html has many lines of unncessary content which we can get rid of for now. Replace the contents with the following lines.

```
<html>
  <head>
    <title>My Calculator</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

All we have in the above html is, title and a body with a div tag with id *root* where we will render our React component. Now under *src* go to App.js. This is where the main component that is rendered on index page is created. We will replace it with the following code. 

```
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
          We will include our calculator component here.
      </header>
    </div>
  );
}

export default App;

```

App.css has some basic styling we need for the React components. We will remove all the styling and we will add new ones later on.

Our calculator is a rectanglular box, with 6 rows, the top and the bottom row spanning 4 columns. 

=> insert image of finished calculator here

To start with, let's add a button component which is display the value that is being passed. Under src, create a folder named *components* and add Button.js and Button.css. Button.js will have the button component and the Button.css will have th styling for the same.

```
import React from 'react';
import './Button.css';

function Button(props) {
    return(<div className='calc_button'>{props.value}</div>)
}
export default Button;
```

As you can see, the button has a style class *calc_button*. Let's define the style for our calculator buttons in Button.css

```
.calc_button {
    display:flex;
    height:4em;
    justify-content: center;
    flex: 1;
    align-items: center;
    font-weight: lighter;
    font-size: 1.4em;
    background-color: #e0e1e6;
    color: black;
    outline: 1px solid #888;
}
```

Now let's include the button in our App.js. Replace the `function App()` in the App.js with the following code. 
```
function App() {
  return (
    <div className="App">
        <div className="calc_box">
          <div className="button_rows">
            <Button value='7'></Button>
            <Button  value='8'></Button>
            <Button  value='9'></Button>
            <Button  value='/'></Button>
          </div>
          <div className="button_rows">
          <Button value='4'></Button>
            <Button  value='5'></Button>
            <Button  value='6'></Button>
            <Button  value='*'></Button>
          </div>
          <div className="button_rows">
          <Button value='1'></Button>
            <Button  value='2'></Button>
            <Button  value='3'></Button>
            <Button  value='+'></Button>
          </div>
          <div className="button_rows">
          <Button value='.'></Button>
            <Button  value='0'></Button>
            <Button  value='='></Button>
            <Button  value='-'></Button>
          </div>
        </div>
    </div>
  );
}
```

In our App, we have a calc_box, which has 4 button_rows each with 4 buttons. With these changes, you should be able to see your react page updated with the buttons. Let's also add some style to our App and see how the page changes. Include the following code in App.css.

```
.App {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width:100%;  
}

.calc_box {
  width: 400px;
  height:600px;
}

.button_rows {
  display:flex;
  width:100%;
}
```
We want our calculator with width 400 px X 600 px to be aligned in the center of the page.

You will see how all the buttons, have the same background color. We want the operators to have an orange background and the rest of it to be grey. We will make changes in the *Button.js* to have different styling when the buttons are operators. Let's include an additional style for the opertor buttons. 

```
.calc_operator {
    display:flex;
    height:4em;
    justify-content: center;
    flex: 1;
    align-items: center;
    font-weight: lighter;
    font-size: 1.4em;
    background-color: orange;
    color: black;
    outline: 1px solid #888;
}
```

We then have to ensure that the buttons take the appropriate style. 

```
import React from 'react';
import './Button.css';

const operandslist = ['+','-','*','/'];

function isOperator(value) {
    if (operandslist.includes(value)) {
        return "calc_operator";
    }
    return "calc_button";
}

function Button(props) {
    return(<div className={isOperator(props.value)}>{props.value}</div>)
}

export default Button;
```

So now the style is set depending on value property to either *calc_operator* or to *calc_button*.

The constructor is a method that’s automatically called during the creation of an object from a class. It can handle your initial setup stuff like defaulting some properties of the object, or sanity checking the arguments that were passed in. Simply put, the constructor aids in constructing things.
 we take a props value from the constructor() and pass it to the super()
 When you call the super() method, it calls the constructor of the parent class which in the case of a React component is React.Component.



=> Create and Add the button component in components folder with ability to display value property
=> Add Button.css to the component folder
=> Add styling to App.css
