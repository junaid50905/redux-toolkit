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

npm install --save react-redux @reduxjs/toolkit

<h3>Step 2 – Create a global store</h3>
<pre>
 Create src/app/store.js –

import { configureStore } from "@reduxjs/toolkit";

export const store = configureStore({
  reducer: {},
});
</pre>

























