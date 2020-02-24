# Load Balancing with Nginx

### Overview

- Load balancing - commonly used technique for optimising resource utilisation, maximizing throughput, reducing latency, and ensuring fault‑tolerant configurations

### Proxying HTTP Traffic to a Group of Servers

- To start using NGINX to load balance HTTP traffic you need to define the group with `upstream` directive

- The directive is placed in the `http` context

- Servers in the group are configured using the `server` directive

- The following example defines a group named `backend` and consists of three server configurations

  ```jinja2
  http {
  	upstream backend{
  		server backend1.example.com weight=5;
  		server backend2.example.com;
  		server 192.0.0.1 backup;
  	}
  }
  ```

- To pass requests to a server group, the name of the group is specified in the `proxy_pass` directive.

- The following example shows a virtual server running on NGINX passes all request to the `backend` upstream group defined above

  ```jinja2
  server {
  	location / {
  		proxy_pass http://backend;
  	}
  }
  ```

- Combining the two pieces of code above shows how to proxy HTTP requests to the `backend` server group.

  ```jinja2
  http {
      upstream backend {
          server backend1.example.com;
          server backend2.example.com;
          server 192.0.0.1 backup;
      }
      
      server {
          location / {
              proxy_pass http://backend;
          }
      }
  }
  ```

- As no load balancing algorithm is specified in the `upstream` block, NGINX uses the default, **Round Robin**.

### Choosing a Load-Balancing Method

- **Round Robin** - Requests are distributed evenly across the servers, with server weights taken into consideration. (default)

- **Least Connections** - A request is sent to the server with the least number of active connections. Server weights are taken into consideration. An example

  ```jinja2
  upstream backend {
      least_conn;
      server backend1.example.com;
      server backend2.example.com;
  }
  ```

- **IP Hash** - The server to which a request is sent is determined from the client IP address In this case, either the first three octets of the IPv4 address or the whole IPv6 address are used to calculate the hash value. The method guarantees that requests from the same address get to the same server unless it is not available.

  ```jinja2
  upstream backend {
      ip_hash;
      server backend1.example.com;
      server backend2.example.com;
  }
  ```

  To temporarily remove a server from the load-balancing rotation, mark it with `down` as such

  ```jinja2
  upstream backend {
      server backend1.example.com;
      server backend2.example.com;
      server backend3.example.com down;
  }
  ```

  This preserves the current hashing of the client IP and requests that were to be processed by the server are sent to the next in the group.

- **Generic Hash** - A user defined key determines which server the request is sent to. This could be a string, variable, or a combination. For example the key may be a paired source IP address and port, or a URI as shown below:

  ```jinja2
  upstream backend {
      hash $request_uri consistent;
      server backend1.example.com;
      server backend2.example.com;
  }
  ```

  `consistent` is optional

- **Least Time** - (NGINX Plus only) For each request, the server with the lowest average latency and lowest number of active connections is selected.

  ```jinja2
  upstream backend {
      least_time header;
      server backend1.example.com;
      server backend2.example.com;
  }
  ```

- **Random** - Each request is passed to a randomly selected server

### Server Weights

- The `weight` parameter to the `server` directive sets the weight of a server. The default is `1`. For example:

  ```jinja2
  upstream backend {
      server backend1.example.com weight=5;
      server backend2.example.com;
      server 192.0.0.1 backup;
  }
  ```

- In the above example `backend1.example.com` has weight `5` whereas the other two have weight `1`. 
- Server `192.0.0.1` is still the backup if the other two are not available
- With this config, out of every `6` requests, `5` are sent to `backend1.example.com` and `1` to `backend2.example.com`.

