---
tags:
  - backend
  - cache
  - http
  - server
---
# Caching using the default HTTP Headers.

There is a HTTP header for default caching for the servers to not re create the same response which will use more computations to redo the same response which the server just did inside the preset time period for cache.

The header is `Cache-control`, 

It will typically have a age for the caching to be done. And the state where we can tell the browser how to store the cache.

[More Info here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)

# How to use as Middlewares in express app

We can use this header in our code to increase the performance of our server and for that we have to simply create a middleware.

Like this 

```ts
const setCache = (req: Request, res: Response, next: NextFuntion) => {
	const period = 60 * 5; // age that tells the browser how much seconds the cache is gonna be in the store

	if (req.method == "GET") {
		res.set("Cache-control", `public, max-age=${period}`);
	} else {
		res.set("Cache-control", "no-store");
	}

	next();
}
```