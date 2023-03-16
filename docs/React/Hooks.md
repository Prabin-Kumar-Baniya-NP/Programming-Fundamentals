# Hooks

## useState

```js
import React, { useState } from "react";

function UseStateWithObject() {
  const [name, setName] = useState({
    firstName: "",
    lastName: "",
  });

  return (
    <div>
      <form>
        <input
          type="text"
          value={name.firstName}
          onChange={(e) => setName({ ...name, firstName: e.target.value })}
        />
        <input
          type="text"
          value={name.lastName}
          onChange={(e) => setName({ ...name, lastName: e.target.value })}
        ></input>
        <h4>First Name is {name.firstName}</h4>
        <h4>Last Name is {name.lastName}</h4>
        <h5>{JSON.stringify(name)}</h5>
      </form>
    </div>
  );
}

export default UseStateWithObject;
```

## useEffect

```js
import React, { useState, useEffect } from "react";

function MyComponent() {
  const [data, setData] = useState([]);

  useEffect(() => {
    async function fetchData() {
      const response = await fetch("https://example.com/api/data");
      const json = await response.json();
      setData(json);
    }

    fetchData();
  }, []);

  return (
    <div>
      {data.map((item) => (
        <div key={item.id}>
          <h2>{item.title}</h2>
          <p>{item.description}</p>
        </div>
      ))}
    </div>
  );
}
```

## useContext

```js
import React, { createContext, useContext } from "react";

const MyContext = createContext({});

function ParentComponent() {
  const data = { message: "Hello from parent component" };

  return (
    <MyContext.Provider value={data}>
      <ChildComponent />
    </MyContext.Provider>
  );
}

function ChildComponent() {
  const data = useContext(MyContext);

  return (
    <div>
      <h2>{data.message}</h2>
      <GrandchildComponent />
    </div>
  );
}

function GrandchildComponent() {
  const data = useContext(MyContext);

  return (
    <div>
      <p>{data.message}</p>
    </div>
  );
}
```

## useRef

```js
import React, { useState, useRef } from "react";

function RefExample() {
  const [num, setNum] = useState();
  const inputText = useRef();
  const inputNum = useRef();

  function changeColor() {
    inputText.current.style.color = "red";
    inputNum.current.style.color = "blue";
  }
  return (
    <div>
      useRef example: <br />
      <input
        ref={inputText}
        type="text"
        value={num}
        onChange={(e) => setNum(e.target.value)}
      />
      <br />
      <input
        ref={inputNum}
        type="num"
        value={num}
        onChange={(e) => setNum(e.target.value)}
      />
      <br />
      <button onClick={changeColor}>Change Color</button>
    </div>
  );
}

export default RefExample;
```

## useReducer

```js
import React, { useReducer, useState } from "react";
import TodoCard from "./TodoCard";

export const ACTIONS = {
  ADD_TODO: "add_todo",
  TOGGLE_TODO: "toggle_todo",
  DELETE_TODO: "delete_todo",
};

function reducer(todos, actions) {
  switch (actions.type) {
    case ACTIONS.ADD_TODO:
      return [...todos, newTodo(actions.payload.name)];
    case ACTIONS.TOGGLE_TODO:
      return todos.map((todo) => {
        if (todo.id === actions.payload.id) {
          return { ...todo, complete: !todo.complete };
        } else {
          return todo;
        }
      });
    case ACTIONS.DELETE_TODO:
      return todos.filter((todo) => todo.id !== actions.payload.id);
    default:
      return todos;
  }
}

function newTodo(name) {
  return { id: Date.now(), name: name, completed: false };
}

function TODO() {
  const [todos, dispatch] = useReducer(reducer, []);
  const [name, setName] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
    dispatch({ type: ACTIONS.ADD_TODO, payload: { name: name } });
    setName("");
  }

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={name}
          onChange={(e) => setName(e.target.value)}
        />
        <input type="submit" value="Submit" />
      </form>
      {todos.map((todo) => {
        return (
          <TodoCard id={todo.id} todo={todo} dispatch={dispatch}></TodoCard>
        );
      })}
    </div>
  );
}

export default TODO;
```

## useMemo

- useMemo is used to memoize a value.

```js
import React, { useState, useEffect, useMemo } from "react";

function MemoExample() {
  const [number, setNumber] = useState(0);

  const getNumber = useMemo(() => {
    return heavyComputation(number);
  }, [number]);

  function heavyComputation(number) {
    for (let i = 0; i <= 100000000; i++) {
      if (i % 2 === 0) {
        i = i + 1 - 1;
      } else {
        i = i + 1 - 1;
      }
    }
    console.log("Computation Completed");
    return 2;
  }
  return (
    <div>
      <button onClick={() => setNumber(getNumber)}>{number}</button>
    </div>
  );
}

export default MemoExample;
```

## useCallback

- useCallback is used to memoize a function.

```js
import React, { useState, useCallback } from "react";

function CallbackExample() {
  const [number, setNumber] = useState(0);

  const getNumber = useCallback(() => {
    return heavyComputation(number);
  }, [number]);

  function heavyComputation(number) {
    for (let i = 0; i <= 100000000; i++) {
      if (i % 2 === 0) {
        i = i + 1 - 1;
      } else {
        i = i + 1 - 1;
      }
    }
    console.log("Computation Completed");
    return 2;
  }
  return (
    <div>
      Callback Example:
      <button onClick={() => setNumber(getNumber)}>{number}</button>
    </div>
  );
}

export default CallbackExample;
```
