# Proxies

## ABOUT

<mark style="color:red;">**Proxy**</mark> is a <mark style="color:purple;">**device**</mark> or <mark style="color:purple;">**service**</mark> that acts as an intermediary between a client (such as a user or device) and a destination server. It sits between two endpoints and handles requests on behalf of the client. In essence, it "mediates" the traffic between the two systems. While the term is often misunderstood, proxies can operate in various contexts, including security, web development, and privacy.

### Key Concepts of Proxy:

1. <mark style="color:yellow;">**Mediator:**</mark>\
   The critical feature of a proxy is its role as a mediator. The proxy intercepts and forwards requests, allowing it to inspect, modify, or control the traffic. This is distinct from a gateway, which simply passes traffic without manipulation.
2. <mark style="color:yellow;">**OSI Layer:**</mark>\
   Proxies typically operate at **Layer 7 (Application Layer)** of the OSI model, meaning they can inspect and modify the actual content of the communication, such as HTTP requests and responses.

## Types of Proxies:

### **Forward Proxy**:

<mark style="color:red;">**Forward Proxy**</mark>**&#x20;**<mark style="color:purple;">**filters outgoing traffic from a client to a server**</mark>. The client sends requests to the proxy, which then forwards them to the target server.

* <mark style="color:yellow;">**Example**</mark><mark style="color:yellow;">:</mark> Tools like **Burp Suite** are used as HTTP forward proxies for penetration testing.

### **Reverse Proxy**:

<mark style="color:red;">**Reverse proxy**</mark> <mark style="color:purple;">**filters incoming traffic to a server,**</mark> often acting as an intermediary between the external network and internal services. The client sends requests to the reverse proxy, which then forwards them to the target server on behalf of the client.

* <mark style="color:yellow;">**Example**</mark><mark style="color:yellow;">:</mark> **Cloudflare** serves as a reverse proxy to protect websites from DDoS attacks, while **ModSecurity** is a Web Application Firewall (WAF) that inspects and blocks malicious requests. Also attackers may use reverse proxies to evade detection, forwarding malicious traffic through infected systems.

## Transparency Types in Proxies

### <mark style="color:red;">**Transparent Proxy**</mark><mark style="color:red;">:</mark>

* The client is unaware of the proxy's existence. The proxy intercepts and processes requests transparently. It's typically used for content filtering, caching, or monitoring.
* <mark style="color:yellow;">**Example**</mark><mark style="color:yellow;">:</mark> A network administrator may deploy a transparent proxy to monitor or filter web traffic without requiring configuration on client devices.

### <mark style="color:red;">**Non-Transparent Proxy**</mark><mark style="color:red;">:</mark>

* The client is aware of the proxy and must configure their system to use it. If not configured, the client cannot communicate via the proxy.
* <mark style="color:yellow;">**Example**</mark><mark style="color:yellow;">:</mark> In corporate environments, employees' web browsers are configured to route traffic through a non-transparent proxy.
