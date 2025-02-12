# Nginx



### (1) Install Nginx (take MacOS as an example):

#### 1.**Install Homebrew** (if not already installed)

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```



#### 2.Install Nginx

```shell
brew install nginx
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.09.39.png" alt="截屏2025-02-10 下午9.09.39" style="zoom: 33%;" /> 



#### 3.View Nginx status and configuration details

```shell
brew info nginx
```

<img src="/Users/alexanderlee/Desktop/截屏2025-02-10 下午9.29.14.png" alt="截屏2025-02-10 下午9.29.14" style="zoom: 42% ;" />  



#### 4.Start Nginx

```
brew services start nginx
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.18.59.png" alt="截屏2025-02-10 下午9.18.59" style="zoom:42%;" /> 



The default port number of Nginx is `80` and the address is `localhost `(127.0.0.1), So open http://localhost:8080 , you will see below.

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.20.20.png" alt="截屏2025-02-10 下午9.20.20" style="zoom: 33%;" /> 



#### 5.Stop Nginx

```
brew services stop nginx
```

  <img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午11.34.46.png" alt="截屏2025-02-10 下午11.34.46" style="zoom: 33%;" />







### (2) Install Nodejs

> Node.js is a JavaScript runtime based on the Chrome V8 engine. We start the server js file written through Nodejs. The Node.js `http` module allows creating basic HTTP services using `require`.
>
> - `createServer`: creates an HTTP server with a callback function that handles 
> - `request` : contains client request details (URL, headers, method, body).
> - `response` is used to send data back to the client with methods like `writeHead` for setting headers and status codes.



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

create a folder named nginx and write four server webserver.js files,==occupying ports 2321,2322,2323,2324==, using server.listen() to listen to the function. When the response request is returned, the string "Hello world" is written into http as a request and displayed on the web page of the browser.

`webserver1.js`

```js
// Import the http module from Node.js to create a server
const http = require('http');

// Define the hostname and port number
const hostname = '127.0.0.1';
const port = 2321;

// Create an HTTP server
const server = http.createServer((req, res) => {
  res.statusCode = 200;
 
  res.setHeader('Content-Type', 'text/plain');
  
  res.end('Hello World from Server One\n');
});

// Start the server and listen on the specified hostname and port
server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```

![截屏2025-02-10 下午9.56.22](/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.56.22.png)

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.56.53.png" alt="截屏2025-02-10 下午9.56.53" style="zoom: 40%;" /> 



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

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.59.12.png" alt="截屏2025-02-10 下午9.59.12" style="zoom:42%;" /> 



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

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午9.58.37.png" alt="截屏2025-02-10 下午9.58.37" style="zoom:42%;" /> 



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

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午10.00.11.png" alt="截屏2025-02-10 下午10.00.11" style="zoom:42%;" /> 



#### 4.Use Shell Script to Start Server (quick way)

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

```js
chmod +x start-web-servers.sh &
chmod +x stop-web-servers.sh
```

- To start all services, run:

```js
./start-web-servers.sh
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午11.10.58.png" alt="截屏2025-02-10 下午11.10.58" style="zoom:42%;" /> 

- To shutdown all services, run:


