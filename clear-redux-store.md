### For clearing data from Redux store we can create action responsible for that:

```
import { combineReducers } from "redux";
import { DESTROY_SESSION } from "../actions/types";

const appReducer = combineReducers({
   state: (state = {}) => state
});

const rootReducer = (state, action) => {   
   if(action.type === DESTROY_SESSION)
      state = undefined;
   
   return appReducer(state, action);
};

export default rootReducer;
```

Usage:

```
import { DESTROY_SESSION } from "./types";
export const onLogout = () => {
   return dispatch => {
      dispatch({ type: DESTROY_SESSION });
   };
}
```

### Above code will clear Redux store completely, if we need to partially clear store we can use object destructuring:

```
  if (action.type === 'DESTROY_SESSION') {
    const { users, comment } = state;
    state = { users, comment };
  }
```

If we need to clear data from Redux store on page/component unmount we need to have action for that and dispatch it on component unmount.
Basic idea is, define a new action type in reducer file to clear the table data, and before unmount dispatch that action.

In Component:

```
  componentDidMount() {
    this.fetch();
  }

  componentWillUnmount() {
    this.props.clearTableData();
  }

  const mapDispatchToProps = dispatch => (
    bindActionCreators({ getTableData, clearTableData }, dispatch)
  )
```

Action:
```
  export const clearTableData = () => {
    return { type: TYPES.CLEAR_TABLE_DATA };
  };
```

Reducer:
```
  case TYPES.CLEAR_TABLE_DATA: {
    // reset the table data here, and return
  }
```

### **NOTE 1**
In case we are using redux-persist, we also need to clean storage. 
Redux-persist keeps a copy of the state in a storage engine, and the state copy will be loaded on refresh.

### **NOTE 2**
In case of Redux we don't need to worry about huge store. 
One developer reported that they have 
   ~500 action types,
   ~400 reducer cases,
   ~150 components,
   5 middlewares,
   ~200 actions,
   ~2300 tests 
and no performance issues.


Also we can use redux-reset - https://github.com/wwayne/redux-reset

TO DO:

- Redux data flex flow
- Reset on route change
- Reset on multiple requests


