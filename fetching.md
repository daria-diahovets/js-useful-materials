# All about fetching in JavaScript

- **Promise** - way to handle async results
- **fetch()** - API for making HTTP requests, return a Promise
- **async/await** - cleaner syntax

|   № | Content                     |
| --: | --------------------------- |
|   1 | [Promises in Javascript](#) |
|   2 | [](#)                       |

## Promises in Javascript

A Promise is an object representing the eventual result (or failure) of an asynchronous operation.
It has 3 states:

- pending -> operation hasn't finished yet.
  ![Promise pending](/images/pending.png")
- fulfilled -> operation finished successfully (resolve was called).
  ![Promise fulfilled](/images/fulfilled.png")
- rejected -> operation failed (reject wal called).
  ![Promise rejected](/images/rejected.png")

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
