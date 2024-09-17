---
tags:
  - backend
  - express
  - javascript
  - morgan
---
# What is logging and why is that needed ?

Generally advanced logging looks like this other than the `console.log`

![[Pasted image 20240721213702.png]]

## Why is this needed ??? 

This is not needed for every application but as the server and api grows, as developers we would need more information than just the console logs such as from which url its coming from and stuffs like that. Although it can be done by creating a wrapper function but using tools like **Morgan** and **Winston** the whole process is much more reliable and seemless and less hectic for us.

They provide greate suppport for beautiful looking logs and we can use them as our primary logging object like console.log. 

We can even the error and normal and even every type of logs inside a log file which we can in future push into a database logging table for more details like this

![[Pasted image 20240721214345.png]]

![[Pasted image 20240721214401.png]]

# Set up


```js
// winston.logger.js

import winston from "winston";

const levels = {
  error: 0,
  warn: 1,
  info: 2,
  http: 3,
  debug: 4,
};

const level = () => {
  const env = process.env.NODE_ENV || "development";
  const isDevelopment = env === "development";
  return isDevelopment ? "debug" : "warn";
};


const colors = {
  error: "red",
  warn: "yellow",
  info: "blue",
  http: "magenta",
  debug: "white",
};

winston.addColors(colors);  

const format = winston.format.combine(
  winston.format.timestamp({ format: "DD MMM, YYYY - HH:mm:ss:ms" }),
  winston.format.colorize({ all: true }),
  winston.format.printf(
    info => `[${info.timestamp}] ${info.level}: ${info.message}`
  )
);

const transports = [
  new winston.transports.Console(),
  new winston.transports.File({ filename: "logs/error.log", level: "error" }),
  new winston.transports.File({ filename: "logs/app.log" }),
];

const log = winston.createLogger({
  level: level(),
  levels,
  format,
  transports,
});

const { info, warn, debug, error } = log


export { info, warn, debug, error };
export default log;
```

```js
// morgan.logger.js

import morgan from "morgan";
import winstonLoggerHelper from "./winston.logger.js";

const stream = {
  write: message => winstonLoggerHelper.http(message.trim()),
};

const skip = () => {
  const env = process.env.NODE_ENV || "development";
  return env !== "development";
};

const loggerMiddleware = morgan(
  ":remote-addr :method :url :status - :response-time ms",
  { stream, skip }
);

export { loggerMiddleware };
```