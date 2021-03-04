---
title: fetch api cheatsheet
date: 2021-03-02
tag: tech
duration: 7min
---

## Fetch API Cheatsheet

### Simple GET request with the Fetch API

```js
fetch('{url}').then((response) => console.log(response));
```

### Simple POST request with the Fetch API

```js
fetch('{url}', {
  method: 'post'
}).then((response) => console.log(response));
```

### GET with an authorization token (Bearer) in the Fetch API

```js
fetch('{url}', {
  headers: {
    Authorization: 'Basic {token}'
  }
}).then((response) => console.log(response));
```

### GET with querystring data in the Fetch API

```js
fetch('{url}?var1=value1&var2=value2').then((response) =>
  console.log(response)
);
```

### GET with CORS in the Fetch API

```js
fetch('{url}', {
  mode: 'cors'
}).then((response) => console.log(response));
```

### POST with authorization token and querystring data in the Fetch API

```js
fetch('{url}?var1=value1&var2=value2', {
  method: 'post',
  headers: {
    Authorization: 'Bearer {token}'
  }
}).then((response) => console.log(response));
```

### POST with form data in the Fetch API

```js
let formData = new FormData();
formData.append('field1', 'value1');
formData.append('field2', 'value2');

fetch('{url}', {
  method: 'post',
  body: formData
}).then((response) => console.log(response));
```

### POST with JSON data in the Fetch API

```js
fetch('{url}', {
  method: 'post',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    field1: 'value1',
    field2: 'value2'
  })
}).then((response) => console.log(response));
```

### POST with JSON data and CORS in the Fetch API

```js
fetch('{url}', {
  method: 'post',
  mode: 'cors',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    field1: 'value1',
    field2: 'value2'
  })
}).then((response) => console.log(response));
```

### How to process the results of the Fetch API request

The Fetch API returns a Promise. Thatʼs why Iʼm always using .then() and a callback function for processing the response:

```js
fetch(...).then(response => {
    // process the response
}
```

But you can also await the result if youʼre in an async function:

```js
async function getData(){
    let data = await fetch(...);
    // process the response
}
```

Now letʼs take a look at how we can extract the data from the response:

### How to check the status code of the Fetch API response

When sending POST, PATCH, and PUT requests, we are typically interested in the return status code:

```js
fetch(...)
    .then(response => {
        if (response.status == 200){
            // all OK
        } else {
            console.log(response.statusText);
        }
    });
```

### How to get a simple value of the Fetch API response

Some API endpoints may send back an identifier of a new database record that was created using your data:

```js
var userId;

fetch(...)
    .then(response => response.text())
    .then(id => {
        userId = id;
        console.log(userId)
    });
```

### How to convert JSON data of the Fetch API response

But in most cases, youʼll receive JSON data in the response body:

```js
var dataObj;

fetch(...)
    .then(response => response.json())
    .then(data => {
        dataObj = data;
        console.log(dataObj)
    });
```

Keep in mind that you can access the data only after both Promises are resolved. This is sometimes a bit confusing, so I always prefer to use async methods and await the results:

```js
async function getData(){
    var dataObj;

    const response = await fetch(...);
    const data = await response.json();
    dataObj = data;
    console.log(dataObj);
}
```
