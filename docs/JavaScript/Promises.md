# Promises

- Promises are used to handle asynchronous operations in JavaScript.

- Benefits of Promises

    - Improves Code Readability
    - Better handling of asynchronous operations
    - Better flow of control definition in asynchronous logic
    - Better Error Handling

- A Promise has four states:
    - fulfilled: Action related to the promise succeeded
    - rejected: Action related to the promise failed
    - pending: Promise is still pending i.e. not fulfilled or rejected yet
    - settled: Promise has fulfilled or rejected

```js
let task1 = new Promise((resolve, reject) => {
  let completed = true;
  if (completed) resolve("Task 1 Downloaded");
  else resolve("Task 1 Failed to download");
});

let task2 = new Promise((resolve, reject) => {
  let completed = false;
  if (completed) resolve("Task 2 Downloaded");
  else resolve("Task 2 Failed to download");
});

let task3 = new Promise((resolve, reject) => {
  let completed = true;
  if (completed) resolve("Task 3 Downloaded");
  else reject("Task 3 Failed to Download");
});

task1
  .then((message) => {
    console.log(message);
  })
  .catch((error) => {
    console.log(error);
  });

task2
  .then((message) => {
    console.log(message);
  })
  .catch((error) => {
    console.log(error);
  });

task3
  .then((message) => {
    console.log(message);
  })
  .catch((error) => {
    console.log(error);
  });

Promise.all([task1, task2, task3])
  .then((messages) => {
    console.log(messages);
  })
  .catch((errors) => {
    console.log("Try again");
  });
```

### Example with an API Request

```js
const axios = require("axios");

const getPosts = () => {
  return new Promise((resolve, reject) => {
    axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then((response) => {
        resolve(response.data);
      })
      .catch((error) => {
        reject(error);
      });
  });
};

getPosts()
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error);
  });
```
