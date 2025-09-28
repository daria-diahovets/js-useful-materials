# All about fetching in JavaScript

- **Promise** - way to handle async results
- **fetch()** - API for making HTTP requests, return a Promise
- **async/await** - cleaner syntax

|   № | Content                                           |
| --: | ------------------------------------------------- |
|   1 | [Promises in Javascript](#promises-in-javascript) |
|   2 | [The `fetch()` API](#)                            |
|   2 | [Async/Await](#)                                  |

## Promises in Javascript

A Promise is an object representing the eventual result (or failure) of an asynchronous operation.
It has 3 states:

- pending -> operation hasn't finished yet.
  ![Promise-pending](/images/github_pending.png)
- fulfilled -> operation finished successfully (resolve was called).
  ![Promise-fulfilled](/images/github_fulfilled.png)
- rejected -> operation failed (reject wal called).
  ![Promise-rejected](/images/github_rejected.png)

**Example:**

```javascript
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve("Successful message! (it's your own message)");
    } else {
      reject("Something went wrong! (it's your own message)");
    }
  }, 1000);
});

myPromise
  .then((result) => console.log(result))
  .catch((error) => console.error(error))
  .finally(() => console.log("Done!"));
```

## The `fetch()` API

The `fetch()` function is an built-in way to make **HTTP requests** in the browser (and in NodeJS if supported or polyfilled).
It always returns a **Promise**.

**Example:**

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => {
    if (!response.ok) {
      throw new Error("Something went wrong.");
    }
    return response.json();
  })
  .then((data) => console.table(data))
  .catch((error) => console.error(error));
```

![fetch](/images/github_fetch.png)

**Notes:**

- `fetch()` doesn't reject on HTTP errors (like 404 or 500). It only rejects on network errors. That's why we check `response.ok`.
- To read the body, you must call a method like `.json()`, `.text()`, `.blob()`, etc. These also return Promises.

## Async/Await

`async/await` is **syntactic sugar** over Promises, making asynchronous code look synchronous.

- `async` before a function makes it return **Promise**.
- `await` pauses execution inside an async function until a Promise resolves (or rejects)

**Example:**

```javascript
async function getPost() {
  try {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/posts/1",
    );
    if (!response.ok) {
      throw new Error(`HTTP error ${response.status}`);
    }

    const data = await response.json();
    console.log(`Data: ${data}`);
  } catch (error) {
    console.error(error);
  }
}
getPost();
```

## fetchData() function example

```javascript
async function fetchData(url, method = "GET", data = null) {
  try {
    const options = {
      method,
      headers: {
        "Content-Type": "application/json",
      },
    };

    if (method === "POST" && data) {
      options.body = JSON.stringify(data);
    }

    const response = await fetch(url, options);

    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }

    return await response.json();
  } catch (error) {
    console.error("Fetch error: ", error.message);
    throw error;
  }
}
```
