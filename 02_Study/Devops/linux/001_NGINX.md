# What is a Web Server?

Whenever you open your browser, type a URL and then click enter. Basically, you are requesting the contents of that URL. Ever wondered where the content are? Yes, you’re right those are contents placed on remote computers which, after accepting your request, send the contents of that URL back as a response.

Web Servers are computers that deliver the requested web pages. Every web server has an IP address and domain name. 
- A **web server** is software that handles HTTP requests from clients (such as browsers) and serves web content (like HTML, CSS, and images).
- It listens on a specific port (usually 80 or 443 for HTTP and HTTPS, respectively) and responds to incoming requests.
- When you visit a website, your browser sends an HTTP request to the web server, which then sends back the requested content.

# What is NGINX then ??
It is open-source software designed for maximum performance and stability. Let’s see basically why we need it basically see how we can benefit from this.

- Originally created by Igor Sysoev in 2004, Nginx was designed to address the C10k problem (handling 10,000 concurrent connections efficiently).
- Over time, Nginx has become more versatile:
    - **Web Server**: Nginx serves static files (like images) and handles basic HTTP requests.
    - **Reverse Proxy**: It can distribute requests to multiple backend servers (like application servers or other web servers). See this - [[#How to host a Next.js app on Raspberry Pi with nginx]]
    - **Load Balancer**: Nginx balances traffic across multiple servers to improve performance and reliability.
    - **HTTP Cache**: It stores frequently accessed content in memory to reduce load on backend servers.
- **How It Works Under the Hood**:
    - Nginx uses an asynchronous, event-driven model:
        - One master process controls multiple worker processes.
        - Requests are handled concurrently without blocking others.
        - Low memory usage and high concurrency.
    - Common features include reverse proxying, load balancing, FastCGI support, WebSockets, and TLS/SSL handling.
    - Nginx excels in scenarios with static content and high concurrent requests.
    - Notable users include Netflix, NASA, and WordPress.com .

Suppose we develop our application on Django or Node. All such frameworks have built-in development servers to host your project. But whenever someone tries to host that application on the production level with built-in development servers, you’ll get a tough time handling all the requests while experiencing downtimes while just handling 30-40 concurrent requests.

Nginx is a dedicated web server that has solved efficiency issues and provided us with an optimum way to handle 1000s of requests concurrently.

# Why do we need a dedicated webserver?

Suppose we develop our application on Django or Node. All such frameworks have built-in development servers to host your project. But whenever someone tries to host that application on the production level with built-in development servers, you’ll get a tough time handling all the requests while experiencing downtimes while just handling 30-40 concurrent requests.

Nginx is a dedicated web server that has solved efficiency issues and provided us with an optimum way to handle 1000s of requests concurrently.
# Web server for reverse proxy, caching, and load balancing. 

The reverse proxy accepts a request from a client, forwards the request to a server that can fulfill it, and returns the response from the server to the client.

Caching is a technique that stores a copy of a given resource and serves it back when requested. When a web cache has a requested resource in its store, it intercepts the request and returns its copy instead of re-downloading from the originating server.

A load balancer distributes the incoming client requests to a group of servers, in which it can handle concurrent requests without experiencing load on a particular server.

Other features of Nginx are as follows:

- It provides HTTP server capabilities.
- Designed to provide stability and maximum performance.
- Functions as a proxy server for email (IMAP, POP3, and SMTP).
- It uses an event-driven and non-threaded architecture to provide less CPU computation per request served.
- It provides scalability.
- Reduces wait time for the client.
- Upgrades can be done while Nginx is hosting a website without any downtime.

# Difference between nginx and apache web server
1. **Apache**:
    - **Web Server**: Apache is an open-source web server that has been around since 1999. It’s widely used and runs on Unix, Linux, Windows, and Solaris platforms.
    - **Dynamic Content**: Apache is excellent for serving dynamic content (like PHP scripts) and handling complex configurations.
    - **Architecture**: It follows a process-based model, creating a new thread for each request.
    - **Modules**: Apache supports dynamically loaded modules, which can make its configuration complex.
    - **Security**: While secure, its codebase is larger.
    - **Performance**: For static content, Apache’s performance is lower compared to Nginx.
    
1. **Nginx**:
    - **Web Server and More**: Nginx is a lightweight, high-performance web server. It also serves as a reverse proxy and load balancer.
    - **Static Files**: Nginx excels at serving static files (like images, CSS, and JS). It’s often used as a front-end proxy to backend services.
    - **Event-Driven Model**: Nginx uses an event-driven approach, handling multiple client requests efficiently.
    - **Security**: Nginx provides better security with a smaller codebase.
    - **Performance**: Nginx’s performance for static content is significantly faster than Apache.
    - **Companies Using Nginx**: IBM, Google, GitLab, DuckDuckGo, and more.

In summary, Apache is versatile for dynamic content, while Nginx shines with static files and efficient event-driven processing. [Choose based on your specific use case! 😊🚀](https://www.geeksforgeeks.org/difference-between-apache-and-nginx/)

---

# How to host a Next.js app on Raspberry Pi with nginx

Certainly! You can deploy your Next.js app on a Raspberry Pi using Nginx. Here’s a step-by-step guide:

1. **Install Nginx**: First, ensure that Nginx is installed on your Raspberry Pi. If it’s not already installed, run the following commands:
    
    ```bash
    sudo apt-get update
    sudo apt-get install nginx
    ```
    
2. **Clone Your Next.js App**: Clone your Next.js app repository to your Raspberry Pi using Git:
    
    ```bash
    git clone <your_app_repository_url>
    ```
    
3. **Install Dependencies and Build**: Navigate to your app directory and install its dependencies:
    
    ```bash
    cd <your_app_directory>
    npm install
    npm run build
    ```
    
4. **Set Up PM2**: Install PM2, a process manager that keeps your app running in the background and restarts it if it crashes:
    
    ```bash
    npm install -g pm2
    pm2 start npm --name "your-app-name" -- start
    ```
    
5. **Configure Nginx**: Create an Nginx configuration file for your app (replace `your-app-name.com` with your domain):
    
    ```bash
    sudo nano /etc/nginx/sites-available/your-app-name.com
    ```
    
    Inside the file, add the following code:
    
    ```nginx
    server {
        listen 80;
        server_name your-domain-name.com www.your-domain-name.com;
        location / {
            proxy_pass http://localhost:3000;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
    ```
    
    Save the file, create a symbolic link, and restart Nginx:
    
    ```bash
    sudo ln -s /etc/nginx/sites-available/your-app-name.com /etc/nginx/sites-enabled/
    sudo systemctl restart nginx
    ```
    
6. **DNS Configuration**: Make sure your domain name points correctly to your Raspberry Pi.
    

That’s it! [Your Next.js app should now be accessible via Nginx on your Raspberry Pi. 🚀](https://dev.to/j3rry320/deploy-your-nextjs-app-like-a-pro-a-step-by-step-guide-using-nginx-pm2-certbot-and-git-on-your-linux-server-3286)[1](https://dev.to/j3rry320/deploy-your-nextjs-app-like-a-pro-a-step-by-step-guide-using-nginx-pm2-certbot-and-git-on-your-linux-server-3286)[2](https://www.bugpilot.com/guides/en/how-to-deploy-nextjs-app-using-nginx-4efa)

---
