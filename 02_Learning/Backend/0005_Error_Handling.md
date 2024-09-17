---
tags:
  - express
  - backend
  - javascript
---
# Handling Errors

By default express handles and processes both synchronous and asynchronous errors thrown by the server it self but that stops the server from being rerun on its own so its very crucial that we log those errors using some logging mechanism like this [[0004_advanced_logging#Set up]] ,and also catch those before those effects our server from being active. 

**One thing to notice that the error handlers always should be added as the latest middleware in the server file it should be defined even after all the routes**
# Set up

**As a middleware**

```ts
export function errorHandler(
	err: Error,
	req: Request,
	res: Response<ErrorResponse>,
	next: NextFunction
) {
	const statusCode = res.statusCode !== 200 ? res.statusCode : 500;
	res.status(statuscode);

	const responseBody = {
		message: err.message,
		stack: process.env.NODE_ENV === "production" ? "Shhh" : err.stack
	};

	console.error("Error : ", responseBody);
	res.json(responseBody)
}
```

**As a wrapper for asynchronous errors**

```js
export const asyncHandler = fn => async (req, res, next) => {
  return Promise.resolve(fn(req, res, next)).catch(e => next(e));
}
```


# Other things

Also it is recommended to always create your own APIResponse object which will throw the errors as we want. 

**Like this**

```js
export class APIResponse {
  constructor(statusCode, data, message = "Success", errors = []) {
    this.statusCode = statusCode;
    this.data = data;
    this.message = message;
    this.success = statusCode >= 200 && statusCode < 400;
    this.errors = errors;
  }
}


export class APIError extends Error {
  constructor(
    statusCode,
    message = "Something went wrong!",
    errors = [],
    stack = ""
  ) {
    super(message);
    this.statusCode = statusCode;
    this.errors = errors;
    this.data = null;
    this.stack = !!super.stack ? super.stack?.toString() : stack;

    if (!stack) {
      Error.captureStackTrace(this, this.constructor);
    }
  }
}
```

And they are gonna be used as simple Error objects and also they are throwable.