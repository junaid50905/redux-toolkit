# redux-toolkit

<h2>What is state in React Js</h2>
The state is a built-in React object that is used to contain data or information about the component.

<h2>Why do we need redux ?</h2>
Redux allows you to manage your app’s state in a single place and keep changes in your app more predictable and traceable.

<h2></h2>
<h2>What Pain does redux solves</h2>
<ul>
  <li>Redux is a global state</li>
  <li>Redux is not necessary for every project.</li>
  <li>You may need Redux if you don’t want to do props drilling (passing props too deep).</li>
  <li>If you are still confused about Redux, just think about the React state. The only difference is you can access the state from anywhere.</li>
</ul>
<img src='https://whataboutcoding.com/wp-content/uploads/2022/12/REDUX-TOOLKIT-DIAGRAM-HIMANSHU-SHEKHAR-1024x641.png'/>


<h2>Let’s Build an Redux App</h2>
Well to make interesting , we will learn redux toolkit along with making a simple counter application.

Let’s start.

<h3>Step 1 – Install Redux and Redux Toolkit package in an react app</h3>
Thankgod✌️ we only need two packages now , so go ahead and install these two.
<pre>
npm install --save react-redux @reduxjs/toolkit
</pre>


<h3>Step 2 – Create a global store</h3>
<pre>
 Create src/app/store.js –

import { configureStore } from "@reduxjs/toolkit";

export const store = configureStore({
  reducer: {},
});

</pre>

configureStore accepts a single object rather that multiple function arguments. It’s because under the hood, the store has been configured to allow using the Redux DevTools Extension and has had some Redux middleware included by default.


<h3>Step 3 – Providing store to complete react app</h3>

This will provide store globally.

Go to src/index.js :

<pre>
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import { store } from "./app/store";
import { Provider } from "react-redux";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
</pre>
Provider wraps the App and the whole application has access to redux store.

Now check your redux dev tool


<h3>Step 4 – Now lets create a slice</h3>
A function that accepts an initial state, an object of reducer functions, and a “slice name”, and automatically generates action creators and action types that correspond to the reducers and state.

Internally, it uses createAction and createReducer, so you may also use Immer to write "mutating" immutable updates

Create a slice – src/features/counter/counterSlice.js

<pre>
import { createSlice } from "@reduxjs/toolkit";

const initialState = { value: 0 };

export const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers: {
    increment: (state) => {
      state.value = state.value + 1;
    },
    decrement: (state) => {
      state.value = state.value - 1;
    },
    incrementByValue: (state, action) => {
      state.value = state.value + action.payload;
    },
    incrementByTypedValue: (state, action) => {
      state.value = state.value + action.payload;
    },
  },
});

export const { increment, decrement } = counterSlice.actions;

export default counterSlice.reducer;

</pre>


<h3>Step 5 – Add Slice Reducers to the Store</h3>

<pre>
import { configureStore } from "@reduxjs/toolkit";
import counterRedcuer from "../features/counter/counterSlice";

export const store = configureStore({
  reducer: { counter: counterRedcuer },
});

</pre>

<h3>Step 6 – Implementing useSelector and useDispatch in React Components</h3>
Components/Counter.js

here, the counter of useSelector == reducer counter of store
<pre>
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { decrement, increment } from "../features/counter/counterSlice";

export default function Counter() {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <>
      <div
        style={{
          display: "flex",
          flexDirection: "column",
          justifyContent: "center",
          width: "40%",
          alignItems: "center",
        }}
      >
        <button onClick={() => dispatch(increment())}>Increment</button>
        <span>{count}</span>
        <button onClick={() => dispatch(decrement())}>Decrement</button>
      </div>
    </>
  );
}
</pre>


<h2>Conclusion</h2>
Franly , redux is more of a flow wich you need to follow instead of trying hard to understand each and every logic .

Lets revise all the steps again –
<ul>
<li>Step 1 – Install the redux and react-redux package</li>
<li>Step 2 – Create a store</li>
<li>Step 3 – Providing store globally</li>
<li>Step 4 – Creating slices (i.e reducers) , where all the major logics are performed</li>
<li>Step 5 – Receiving action from UI (using useDispatch hook) and receiving data from global store to fronted (using useSelector hook).</li>
 </ul>




















