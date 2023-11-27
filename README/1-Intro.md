### REDUX
#### Introduction
#### Redux Architecture
- Redux is a predictable state container for JavaScript applications, often used in conjunction with libraries like React for building user interfaces. Its architecture revolves around several key concepts:
- By adhering to this architecture, Redux provides a predictable and centralized way of managing state in an application, making it easier to reason about and debug. It's particularly powerful in applications with complex state management requirements.
1. **Store:**
2. **Actions:**
3. **Reducers:**
4. **Action Creators:**
5. **Middleware:**
6. **Selectors:**
2. **Dispatch:**
5. **Store Update:**
6. **Component Re-render:**

#### Props in Redux
#### Action
#### Reducer
#### Root Reducer
#### Container
#### Middleware
- Middleware in Redux is a way to extend the Redux store's behavior. It provides a third-party extension point between dispatching an action and the moment it reaches the reducer. Middleware is commonly used for logging, asynchronous actions, or performing tasks that need to intercept or modify the normal flow of actions.

1. **Redux Thunk:**
- **Purpose:** Allows action creators to return functions instead of plain objects. This is often used for handling asynchronous logic.
- **Example:**
  ```javascript
  const fetchData = () => {
    return async (dispatch) => {
      dispatch(requestData());
      try {
        const data = await api.getData();
        dispatch(receiveData(data));
      } catch (error) {
        dispatch(requestError(error));
      }
    };
  };
  ```

2. **Redux Saga:**
- **Purpose:** Manages side effects (e.g., asynchronous tasks like data fetching) in a more declarative way using generator functions.
- **Example:**
  ```javascript
  function* fetchDataSaga() {
    try {
      const data = yield call(api.getData);
      yield put(receiveData(data));
    } catch (error) {
      yield put(requestError(error));
    }
  }
  
  function* rootSaga() {
    yield takeEvery('FETCH_DATA_REQUEST', fetchDataSaga);
  }
  ```

3. **Redux Logger:**
- **Purpose:** Logs actions and state changes to the console, providing a clear view of what's happening in the application.
- **Example:**
  ```javascript
  import logger from 'redux-logger';
  
  const store = createStore(
    rootReducer,
    applyMiddleware(logger)
  );
  ```

4. **Redux Promise Middleware:**
- **Purpose:** Allows action creators to return promises. It dispatches pending, fulfilled, and rejected actions based on the promise resolution.
- **Example:**
  ```javascript
  const fetchData = () => ({
    type: 'FETCH_DATA',
    payload: api.getData(),
  });
  ```

5. **Redux Batched Actions:**
- **Purpose:** Allows dispatching multiple actions in a batch, which can improve performance in certain scenarios.
- **Example:**
  ```javascript
  import { batchedSubscribe } from 'redux-batched-subscribe';
  
  const store = createStore(
    rootReducer,
    applyMiddleware(...middleware),
  );
  
  batchedSubscribe((notify) => {
    notify();
  })(store);
  ```

When using middleware, it's added to the store during its creation using `applyMiddleware` from the Redux library. Middleware can be composed, allowing multiple middleware to be applied in a specific order. Each middleware has access to the `dispatch` and `getState` functions of the Redux store.

Keep in mind that the middleware you choose depends on the specific requirements of your application. The examples above cover common use cases, but there are many other middleware options available in the Redux ecosystem.
#### Selector

### Interview Questions
Certainly! Here are some common Redux interview questions that you might encounter:

1. **What is Redux?**
   - Redux is a predictable state container for JavaScript applications. It helps manage the state of an application in a predictable way by maintaining a single source of truth.

2. **What are the core principles of Redux?**
   - Single source of truth
   - State is read-only
   - Changes are made with pure functions

3. **Explain the concept of "actions" in Redux.**
   - Actions are plain JavaScript objects that describe changes in the application state. They must have a `type` property indicating the type of action to be performed.

4. **What is a "reducer" in Redux?**
   - A reducer is a pure function that takes the current state and an action as arguments and returns the next state of the application.

5. **What is a "store" in Redux?**
   - The store is an object that holds the application state and allows access to the state, dispatching actions, and registering listeners.

6. **Explain the role of the "dispatch" function.**
   - The `dispatch` function is used to dispatch actions to the Redux store. It is the only way to trigger a state change.

7. **What is the purpose of the "connect" function in React-Redux?**
   - The `connect` function is used to connect a React component to the Redux store. It provides the component with the necessary state and action dispatchers.

8. **What is the purpose of the "mapStateToProps" and "mapDispatchToProps" functions?**
   - `mapStateToProps` is used to subscribe the component to updates from the Redux store, while `mapDispatchToProps` is used to provide the component with callback functions that dispatch actions.

9. **Explain the concept of "middleware" in Redux.**
   - Middleware in Redux provides a way to extend the behavior of the `dispatch` function. It allows you to perform additional tasks such as logging, asynchronous actions, etc., before the action reaches the reducer.

10. **What is the difference between "container components" and "presentational components" in the context of React-Redux?**
    - Container components are connected to the Redux store and are responsible for passing down the state and action dispatchers to presentational components. Presentational components are concerned with how things look and receive data and callbacks via props.

11. **How does Redux handle asynchronous operations?**
    - Redux itself does not handle asynchronous operations, but middleware like Redux Thunk or Redux Saga can be used to handle asynchronous logic. Thunk allows action creators to return functions instead of plain objects, enabling asynchronous operations.

12. **Explain the concept of "selectors" in the context of Redux.**
    - Selectors are functions that take the Redux state as an argument and return specific pieces of the state. They are used to encapsulate the logic for extracting specific data from the state.

These questions cover a range of topics related to Redux. Depending on the position you're interviewing for, you may encounter more in-depth questions about specific aspects of Redux or its integration with React.