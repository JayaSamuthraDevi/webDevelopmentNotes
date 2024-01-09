# React with Redux Toolkit

install neccessary packages:
```npm install @reduxjs/toolkit```
```npm install react-redux```
![image](https://github.com/JayaSamuthraDevi/webDevelopmentNotes/assets/115087700/8f9ce2a9-12c7-410c-abe0-f2b2988fe7c1)

## example of Slice
```import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";
import { fetch_get, fetch_getNotAuth } from "../utils";

export const showList = createAsyncThunk(
  "showList",
  async (args,{ rejectWithValue }) => {
    const response = await fetch_getNotAuth("http://192.168.1.197:5005/recommendation/get")
    try {
      const result = await response.data
      return result
    } catch (error) {
      return rejectWithValue(error)
    }
  }
);


export const interestList = createSlice({
  name: "interestList",
  initialState: {
    lists: [],
    loading: false,
    error: null,
  },
  reducers: {
    curdList: (state, action) => {
      return {...state, lists: action.payload}
    }
  },
  extraReducers: (builder) =>{
    builder.addCase(showList.pending, (state)=>{
      state.loading = true;
    })
    builder.addCase(showList.fulfilled, (state, action)=>{
      state.loading = false;
      state.lists = action.payload
    })
    builder.addCase(showList.rejected, (state, action)=>{
      state.loading = false;
      state.error = action.payload;
    })
  }
});

export const {
  curdList,
 } = interestList.actions;

export default interestList.reducer;
```

## example for store
```
import { userDetail } from "../Reducers/userDetailsSlice";
import { interestList } from "../Reducers/interestListsSlice";
import { recommendationList } from "../Reducers/recommendationListsSlice";
import { applyMiddleware, combineReducers, compose, createStore } from "redux";
import thunk from "redux-thunk";
import { post } from "../Reducers/postsSlice";


const middleware = applyMiddleware(thunk);

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

const reducers = combineReducers({
  list_interest: interestList.reducer,
  userDetails: userDetail.reducer,
  followSuggestion: recommendationList.reducer,
  posts:post.reducer,


});

export const store = createStore(reducers, composeEnhancers(middleware));
```
## example for dispatching an action
```const dispatch = useDispatch();
  useEffect(() => {
    dispatch(showList());
  }, []);
```
## example for fetching data from store
``` const lists = useSelector((state) => {
    return state.list_interest.lists;
  });
```
