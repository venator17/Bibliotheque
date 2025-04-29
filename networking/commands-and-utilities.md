---
icon: screwdriver-wrench
---

# Commands and Utilities

## <mark style="color:yellow;">NETCAT</mark>

<mark style="color:purple;">**Universal utility for network connection in Unix and similar operating systems**</mark>

| Command                                                                                 | Explanation                                                                                            |
| --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| <mark style="color:green;">`nc host port`</mark>                                        | Connects to the host on the specified port                                                             |
| <mark style="color:green;">`nc -l -p port`</mark>                                       | Starts nc in listener mode on the specified port                                                       |
| <mark style="color:green;">`nc -z host {port-range}`</mark>                             | Basic port scanner                                                                                     |
| <mark style="color:green;">`nc -v host port`</mark>                                     | Get banner                                                                                             |
| <mark style="color:green;">`nc -l -p local_port -c 'nc remote_host remote_port'`</mark> | Configures a basic proxy where it listens for a specific local port and forwards it to a remote server |
| <mark style="color:green;">`nc -l -p 1234 -e /bin/bash`</mark>                          | Simple backdoor                                                                                        |

***

## <mark style="color:yellow;">IP</mark>

<mark style="color:purple;">**Linux command to manage ІР.**</mark> Older brother of ifconfig

| Command                                        | Explanation         |
| ---------------------------------------------- | ------------------- |
| <mark style="color:green;">`ip addr`</mark>    | Shows all addresses |
| <mark style="color:green;">`ip -4 addr`</mark> | Shows IPv4 address  |
| <mark style="color:green;">`ip -6 addr`</mark> | Shows IPv6 address  |

## <mark style="color:yellow;">NETSTAT</mark>

<mark style="color:red;">**netstat**</mark> command lets you <mark style="color:purple;">**discover which sockets are connected**</mark> and which sockets are listening. Meaning, it tells you which ports are in use and which processes are using them. It can show you routing tables and statistics about your network interfaces and multicast connections.This command is liable to produce a long listing, so we pipe it into less.

| Syntax                                                              | Explanation                                                                                                                     |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| <mark style="color:green;">`netstat -at \| less`</mark>             | Looks for all tcp sockets                                                                                                       |
| <mark style="color:green;">`netstat -au \| less`</mark>             | Looks for all udp sockets                                                                                                       |
| <mark style="color:green;">`netstat -l \| less`</mark>              | Looks for all listening sockets. We could combine with -t to make netstat -lt or -lu to search for listening tcp or udp sockets |
| <mark style="color:green;">`netstat -p -at`</mark>                  | Shows all TCP sockets with PID                                                                                                  |
| <mark style="color:green;">`sudo netstat -anp \| grep ":22"`</mark> | Finds 22 port target string                                                                                                     |
| <mark style="color:green;">`sudo netstat -i`</mark>                 | Show network interfaces                                                                                                         |
| <mark style="color:green;">`sudo netstat -r`</mark>                 | Display kernel routing table                                                                                                    |

***

## <mark style="color:yellow;">TRACEROUTE</mark>

For understanding traceroute you should know what is TCP/IP suite of protocols, especially what is UDP or User Datagram Protocol. There are a lot of headers but we need TTL (Time to Live). It is a count how much routers, gateways could possibly pass this packet, each router decrements 1. When TTL reaches 0, router sends ICMP "Time Exceeded" message back to the origin of the packet. So traceroute first sends packet with ttl 1, then 2, then 3 etc. until destination is reached or maximum number of hops (30 by default) is tested.

| Syntax                                               | Explanation                                   |
| ---------------------------------------------------- | --------------------------------------------- |
| <mark style="color:green;">`traceroute -l IP`</mark> | Use ICMP Echo requests instead of UDP packets |
| <mark style="color:green;">`traceroute -n IP`</mark> | Do not resolve hostnames                      |
| <mark style="color:green;">`traceroute -q IP`</mark> | Set the number of queries per hop             |
| <mark style="color:green;">`traceroute -m IP`</mark> | Set the maximum hop count                     |

***
