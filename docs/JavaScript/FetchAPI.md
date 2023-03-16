# Fetch API
```js
url = 'https://reqres.in/api/users/23';
params = {
    method: 'POST',
    headers: {
        'Content-type' : 'application/json',
    },
    body: JSON.stringify({
        name: 'User 1',
    })
}


fetch(url, params).
    then(res => res.json())
    .then(data => console.log(data))
    .catch(error => console.log('Error'))
```