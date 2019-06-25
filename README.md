# Simple React random number generator using react redux.

1. Create react boiler template using `create-react-app` 
```
sudo npx create-react-app redux-demo
```

2. Install `redux` and `react-redux` dependencies
```
sudo npm i --save redux react-redux
```

3. Start react app
```
sudo npm start
```

4. Inside **redux-demo/src** create `Random.js` component with these values
```
//redux-demo/src/Random.js

//Import react and react-redux
import React from "react";
import {connect} from "react-redux";

class Random extends React.Component{

    //dispatch actions so that it will received by `reducer` 
    start = () => {
        this.props.dispatch({ type: "start" });
    };
    
    reset = () => {
        this.props.dispatch({ type: "reset"});
    };

    render() {
        return (
          <div>
            <span>{this.props.statusText}</span><br />
            <button onClick={this.start}>Start</button>
            <span>{this.props.randomNumber}</span>
            <button onClick={this.reset}>Reset</button>
          </div>
        );
      }
}

//Map all state(s) to properties in App.js
const mapStateToProps = state => ({
    randomNumber: state.myCounter,
    statusText: state.myStatus
});

//Wrap component and connect to redux-redux
export default connect(mapStateToProps)(Random);
```

5. Inside **redux-demo/src/App.js** replace with the ff:
```
//redux-demo/src/App.js

//import react
import React from 'react';

//import random 
import Counter from "./Random";

//import redux 
import {createStore} from "redux";
import {Provider} from "react-redux";

//Create intial state that will display on frontend
const MyIntitialState = {
  myStatus: 'Please click start to generate random numbers',
  myCounter : 0
};

//Reducers =  it will read all dispatch actions (start and end) under `App.js`
function reducer(state = MyIntitialState,action){
  switch(action.type){
      case "start":
      return{
          myCounter: Math.random(),
          myStatus: 'Generated random numbers are '
      }
      case "reset":
      return{
          myCounter: 0,
          myStatus: MyIntitialState.myStatus
      }

      //Return default states = MyIntitialState
      default: return state;
  }
}

//Create store for `Counter`
const MyStore = createStore(reducer);

function App() {
  return (
    <div className="App">
       <Provider store={MyStore}>
          <Counter />
      </Provider>
    </div>
  );
}

export default App;
```

### Resources 

[Usefull redux Form](https://davidkpiano.github.io/react-redux-form/)

[Redux basic workflow](https://hackernoon.com/https-medium-com-heypb-react-redux-workflow-in-4-steps-beginner-friendly-guide-4aea9d56f5bd)


