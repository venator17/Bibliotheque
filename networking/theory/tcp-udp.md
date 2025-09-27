# TCP / UDP

## <mark style="color:yellow;">TCP</mark>

<mark style="color:red;">**TCP (Transmission Control Protocol)**</mark> is a <mark style="color:purple;">**connection-oriented transport layer protocol**</mark> that ensures reliable data transmission. It establishes a connection using a <mark style="color:red;">**three-way handshake (SYN, SYN-ACK, ACK)**</mark> and guarantees that data is delivered in order, <mark style="color:orange;">**without duplication or loss**</mark>. TCP uses acknowledgments, sequence numbers, flow control, and congestion control mechanisms to manage data flow. It's used in applications where reliability matters, such as HTTP, HTTPS, SSH, and FTP.

## <mark style="color:yellow;">UDP</mark>

<mark style="color:red;">**UDP (User Datagram Protocol)**</mark> is a <mark style="color:purple;">**connectionless transport layer protocol**</mark> that sends <mark style="color:red;">**datagrams**</mark> without establishing a connection. It provides low-latency, <mark style="color:orange;">**best-effort delivery with no guarantee of order or reliability**</mark>. UDP does not perform retransmissions or acknowledgments, making it faster and more lightweight than TCP. It's used in applications where speed is more important than reliability, such as DNS, VoIP, online gaming, and video streaming.
