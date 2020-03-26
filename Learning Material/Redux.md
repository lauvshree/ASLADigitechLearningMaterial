###Prerequisite
React, Java script, Node JS

We are familiar with the advantages and disadvantages of smart(class component) and dumb(function) components in React. Smart components are react Class components, which have both properties and states. Dumb components are function components which have only properties but no state. 

Having the state within the class component might make it smart. But when the state needs to be accessed outside of the component, it becomes impossible. There are many occasions when it is imperative to pass the state from one component to the other irrespective of their nesting. It is for this purpose that, state management was separated from the components. In React we achieve this state management with Redux.

`Redux` library has all that it requires for store management and `react-redux` binds react and redux libraries together. 

The store management with redux has 3 main components:
### Actions - 
**Actions represents what happens**
 are block of information that send data from your application to your store. They are plain JavaScript objects. Actions must have a `type` property that indicates the type of action being performed. Types should typically be defined as `string` constants. They are the only source of information for the store. You send them to the store using `store.dispatch()`.  We will see how we use the `action` as we work out our example.

### Reducers - 
**Reducers represents how it happens**
Reducers specify how the application's state changes in response to actions sent to the store. Remember that actions only describe what happened, but don't describe how the application's state changes. For example, if we have a `counter` in the store the `action` would would describe that we will `increase` the counter. But the `reducer` will specify it will increase by 1. We will create the reducer in such a way that if there is no state set, the default state is returned. That is if there is no action performed on the value we are storing, it will return it's current value. 

### Store - 
The Store is the object that brings the `action` and `reducer` together. The store has the following responsibilities:

Holds application state;
Allows access to state;
Allows state to be updated via dispatch(action);

### Creating an application with React redux
1. `npx create-react-app redux_ex1` - This will create a react appliction name redux_ex1 in the directory called redux_ex1 under the current directory from where the command is run
2. `cd redux_ex1` - Change to your application directory
3. `npm install redux react-redux` - Install the redux and react-redux libraries for your application. Open package.json and verify if it has installed properly.

In this application that we are building to learn the use of redux with react, we will have one `MainPanel` component which contain two internal Components, `MyButton` and `DivPanel`. `MyButton` is a button component which maintains a counter `onClick`. The value of this counter will be displayed in `DivPanel`. The content of `DivPanel` will be automatically refreshed everytime the counter value changes. Remember we will be using only dumb components as we are separating out state management. 

Under `src`, create a folder name `action` to define the actions for our application. The only action we are going to perform is incrementing the counter. In the action folder, create `index.js` with the following content.

```
const increment = (val) => {
    return {
        type : 'INCREMENT',
        inc : val
    }
}

export default increment;
```

`val` is the value we want to increase the counter by everytime the button is clicked. 

Now that we have our `action` which defines *what is to be done*, let's create the reducers which will define *how it is done*.

Under `src`, create a folder named `reducers`. In the reducers folder create `index.js` with the following content. 

```
import {combineReducers} from 'redux'

const counter = (state=0,action)=>{
    if(action.type === 'INCREMENT') {
        //This will increase the value of counter by the value passed to the increment method
        return state+action.inc;
    }
    //Returns the current value of the counter
    return state;
}

const myReducers = combineReducers({counter});

export default myReducers;
```

Now we have our action and reducers. What is left to be created is the store. Before we create the store we will create the components. Create a folder for the components named `components`. Create `MyButton.js` with the following content.

```
import React from 'react'
import { useDispatch} from 'react-redux';
import increment from '../action'

const MyButton = ()=>{
    let dispatch = useDispatch();
    return (
        <button onClick={()=>dispatch(increment(1))}>Increase counter</button>
    );
}

export default MyButton;
```
`useDispatch` dispatches the event to the store and finds out what action is to be taken and uses the appropriate reducer to do the same.

Let's now create DivPanel.js which will contain `DivPanel` where we will display the counter value. 
```
import React from 'react'
import { useSelector } from 'react-redux';

const DivPanel = () =>{
    let counterVal = useSelector(state => state.counter)
    return (
        <div>
            The present value of counter is 
            {counterVal}
        </div>
    );
}

export default DivPanel;
```
`useSelector` is used to select the state from the store whose value we want to access. 

Now let's create the MainPanel with the two components in the file `MainPanel.js`.

```
import React from 'react'
import MyButton from './MyButton'
import DivPanel from './DivPanel';

const MainPanel = ()=>{
    return (
        <div>
            This is main panel
            <MyButton></MyButton>
            <DivPanel></DivPanel>
        </div>
    );
}
export default MainPanel;
```

We have all the panels created. Now let's render the MainPanel through `App.js`. 

```
import React from 'react';
import MainPanel from './components/MainPanel';

function App() {
  return (
      <div>
        <MainPanel/>
      </div>
    );
}

export default App;

```

Now for the final set up of react application, we need to create and set up the store, where we can manage all the states (in this application, the `counter`) we want. This is done in `index.js`

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import * as serviceWorker from './serviceWorker';

import {createStore} from 'redux';
import {Provider} from 'react-redux'
import myReducers from './reducers'


//Create the store
const myStore = createStore(myReducers);

//This will console log the current state everytime the state changes
myStore.subscribe(()=>console.log(myStore.getState()));

//Enveloping the App inside the Provider, ensures that the states in the store are available
//throughout the application
ReactDOM.render(<Provider store={myStore}><App/></Provider>, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();

```

That is it! Our redux configuration is all done and we are ready to run the application. 
From the terminal run `npm start`. 


