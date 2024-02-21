**Load balancing**: 
  - To distribute incoming network traffic across multiple servers or resources to ensure optimal utilization, maximize throughput, minimize response time, and avoid overloading any single server.

List of common algorithms:
  - Round Robin: 
    - Decs: Requests are distributed across servers in a circular order. Each server is selected in turn, and when the end of the list is reached, the selection starts over from the beginning.
    - Example:
      - Imagine we have three servers: Server A, Server B, and Server C. Requests are distributed in a circular order:
        - Request 1 goes to Server A
        - Request 2 goes to Server B
        - Request 3 goes to Server C
        - Request 4 goes back to Server A
        - And so on, continuing in this circular fashion.
    - Coding:
      ```python
        class RoundRobinBalancer:
          def __init__(self, servers):
              self.servers = servers
              self.current_index = 0

          def get_next_server(self):
              next_server = self.servers[self.current_index]
              self.current_index = (self.current_index + 1) % len(self.servers)
              return next_server

        # Example usage
        servers = ['ServerA', 'ServerB', 'ServerC']
        rr_balancer = RoundRobinBalancer(servers)
        for _ in range(10):
            print(rr_balancer.get_next_server())
      ```

  - Least Connection: 
    - Desc: New requests are sent to the server with the fewest active connections. This algorithm aims to distribute the load evenly among servers based on their current connection count.
    - Example:
      - Suppose we have three servers: Server X, Server Y, and Server Z. Let's say at a certain moment:
        - Server X has 10 active connections
        - Server Y has 8 active connections
        - Server Z has 12 active connections
        - When a new request comes in, it will be routed to Server Y because it currently has the fewest active connections.
    - Coding:
      ```python
        class LeastConnectionBalancer:
          def __init__(self, servers):
              self.servers = servers

          def get_next_server(self):
              return min(self.servers, key=lambda server: server['connections'])

        # Example usage
        servers = [{'name': 'ServerX', 'connections': 10},
                  {'name': 'ServerY', 'connections': 8},
                  {'name': 'ServerZ', 'connections': 12}]
        lc_balancer = LeastConnectionBalancer(servers)
        print(lc_balancer.get_next_server()['name'])
      ```

  - Least Response Time: 
    - Desc: New requests are sent to the server with the lowest average response time or latency. This algorithm aims to minimize response times for clients by directing requests to the server that can respond the fastest.
    - Example:
      - Consider three servers: Server P, Server Q, and Server R. Based on historical response times:
        - Server P has an average response time of 50 ms
        - Server Q has an average response time of 40 ms
        - Server R has an average response time of 60 ms
        - A new request would be directed to Server Q because it has the lowest average response time.
    - Coding:
      ```python
        class LeastConnectionBalancer:
          def __init__(self, servers):
              self.servers = servers

          def get_next_server(self):
              return min(self.servers, key=lambda server: server['connections'])

        # Example usage
        servers = [{'name': 'ServerX', 'connections': 10},
                  {'name': 'ServerY', 'connections': 8},
                  {'name': 'ServerZ', 'connections': 12}]
        lc_balancer = LeastConnectionBalancer(servers)
        print(lc_balancer.get_next_server()['name'])
      ```

  - IP Hash: 
    - Desc: The IP address of the client is used to determine which server receives the request. This ensures that requests from the same client are always directed to the same server, which can be useful for maintaining session state or caching.
    - Example:
      - If a client with IP address 192.168.1.100 sends a request, based on its IP address hash, it always gets directed to Server A. Similarly, if another client with IP address 192.168.1.200 sends a request, it will always be directed to Server B.

  - Weighted Round Robin: 
    - Decs: Similar to Round Robin, but each server is assigned a weight indicating its processing capacity. Servers with higher weights receive a larger proportion of requests.
    - Example:
      - Let's say we have three servers with different capacities:
        - Server A with a weight of 1
        - Server B with a weight of 2
        - Server C with a weight of 1
        - Requests would be distributed accordingly, with Server B receiving twice as many requests as Server A or Server C.

  - Weighted Least Connection: 
    - Decs: Similar to Least Connection, but each server is assigned a weight indicating its processing capacity. Servers with higher weights can handle more connections before new connections are directed to other servers.
    - Example:
      - Similar to Least Connection, but taking into account server capacity weights. Servers with higher weights can handle more connections before new connections are directed elsewhere.

  - Random: 
    - Decs: Requests are distributed randomly among the available servers. While simple, this approach may not always result in evenly balanced loads.

  - Source IP Affinity: 
    - Decs: Similar to IP Hash, but instead of hashing the client's IP address, the server maintains a mapping of client IP addresses to specific servers. Requests from the same client are consistently routed to the same server.
    - Example:
      - Requests from IP address 192.168.1.100 are always directed to Server A, while requests from IP address 192.168.1.200 are always directed to Server B.