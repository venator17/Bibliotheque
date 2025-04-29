---
description: Some useful commands for Linux which could help you out.
---

# Useful Commands

## Cut

The <mark style="color:blue;">**cut**</mark> command allows you to extract specific sections (columns) of lines from a file or input stream by "cutting" the line into columns based on a delimiter and selecting which columns to display

```bash
--> cut -d ' ' -f1,3,6 access.log
[2023/10/25:15:42:02] sway.com:443 200
[2023/10/25:15:42:02] sway.com:443 301
```

## Top

The [**top**](https://www.geeksforgeeks.org/top-command-in-linux-with-examples/) command shows you a list of processes in real time with their usage. It's a dynamic list, meaning it changes with the resource usage of each process.

## **Look for an installed software**

```bash
dpkg -l
```

## **Base64 encode/decode**

```bash
base64 [encode]
base64 -d [decode]
```

## **Grab banner**

```bash
nc -nv 13.13.13.13 25
sudo tcpdump -i eth0 host 13.13.13.13 and 13.13.13.14
```

## pspy64

Use **pspy64** script to monitor Linux processes

```bash
./pspy64
```

## File Hunting <a href="#file-hunting" id="file-hunting"></a>

```bash
for ext in $(echo ".xls .xls* .xltx .csv .od* .doc .doc* .pdf .pot .pot* .pp*");do echo -e "File extension: " $ext; find / -name *$ext 2>/dev/null | grep -v "lib\|fonts\|share\|core" ;done​
```

***