```js
./stop-web-servers.sh
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午11.11.24.png" alt="截屏2025-02-10 下午11.11.24" style="zoom:42%;" /> 







### (3) Modify the Nginx configuration file

#### 1. Open `nginx.conf`

Open configuration file `nginx.conf`and Change the original port number 8080 to an unused one.

- `nginx.conf`

```js
vim /usr/local/etc/nginx/nginx.conf
```

- You can also use the find command to locate it

```js
find / -name nginx.conf
```

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-10 下午10.04.14.png" alt="截屏2025-02-10 下午10.04.14" style="zoom:42%;" /> 



#### 2. Change port number

```shell
server {
        #listen       8080;
        listen       2025;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
.....
}
```

**Note: Please check if the port is already in use.** 

```
lsof -i :<portnumber> // If the port is in use, it will display the process information.
kill -9 <PID> // kill the process
```



#### 3.  Configure the server cluster in `nginx.conf` and set to reverse proxy pass

`proxy_pass` specifies that the request should be forwarded to the server group defined by myservers (http://myservers).

`upstream myservers`defines a set of back-end servers for load balancing in Nginx. Each server instruction specifies a local server running on a different port (127.0.0.1: 2321-2324). By default, Nginx uses a round-robin strategy(chapter 4) to distribute requests evenly across these servers.

<img src="/Users/alexanderlee/Desktop/截屏2025-02-10 下午10.25.40.png" alt="截屏2025-02-10 下午10.25.40" style="zoom:42%;" /> 

 

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



#### 4. Restart Nginx 

**Note: When modifying the `nginx.conf`, please execute**

```
nginx -s reload
```





### (4) Basic load balancing with Nginx

>Nginx is a high-performance server that supports load balancing. It improves system performance and reliability by distributing requests to multiple backend servers. Nginx supports strategies such as round-robin, weighted round-robin, and IP hash for efficient traffic distribution.

Initally, We can send an http request to the server at the command line with the `curl localhost:2025` command, and the Nginx proxy server forwards the request to one of the servers in the server cluster and gets the response back. 

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 上午11.34.23.png" alt="截屏2025-02-11 上午11.34.23" style="zoom:42%;" /> 

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



- **Send requests to the server**

Execute the following request eight times.

```
curl localhost:2025  // 8 times
```



- **Execution Result**

All servers share equal weight and connections.

| Server | Weight（Standard） | Connections |
| ------ | ------------------ | ----------- |
| 2321   | 1                  | 2           |
| 2322   | 1                  | 2           |
| 2323   | 1                  | 2           |
| 2324   | 1                  | 2           |

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 上午10.53.28.png" alt="截屏2025-02-11 上午10.53.28" style="zoom:42%;" /> 





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



- **Send requests to the server**

Execute the following request eight times.

```
curl localhost:2025  // 8 times
```



- **Execution Result**

High-weight servers are allocated more requests than low-weight servers, and the allocation process follows a certain weight order.

| Server | Weight | Connections |
| ------ | ------ | ----------- |
| 2321   | 4      | 4           |
| 2322   | 2      | 2           |
| 2323   | 1      | 1           |
| 2324   | 1      | 1           |

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-11 上午11.09.41.png" alt="截屏2025-02-11 上午11.09.41" style="zoom:42%;" /> 





#### 3.IP Hash

> The server to which a request is sent is determined from the client IP address. In this case, either the ==first three octets of the IPv4 address or the whole IPv6 address== are used to calculate the hash value. The method guarantees that requests from the same address get to the same server unless it is not available.

`nginx.conf`

```js
upstream myservers {
        #random;
        ip_hash;
        server 127.0.0.1:2321;
        server 127.0.0.1:2322;
        server 127.0.0.1:2323;
        server 127.0.0.1:2324;
}
```

- **Create and Bind virtual IP address**

```js
ifconfig lo0 alias 192.168.1.101 up // Bind 192.168.1.101 as a virtual address to lo0
ifconfig lo0 alias 192.168.1.102 up
ifconfig lo0 alias 192.168.1.103 up
ifconfig lo0 alias 192.168.1.104 up
ifconfig lo0 alias 192.168.255.101 up
```

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 下午4.19.31.png" alt="截屏2025-02-11 下午4.19.31" style="zoom:42%;" /> 



- **Send requests with IP addresses**

Execute commands below to initiate requests to 127.0.0.1:2025 through 192.168.x.x as the source IP.

``` js
curl localhost:2025 --interface 192.168.1.101
curl localhost:2025 --interface 192.168.1.102
curl localhost:2025 --interface 192.168.1.103
curl localhost:2025 --interface 192.168.1.104
curl localhost:2025 --interface 192.168.255.101
```



- **Execution Result**

192.168.1.101...192.168.1.104 have the ==same three octets==, so their hash values are the same and point to the same server. But 192.168.255.101 has different octets, resulting in a different hash value compared to the four, so it is assigned to a different server(though it might collide due to hash conflicts).

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 下午4.21.04.png" alt="截屏2025-02-11 下午4.21.04" style="zoom:42%;" /> 





#### 4. Least Connections

> A request is sent to the server with the least number of active connections, again with server weights taken into consideration

**Simple Algorithm Pseudocode:**

```js
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



- **Send requests to the server**

Execute the following request twelve times.

```js
curl localhost:2025  // 12 times
```



- **Count the number of server connections and Weighted connections (Weighted Connections)**

| Server | Weight | Connections | Connections / Weight |
| ------ | ------ | ----------- | -------------------- |
| 2321   | 4      | 6           | 1.5                  |
| 2322   | 2      | 3           | 1.5                  |
| 2323   | 1      | 2           | 2                    |
| 2324   | 1      | 1           | 1. (the smallest)    |

- **Execution Result**

**the new request is assigned to Server4 since it has the smallest weighted connection count.**

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 下午12.56.39.png" alt="截屏2025-02-11 下午12.56.39" style="zoom:42%;" />    





#### 5. Consistent Hash

> Requests are evenly distributed across all upstream servers based on the user‑defined hashed key value. If an upstream server is added to or removed from an upstream group, only a few keys are remapped which minimizes cache misses in the case of load‑balancing cache servers or other applications that accumulate state.

**Simple Algorithm Pseudocode:**

```js
1.All servers (Server1... Server4) are mapped to a virtual ring (integer space from 0 to 2³²) using a hash function based on their identifier (e.g., IP address, server name).

2.The request key (URI) is hashed to determine its position on the ring.

3.Start from the request’s hash position and move clockwise on the ring to find the first server. The request is assigned to that server.
If the end of the ring is reached, continue from the beginning.
Add or Remove Servers

4.Removing a Server: Only the keys on that server are reassigned to the next server in the clockwise direction, while other servers remain unaffected.
```



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

- **Send requests to the server**

Make requests to the web server running on `localhost` on port `2025`, and specifically requesting the resource at `/path`. 

```js
curl localhost:2025/path1
curl localhost:2025/path2
curl localhost:2025/path3
curl localhost:2025/path4
```

Take `curl localhost:2025/path1`  for example. Nginx will **calculate the hash for `/path1`** and route the request to one of the backend servers. Based on the consistent hashing, **`/path1` will always be directed to the same server** as long as the upstream server configuration doesn't change.



- **Execution Result**

1)Based on the hash of therequestURI: **`/path1` goes to Server1, `/path2` goes to Server2, and both `/path3` and `/path4` are routed to Server4.**

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-11 下午2.26.55.png" alt="截屏2025-02-11 下午2.26.55" style="zoom:42%;" /> 



2)Execute the same requests again, the result doesn't change.

<img src="/Users/alexanderlee/Desktop/截屏2025-02-11 下午2.39.14.png" alt="截屏2025-02-11 下午2.39.14" style="zoom:42%;" />  



3)Delete server4, Execute the same requests again.

`path1` and `path2` remain unchanged, while `path3` and `path4` are assigned to different servers.

<img src="/Users/alexanderlee/Library/Application Support/typora-user-images/截屏2025-02-11 下午3.11.08.png" alt="截屏2025-02-11 下午3.11.08" style="zoom: 42%;" /> 





