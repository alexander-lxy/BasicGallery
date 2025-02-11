# Nginx

### (1) Install nginx (take MacOS as an example):

#### 1.**Install Homebrew** (if not already installed)

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```



#### 2.Install Nginx

```shell
brew install nginx
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.09.39.png" alt="截屏2025-02-10 下午9.09.39" style="zoom: 50%;" /> 



#### 3.View Nginx status and configuration details

```shell
brew info nginx
```

<img src="/Users/alexanderlee/Desktop/截屏2025-02-10 下午9.29.14.png" alt="截屏2025-02-10 下午9.29.14" style="zoom:50%;" /> 



#### 4.Start Nginx

```
brew services start nginx
```

![截屏2025-02-10 下午9.18.59](/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.18.59.png)

重启后，我们验证下，因为nginx默认的端口号是8080，因此我们页面访问 http://localhost:8080

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.20.20.png" alt="截屏2025-02-10 下午9.20.20" style="zoom: 33%;" /> 



#### 5.Stop Nginx

```
brew services stop nginx
```

  <img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午11.34.46.png" alt="截屏2025-02-10 下午11.34.46" style="zoom: 33%;" />







### (2) Install Nodejs

> Node.js is a JavaScript runtime based on the Chrome V8 engine. We start the server js file written through Nodejs.



#### 1.Install Node

```
brew install node
```



#### 2.View Node Version

**After successful installation you can see:** 

```
node -v
```

![截屏2025-02-10 下午9.47.23](/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.47.23.png)





#### 3.create and start server

**create a folder named nginx and write four server webserver.js files, occupying
ports 2321,2322,2323,2324, using server.listen() to listen to the function. When the
response request is returned, the string "Hello world" is written into http as a request and
displayed on the web page of the browser.**

`webserver1.js`

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 2321;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World from Server One\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```

![截屏2025-02-10 下午9.56.22](/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.56.22.png)

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.56.53.png" alt="截屏2025-02-10 下午9.56.53" style="zoom: 50%;" /> 



`webserver2.js`

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 2322;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World from Server Two\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```

![截屏2025-02-10 下午9.57.25](/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.57.25.png)

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.59.12.png" alt="截屏2025-02-10 下午9.59.12" style="zoom:50%;" /> 



`webserver3.js`

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 2323;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World from Server Three\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```

![截屏2025-02-10 下午9.58.16](/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.58.16.png)

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.58.37.png" alt="截屏2025-02-10 下午9.58.37" style="zoom:50%;" /> 



`webserver4.js`

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 2324;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World from Server Four\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```

![截屏2025-02-10 下午9.59.36](/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.59.36.png)

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午10.00.11.png" alt="截屏2025-02-10 下午10.00.11" style="zoom:50%;" /> 



#### 4.Use Shell Script to Start Server 

- Create a startup script named `start-web-servers.sh`

```shell
#!/bin/bash

echo -e "\nStarting all web servers...\n"

node webserver1.js &
node webserver2.js &
node webserver3.js &
node webserver4.js &

sleep 1
```

- Create a shutdown script named `stop-web-servers.sh`

```shell
#!/bin/bash

for PORT in {2321..2324}; do
  PID=$(lsof -ti :$PORT)
  if [ -z "$PID" ]; then
    echo "Port $PORT is not in use."
  else
    echo "Port $PORT is being used by process $PID. Killing process..."
    kill -9 $PID
    echo "Process $PID killed. Port $PORT is now free."
  fi
done
```

- Grant execution permissions to make both scripts executable:

```
chmod +x start-web-servers.sh &
chmod +x stop-web-servers.sh
```



- To start all services, run:

```
./start-web-servers.sh
```

- To stop the services and free up the ports, run:

```
./stop-web-servers.sh
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午11.10.58.png" alt="截屏2025-02-10 下午11.10.58" style="zoom:50%;" /> 

关闭所有服务

```
./stop-web-servers.sh
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午11.11.24.png" alt="截屏2025-02-10 下午11.11.24" style="zoom:50%;" /> 







### (3) Modify the nginx configuration file

#### 1. Open `nginx.conf`

Open configuration file `nginx.conf`and Change the original port number 8080 to an unused one.

- Nginx.conf

```
vim /usr/local/etc/nginx/nginx.conf
```

- You can also use the find command to locate it

```
find / -name nginx.conf
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午10.04.14.png" alt="截屏2025-02-10 下午10.04.14" style="zoom:50%;" /> 

#### 2. Change port number

```shell
server {
        listen       2025;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
.....
}
```

Note: Please check if the port is already in use. 

```
lsof -i :<portnumber> // If the port is in use, it will display the process information.
kill -9 <PID> // kill process
```



#### 3.  Configure the server cluster in `nginx.conf` and set to reverse proxy pass

<img src="/Users/alexanderlee/Desktop/截屏2025-02-10 下午10.25.40.png" alt="截屏2025-02-10 下午10.25.40" style="zoom:50%;" /> 

 

`nginx.conf`

```java
......

