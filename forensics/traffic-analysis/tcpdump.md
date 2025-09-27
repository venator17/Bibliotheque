# TCPdump

## <mark style="color:yellow;">CHEATSHEET</mark>

<pre class="language-bash"><code class="lang-bash"># Basic info
tcpdump --version               # Show tcpdump &#x26; libpcap version
tcpdump -h                      # Show help/usage
tcpdump -D                      # List available interfaces

# Capturing
<strong>tcpdump -i eth0                 # Capture on interface eth0
</strong>tcpdump -i eth0 -c 20           # Capture 20 packets then stop
tcpdump -i eth0 -w capture.pcap # Write capture to file
tcpdump -r capture.pcap         # Read from saved file

# Display / output
tcpdump -n                      # Don’t resolve hostnames
tcpdump -nn                     # Don’t resolve hostnames or ports
tcpdump -X                      # Show packet contents (hex + ASCII)
tcpdump -XX                     # Show hex + ASCII and Ethernet headers
tcpdump -v                      # Verbose output
tcpdump -vv                     # More verbose
tcpdump -vvv                    # Most verbose
tcpdump -q                      # Print less protocol info

# Basic filters
tcpdump -i eth0 host 192.168.1.10        # Traffic to/from host
tcpdump -i eth0 src 192.168.1.10         # Only source traffic
tcpdump -i eth0 dst 192.168.1.10         # Only destination traffic
tcpdump -i eth0 port 80                  # Traffic on port 80
tcpdump -i eth0 portrange 20-25          # Traffic in port range
tcpdump -i eth0 tcp                      # Only TCP packets
tcpdump -i eth0 udp                      # Only UDP packets
tcpdump -i eth0 icmp                     # Only ICMP packets

# Network / address filters
tcpdump -i eth0 net 10.0.0.0/24          # Traffic to/from subnet
tcpdump -i eth0 src net 10.0.0.0/24      # Traffic sourced from subnet
tcpdump -i eth0 dst net 10.0.0.0/24      # Traffic destined to subnet
tcpdump -i eth0 broadcast                # Broadcast traffic (one-to-all)
tcpdump -i eth0 multicast                # Multicast traffic (one-to-many)
tcpdump -i eth0 unicast                  # Unicast traffic (one-to-one)

# Logical operators &#x26; negation
tcpdump -i eth0 tcp port 80 and host 192.168.1.10  # HTTP traffic for a host
tcpdump -i eth0 not port 22                        # Everything except SSH
tcpdump -i eth0 tcp and src net 10.0.0.0/24        # TCP from subnet
tcpdump -i eth0 port 20 or port 21                 # Match either port 20 or 21
tcpdump -i eth0 not (src net 10.0.0.0/24)          # Everything but that subnet

# File + live combos
tcpdump -r - -l | grep 'string'   # Read piped input (-), line-buffer, grep live output
tcpdump -i eth0 -s 0 -w - | tee out.pcap  # Capture full packets (-s 0) and stream to file

# Advanced / helpful flags
tcpdump -e                      # Show link-level (Ethernet) header
tcpdump -S                      # Show absolute TCP sequence numbers
tcpdump -c 100                  # Stop after capturing 100 packets
tcpdump -s 65535                # Capture full packet (no truncation)

# TCP flags you'll see in output
# [S]   -> SYN
# [S.]  -> SYN+ACK
# [.]   -> ACK
# [P.]  -> PUSH + ACK (data)
# [F.]  -> FIN+ACK (closing)
</code></pre>
