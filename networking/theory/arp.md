# ARP

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**ARP or Address Resolution Protocol**</mark> which is <mark style="color:purple;">**one of the most important protocols**</mark> of the Data link layer in the OSI model. <mark style="color:yellow;">**It is responsible to find the hardware address of a host from a known IP address**</mark>. So as I get we use ARP when we need to send some info on 2 level of OSI, which requires MAC address. Every machine has it's own ARP cache, where is table like IP-MAC data. So when we need to send some data on Data Link level, we broadcast request to entire network like:

_<mark style="color:orange;">**"Hey, who is 10.10.10.10, I want to find his MAC". And if we found it address, it will tell us back with "Hi, you looking for 10.10.10.10? It's me, here's my MAC"**</mark>_<mark style="color:orange;">**.**</mark>

## <mark style="color:yellow;">ARP Spoofing & ARP DOS</mark>

### <mark style="color:blue;">Bettercap</mark>

<mark style="color:red;">**Bettercap**</mark> is a powerful, modular, and <mark style="color:purple;">**flexible open-source tool**</mark> designed for network penetration testing. It is primarily used for network discovery, man-in-the-middle attacks, and other security assessments. Bettercap is written in Go and comes with a variety of features that make it a valuable tool for security professionals and ethical hackers. Here are some key aspects that make Bettercap useful:

***

**Example**

_Ban the address 192.168.1.6 from the network:_

```bash
> set arp.spoof.targets 192.168.1.6; arp.ban on
```

_Spoof 192.168.1.2, 192.168.1.3 and 192.168.1.4:_

```bash
> set arp.spoof.targets 192.168.1.2-4; arp.spoof on
```

**After spoofing or poisoning we could look or change traffic with wireshark**
