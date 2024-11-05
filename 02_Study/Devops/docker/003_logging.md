In a Docker Compose file, logging configuration is specified under the `services` section, where you can define how logs from your containers are managed. Docker supports different logging drivers that allow you to control how logs are collected and stored. 

### Basic Structure of Logging in Docker Compose

In your `docker-compose.yml` file, you can specify the logging options under a service like this:

```yaml
version: '3.8'

services:
  my_service:
    image: my_image
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"
```

### Available Logging Drivers

Docker provides several logging drivers, each suited for different use cases. Here are some commonly used ones:

1. **json-file**: This is the default logging driver. Logs are stored as JSON on the host's filesystem. You can configure options like `max-size` and `max-file` to control log file sizes and the number of log files.

2. **syslog**: Sends logs to a syslog server. This is useful for centralized logging.

3. **journald**: Uses the systemd journal for logging.

4. **gelf**: Sends logs to a Graylog Extended Log Format (GELF) endpoint. This is typically used with services like Graylog for log management and analysis.

5. **fluentd**: For using Fluentd to aggregate logs.

6. **awslogs**: Sends logs to AWS CloudWatch.

7. **splunk**: Sends logs to a Splunk server.

8. **none**: Disables logging.

### Using GELF with an Express API

To use the GELF logging driver with a basic Express API, you'll need a GELF-compatible logging service (like Graylog) running and accessible. Here's how you can set it up.

#### Step 1: Create a Basic Express API

First, set up a simple Express API. Create a folder for your project and run the following commands:

```bash
mkdir express-gelf-logger
cd express-gelf-logger
npm init -y
npm install express bunyan-gelf
```

Create an `index.js` file:

```javascript
const express = require('express');
const bunyan = require('bunyan');
const bunyanGelf = require('bunyan-gelf');

const app = express();
const PORT = process.env.PORT || 3000;

// Configure logging
const logger = bunyan.createLogger({
  name: 'my-express-api',
  streams: [
    {
      level: 'info',
      type: 'raw',
      stream: bunyanGelf.createGelfStream({
        host: 'your-graylog-server-host',
        port: 12201, // Default GELF port
        hostname: 'my-express-api',
      }),
    },
  ],
});

// Sample route
app.get('/', (req, res) => {
  logger.info('Root endpoint hit');
  res.send('Hello World!');
});

app.listen(PORT, () => {
  logger.info(`Server is running on port ${PORT}`);
});
```

Replace `your-graylog-server-host` with the actual host of your Graylog server.

#### Step 2: Create a Dockerfile

Create a `Dockerfile` for your Express app:

```Dockerfile
# Use the official Node.js image.
FROM node:14

# Create and set the working directory.
WORKDIR /usr/src/app

# Copy package.json and install dependencies.
COPY package*.json ./
RUN npm install

# Copy the rest of the application code.
COPY . .

# Expose the app's port.
EXPOSE 3000

# Command to run the application.
CMD ["node", "index.js"]
```

#### Step 3: Update docker-compose.yml

Now, create or update your `docker-compose.yml` file:

```yaml
version: '3.8'

services:
  my-express-api:
    build: .
    ports:
      - "3000:3000"
    logging:
      driver: "gelf"
      options:
        gelf-address: "udp://your-graylog-server-host:12201" # Replace with your Graylog server
```

### Step 4: Build and Run the Application

Run the following commands in your project directory:

```bash
docker-compose up --build
```

### Step 5: Verify Logs

1. Make a request to your Express API (e.g., `http://localhost:3000/`).
2. Check your Graylog interface to verify that the logs are being received correctly.

### Summary

By configuring logging in your Docker Compose file, you can effectively manage and route logs from your services. The GELF driver allows integration with centralized logging solutions like Graylog, making it easier to monitor and analyze logs from your applications.