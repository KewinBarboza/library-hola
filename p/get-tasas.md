---
  title: 'get-tasas.ts'
  description: 'component description'
  pubDate: 'August 1, 2024'
  author: 'Kewin Barboza'
  ---
  
  
  
  # get-tasas.ts
  ## Explanation of `fetchGetTasa` Function

The provided code snippet is a JavaScript function that fetches data from an external API endpoint and processes the response to extract specific information. Below is a breakdown of the code:

1. **Function Declaration**:
   - The function `fetchGetTasa` is declared as an asynchronous function using the `async` keyword. This allows the function to use `await` to handle promises in a more readable manner.

2. **Fetching Data**:
   - The function uses the `fetch` API to make a GET request to the URL "https://exchange.vcoud.com/coins/latest" and awaits the response.
   - If the response status is not 200 or `ok` property is false, an error is thrown indicating a communication error with the status code.

3. **Processing Data**:
   - The response data is converted to JSON format using `result.json()`.
   - The data is then filtered to find a specific monitor object with `_id` equal to "5d5e08bb639f395c7fd11da9".
   - If a monitor with the specified `_id` is found, its `price` and `updatedAt` properties are extracted.

4. **Return Value**:
   - The function returns an object containing the `price` as a string under the key `bcv` and the `updatedAt` value.

5. **Error Handling**:
   - Any errors that occur during the execution of the function are caught in the `catch` block, and the error is logged to the console.

### Example Usage:
```javascript
fetchGetTasa()
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error);
  });
```

### Dependencies:
- The code snippet relies on the `fetch` API provided by modern browsers to make HTTP requests.
- It also uses `async/await` syntax for handling promises in a more synchronous way.

This function is designed to fetch a specific monitor's price data from a cryptocurrency exchange API and return it in a structured format for further processing or display.
  
  ## Component Code
  ```jsx
  export const fetchGetTasa = async () => {
  try {
    const result = await fetch("https://exchange.vcoud.com/coins/latest")

    if (result.status !== 200 || result.ok === false) {
      throw new Error(
        `Error de comunicación CriptoDolar. Código: ${result.status}`
      )
    }

    const data = await result.json()

    const getTasaMonitor = data
      .map((monitor: any) => {
        if (monitor._id === "5d5e08bb639f395c7fd11da9") {
          return monitor
        }
      })
      .filter(Boolean)

    const { price, updatedAt } = getTasaMonitor[0]

    return {
      bcv: price.toString(),
      updatedAt
    }

  } catch (error) {
    console.log(error)
  }
}
  ```
  