http {
    ......

    #gzip  on;

		upstream myservers {
        #random;
        server 127.0.0.1:2321;         
        server 127.0.0.1:2322;
        server 127.0.0.1:2323;
        server 127.0.0.1:2324;
    }
    server {
        #listen       8080;
				listen	     2025;
        server_name  localhost;

        ......
        location / {
            root   html;
            index  index.html index.htm;
	    			proxy_pass http://myservers;
        }

    ......
}

```



#### 4. Restart nginx 

```
nginx -s reload
```







### (4) Basic load balancing with NGINX

Send an http request to the server at the command line with the `curl localhost:2025` command, and the nginx proxy server forwards the request to one of the servers in the server cluster and gets the response back. 

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 上午11.34.23.png" alt="截屏2025-02-11 上午11.34.23" style="zoom:50%;" /> 

**Note: To make `nginx.conf` take effect, please execute  `nginx -s reload` to reload Nginx.**

#### 1. Round Robin

> Requests are distributed evenly across the servers, with server weights taken into consideration. This method is used by default.

`nginx.conf`

```js
upstream myservers {
        #random;
        server 127.0.0.1:2321;
        server 127.0.0.1:2322;
        server 127.0.0.1:2323;
        server 127.0.0.1:2324;
    }
```

| Server | Weight（Standard） | Connections |
| ------ | ------------------ | ----------- |
| 2321   | 1                  | 2           |
| 2322   | 1                  | 2           |
| 2323   | 1                  | 2           |
| 2324   | 1                  | 2           |

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 上午10.53.28.png" alt="截屏2025-02-11 上午10.53.28" style="zoom:50%;" /> 





#### 2. Weighted Round Robin

> Based on the standard Round Robin algorithm, each server is assigned a weight, and servers with higher weights receive more requests.

`nginx.conf`

```js
upstream myservers {
        #random;
        server 127.0.0.1:2321 weight=4;
        server 127.0.0.1:2322 weight=2;
        server 127.0.0.1:2323 weight=1;
        server 127.0.0.1:2324 weight=1;
    }

```

| Server | Weight | Connections |
| ------ | ------ | ----------- |
| 2321   | 4      | 4           |
| 2322   | 2      | 2           |
| 2323   | 1      | 1           |
| 2324   | 1      | 1           |

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-11 上午11.09.41.png" alt="截屏2025-02-11 上午11.09.41" style="zoom:50%;" /> 



#### 3. Least Connections

> A request is sent to the server with the least number of active connections, again with server weights taken into consideration

**Simple Algorithm Pseudocode:**

```
1. Initialize the server list serverList = {server1, server2, ..., serverN}
2. For each request:
   a. Find the server with the minimum (active_connections / weight)
   b. Assign the request to that server
   c. Increment the server's active connection count active_connections++
3. After request processing, decrement the active connection count active_connections--
```

`nginx.conf`

```js
upstream myservers {
    	#random;
      least_conn;
    	server 127.0.0.1:2321 weight=4; 
    	server 127.0.0.1:2322 weight=2;
    	server 127.0.0.1:2323 weight=1;
    	server 127.0.0.1:2324 weight=1;
}
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/image-20250211125452947.png" alt="image-20250211125452947" style="zoom:50%;" /> 

| Server | Weight | Connections | Connections / Weight |
| ------ | ------ | ----------- | -------------------- |
| 2321   | 4      | 6           | 1.5                  |
| 2322   | 2      | 3           | 1.5                  |
| 2323   | 1      | 2           | 2                    |
| 2324   | 1      | 1           | 1                    |

**So a new request will be assigned to Server4 since it has the smallest weighted connection count.**

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 下午12.56.39.png" alt="截屏2025-02-11 下午12.56.39" style="zoom:50%;" />    





#### 4. Generic Hash

> The server to which a request is sent is determined from a user‑defined key which can be a text string, variable, or a combination. The key may be a paired source IP address and port, or a URI

- **Using URIs as Hash Keys**

```js
upstream myservers {
        #random;
        hash $request_uri consistent;
        server 127.0.0.1:2321 weight=1;
        server 127.0.0.1:2322 weight=1;
        server 127.0.0.1:2323 weight=1;
        server 127.0.0.1:2324 weight=1;
}
```

- **Request to web server**

Make requests to the web server running on `localhost` on port `2025`, and specifically requesting the resource at `/path`. 

```
curl localhost:2025/path1
curl localhost:2025/path2
curl localhost:2025/path3
curl localhost:2025/path4
```

Take `curl localhost:2025/path1`  for example. Nginx will **calculate the hash for `/path1`** and route the request to one of the backend servers. Based on the consistent hashing, **`/path1` will always be directed to the same server** as long as the upstream server configuration doesn't change.



- **Execution Result**

Based on the hash of the request URI: **`/path1` goes to Server1, `/path2` goes to Server2, and both `/path3` and `/path4` are routed to Server4.**

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-11 下午2.26.55.png" alt="截屏2025-02-11 下午2.26.55" style="zoom:50%;" /> 



Execute the same requests again, **the result doesn't change.**

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 下午2.39.14.png" alt="截屏2025-02-11 下午2.39.14" style="zoom:50%;" />  





