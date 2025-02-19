# Port-Forwarding

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**Port forwarding**</mark> is a technique that allows us to <mark style="color:purple;">**redirect a communication request from one port to another**</mark>. Port forwarding uses **TCP** as the primary communication layer to provide interactive communication for the forwarded port. Basically if shortly:

* <mark style="color:yellow;">**Local Port-Forwarding**</mark> is like regular shell. Forwards our traffic through port to victim host port
* <mark style="color:yellow;">**Remote Port-Forwarding**</mark> is like reverse shell. To bypass firewall we make victim host to forward traffic to our host
* <mark style="color:yellow;">**Dynamic Port-Forwarding**</mark> is just a proxy, working with inbound and outbound traffic

## <mark style="color:yellow;">**LOCAL PORT FORWARDING**</mark>

Local port forwarding allows you to forward traffic from your local machine to a remote server. This is commonly used to access services behind a firewall or to create a secure channel for data transmission.

### <mark style="color:blue;">**How it works**</mark>&#x20;

You specify a local port (e.g., 1234) and bind it to a remote service through an intermediary (like an SSH server). Traffic sent to the local port is encrypted and forwarded to the destination.

### <mark style="color:blue;">**Use case**</mark>

Accessing an intranet site or database from your local machine using SSH.

### <mark style="color:blue;">**Example**</mark>

```bash
ssh -L <local-port>:<remote-ip>:<remote-port> user@<remote-ip>
```

## <mark style="color:yellow;">**REMOTE PORT FORWARDING**</mark>

Remote port forwarding is the reverse of local port forwarding. It allows a remote machine to forward its traffic to a service on your local machine.

### <mark style="color:blue;">**How it works**</mark>

You expose a local service (e.g., a web server running on your local machine) to a remote server. The remote server listens on a specified port and forwards traffic to your local machine.

### <mark style="color:blue;">**Use case**</mark>

Making a local service accessible to others through a remote server (e.g., for debugging or sharing an application).

### <mark style="color:blue;">**Example**</mark>

```bash
ssh -R <remote-port>:localhost:<local-port> user@<remote-ip>
```

Here, anyone accessing `<remote-ip>:<remote-port>` will be redirected to your local machine's `localhost:<local-port>`.

## <mark style="color:yellow;">**DYNAMIC PORT FORWARDING**</mark>

Dynamic port forwarding creates a SOCKS proxy, allowing traffic to be forwarded dynamically to various destinations based on requests. This is useful for tunneling multiple connections.

### <mark style="color:blue;">**How it works**</mark>

Your local machine acts as a SOCKS proxy server, and applications can configure this proxy to route traffic through it. The traffic is dynamically forwarded to different destinations through the SSH server.

### <mark style="color:blue;">**Use case**</mark>

Bypassing firewalls, anonymizing traffic, or routing web browsing through an SSH tunnel.

### <mark style="color:blue;">**Example**</mark>

```bash
ssh -D <local-port> user@<remote-ip>
```

This creates a SOCKS proxy on `localhost:<local-port>`. Applications configured to use this proxy will route traffic through the SSH server dynamically.
