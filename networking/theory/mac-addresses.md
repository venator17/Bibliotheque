# MAC Addresses

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**Media Access Control (MAC)**</mark> address is the physical address for our network interfaces. Each host in a network has its own 48-bit (6 octets), represented in hexadecimal format. There are several different standards for the MAC address:

* <mark style="color:$primary;">**Ethernet (IEEE 802.3)**</mark>
* <mark style="color:$primary;">**Bluetooth (IEEE 802.15)**</mark>
* <mark style="color:$primary;">**WLAN (IEEE 802.11)**</mark>

This is because the MAC address addresses the physical connection (network card, Bluetooth, or WLAN adapter) of a host. Each network card has its individual MAC address, which is configured once on the manufacturer's hardware side but can always be changed, at least temporarily.

The MAC address consists of a total of <mark style="color:yellow;">**6 bytes**</mark>. The <mark style="color:yellow;">**first half (3 bytes / 24 bit)**</mark> is the so-called <mark style="color:red;">**Organization Unique Identifier (OUI)**</mark> defined by the <mark style="color:red;">**Institute of Electrical and Electronics Engineers (IEEE)**</mark> for the respective manufacturers. The last half of the MAC address is called the <mark style="color:red;">**Individual Address Part or Network Interface Controller (NIC)**</mark>, which the manufacturers assign. The manufacturer sets this bit sequence only once and thus ensures that the complete address is unique.

Furthermore, the last two bits in the first octet can play another essential role. The last bit can have two states, <mark style="color:yellow;">**0**</mark> and <mark style="color:yellow;">**1**</mark>, as we already know. The last bit identifies the MAC address as <mark style="color:yellow;">**Unicast (0)**</mark> or <mark style="color:yellow;">**Multicast (1)**</mark>. With unicast, it means that the packet <mark style="color:purple;">**sent will reach only one**</mark> specific host. With multicast, the packet is sent <mark style="color:purple;">**only once to all hosts**</mark> on the local network, which then decides whether or not to accept the packet based on their configuration. The multicast address is a unique address, just like the **broadcast** address, which has fixed octet values.
