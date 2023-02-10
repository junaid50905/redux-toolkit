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
 Create src/app/store.js –
<pre>

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


## exmaples: 



- configureStore
  - reducer
- createSlice
  - name
  - initialState
  - reducers
    - reducer
    - prepare
- useDispatch and useSelector
## 1

### i.store.jsx
```javascript
import {
    configureStore
} from "@reduxjs/toolkit";

import bookReducer from '../features/Book/BookSlice'

export const store = configureStore({
    reducer: {
        book: bookReducer,
    },
});

```
### ii.main.jsx

```javascript
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import './index.css'
import { store } from "./app/store";
import { Provider } from "react-redux";

ReactDOM.createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </Provider>
  ,
)

```
### iii.bookSlice.js
```javascript

import {createSlice} from "@reduxjs/toolkit";

const initialState = {
    booksList: []
};

export const bookSlice = createSlice({
    name: "book",
    initialState,
    reducers: {
        addBook: (state, action) => {
            state.booksList.push(action.payload)
        }
    }
});

export const { addBook } = bookSlice.actions

export default bookSlice.reducer;

```
### iv.BookList.jsx(ui)
```javascript
import { nanoid } from '@reduxjs/toolkit'
import React,{useState} from 'react'
import { useDispatch } from 'react-redux'
import { addBook } from '../features/Book/BookSlice'

const BookList = () => {
    const [bookName, setBookName] = useState('')
    const [bookAuthor, setBookAuthor] = useState('')
    const [bookPrice, setBookPrice] = useState('')

    const dispatch = useDispatch()

    const submitHandler = (e)=>{
        e.preventDefault()
        dispatch(addBook({ id: nanoid(), name: bookName, author: bookAuthor, price: bookPrice, date: new Date()}))
    }
  return (
    <div>
      <form action="" onSubmit={submitHandler}>
        <input type="text" onChange={(e)=> setBookName(e.target.value)} value={bookName} placeholder="book name"/>
        <input type="text" onChange={(e)=> setBookAuthor(e.target.value)} value={bookAuthor} placeholder="book author"/>
        <input type="text" onChange={(e)=> setBookPrice(e.target.value)} value={bookPrice} placeholder="book price"/>
        <button type='submit'>add</button>
      </form>
    </div>
  )
}

export default BookList

```


![Logo](https://i.ibb.co/DrNbf08/Screenshot-20230208-065219.png)


## 2
1 এ  আমরা দেখেছি ui থেকে { id: nanoid (),: bookName, author: bookAuthor, price: bookPrice, date : new Date ()}) payload হিসেবে পাঠনো হয়েছে।  কিন্তু ui  থেকে কিন্তু আমরা name, author, price পাঠাচ্ছি।  তাই ইটা আমরা এই দুই নম্বর এক্সাম্পল দিয়ে সল্ভ করবো। 

reducer  আর মাধ্যমে handle করবো ui থেকে যেটা পাঠনো হচ্ছে ,আর prepare এর মাধ্যমে handle করবো ui থেকে যেই data পাওয়া যায় না 


### i. BookList.jsx(ui)
```javascript
import React,{useState} from 'react'
import { useDispatch } from 'react-redux'
import { addBook } from '../features/Book/BookSlice'

const BookList = () => {
    const [bookName, setBookName] = useState('')
    const [bookAuthor, setBookAuthor] = useState('')
    const [bookPrice, setBookPrice] = useState('')

    const dispatch = useDispatch()

    const submitHandler = (e)=>{
        e.preventDefault()
        dispatch(addBook({ name: bookName, author: bookAuthor, price: bookPrice}))
    }
  return (
    <div>
      <form action="" onSubmit={submitHandler}>
        <input type="text" onChange={(e)=> setBookName(e.target.value)} value={bookName} placeholder="book name"/>
        <input type="text" onChange={(e)=> setBookAuthor(e.target.value)} value={bookAuthor} placeholder="book author"/>
        <input type="text" onChange={(e)=> setBookPrice(e.target.value)} value={bookPrice} placeholder="book price"/>
        <button type='submit'>add</button>
      </form>
    </div>
  )
}

export default BookList

``` 

### ii. bookSlice.js
```javascript
import {createSlice,nanoid} from "@reduxjs/toolkit";


const initialState = {
    booksList: []
};

export const bookSlice = createSlice({
    name: "book",
    initialState,
    reducers: {
        addBook: {
            reducer: (state, action) => {
                state.booksList.push(action.payload)
            },
            prepare: (value) => {
                return {
                    payload: {
                        ...value,
                        id: nanoid(),
                        date: new Date()
                    }
                }
            }
        }
    }
});

export const { addBook } = bookSlice.actions

export default bookSlice.reducer;

```




## 3 createAsyncThunk
---------
#### postsSlice.js

```javascript
import { createAsyncThunk, createSlice } from "@reduxjs/toolkit";

export const getPosts = createAsyncThunk(
    'posts/getPosts',
    async() => {
        return await fetch('https://jsonplaceholder.typicode.com/posts').then((res) => res.json())
    }
)

const initialState = {
    postsList: [],
    isLoading: false,
    error: ''
}
const postsSlice = createSlice({
    name: 'posts',
    initialState,
    extraReducers: {
        [getPosts.pending]: (state) => {
            state.isLoading = true
        },
        [getPosts.fulfilled]: (state, action) => {
            state.postsList = action.payload,
                state.isLoading = false
        },
        [getPosts.rejected]: (state, action) => {
            state.isLoading = false
        },
    }
})


export default postsSlice.reducer

```

#### store.js

```javascript
import {
    configureStore
} from "@reduxjs/toolkit";

import bookReducer from '../features/Book/BookSlice'
import postsReducer from '../features/products/productsSlice'

export const store = configureStore({
    reducer: {
        book: bookReducer,
        posts: postsReducer
    }
});
```

#### PostsList.jsx

```javscript
import React,{useEffect} from 'react'
import { useDispatch } from 'react-redux'
import { getPosts } from '../features/products/productsSlice'

const PostsList = () => {
    const dispatch = useDispatch()
    useEffect(()=>{
        dispatch(getPosts())
    },[dispatch])
  return (
    <div>
      postslist
    </div>
  )
}

export default PostsList


```

#### output preview

![Logo](https://i.ibb.co/PFWXThR/Screenshot-20230210-101623.png)












