# Async Await

```js
async function getJSON2(){
   try {
    let response = await fetch("https://jsonplaceholder.typicode.com/todos/2");

    if (!response.ok){
        throw new Error(`HTTP status ${response.status}`);
    }
    let data = await response.json();
    console.log(data);
   }
   catch(error){
       console.log(error);
   }
}
getJSON2();
```