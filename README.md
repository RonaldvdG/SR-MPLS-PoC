# Segment Routing over MPLS

! Important notice! The files on this GitHub were used on JunOS vMX 18.2R1.9 devices.

This Git Repository consists of a Proof of Concept for Segment Routing over MPLS. With this Proof of Concept, two types scenario's are verified. The first scenario being with a Segment Routing Unaware Function and the second scenario with a Segment Routing Aware Function.

### Proof of Concept setup
This environment consisted of the following devices:
  - 3 routers
    - 2 routers as Segment Routing Domain edge routers
    - 1 router as Segment Routing Domain interior router
  - 1 proxy
    - In the first scenario (SR-Unaware) everything will be forwarded towards the Firewall attached to this proxy
    - In the second scenario, this proxy functions as the SR-Aware function

The setup is as follows:
For the scenario with a SR-Unaware function:
```
+------------+  +------------+
|            |  |            |
|Internet VM |  |Institute VM|
| 10.0.10.10 |  | 10.0.20.10 |
|            |  |            |
| +--------+ |  | +--------+ |
+-+Router 1+-+  +-+Router 2+-+
  |10.0.0.1|      |10.0.0.2|
+-+        +------+        +-+
| +--+-----+      +-----+--+ |
|    |    |        |    |    |
|    |    |        |    |    |
|    |    +--------+    |    |
|    |                  |    |
|    |    +--------+    |    |
|    |    |Router 3|    |    |
|    +----+10.0.0.3+----+    |
|         |        |         |
|         +---+-----         |
|             |              |
|  SR Domain  |              |
|         +---+----+         |
+---------+ Proxy  +---------+
          |10.0.0.4|
+---------+        +---------+
|         +---+----+         |
|             |              |
|       +-----+------+       |
|       |  Firewall  |       |
|       | 10.0.40.11 |       |
|       |            |       |
|       +------------+       |
| SR Unaware domain          |
+----------------------------+
```
For the scenario with an SR-Aware function:
```
+------------+  +------------+
|            |  |            |
|Internet VM |  |Institute VM|
| 10.0.10.10 |  | 10.0.20.10 |
|            |  |            |
| +--------+ |  | +--------+ |
+-+Router 1+-+  +-+Router 2+-+
  |10.0.0.1|      |10.0.0.2|
+-+        +------+        +-+
| +--+-----+      +-----+--+ |
|    |    |        |    |    |
|    |    |        |    |    | 
|    |    +--------+    |    |
|    |                  |    |
|    |    +--------+    |    |
|    |    |Router 3|    |    |
|    +----+10.0.0.3+----+    |
|         |        |         |
|         +---+-----         |
|             |              |
|             |              |
|         +---+----+         |
|         | Proxy  |         |
|         |10.0.0.4|         |
|         |        |         |
|         +--------+         |
| SR Domain                  |
+----------------------------+
```

## Configurations
This GitHub provides the configurations for the Routers, the Proxy, the internet and the used iptables rule for the firewall.

The configurations for the Routers and the Proxy were succesfully tested on JunOS vMX 18.2R1.9 devices, we do not claim that this same configuration will work for other devices. 

### Internet
For simulating the internet, we used an Ubuntu 18.04 Virtual Machine where we made use of two Docker containers (For both [port 8080](https://hub.docker.com/r/mslotboom/app8080) and [port 8181](https://hub.docker.com/r/mslotboom/app8181)). 

### Institute
As Institute we also made use of an Ubuntu 18.04 Virtual Machine. The Institute did nothing else but retrieving the webpages served by the simulated Internet.

### Firewall
Also the Firewall was an Ubuntu 18.04 machine. This Firewall enabled IPv4 Forwarding and blocked the traffic with destination port 8181.

# Licence
These files are free to use! :)
