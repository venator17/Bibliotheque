# Responder

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**Responder**</mark> is a widely used <mark style="color:yellow;">**tool**</mark> in penetration test scenarios and can be used for lateral movement across the network by red teamers. The tool contains many useful features like <mark style="color:yellow;">**LLMNR**</mark>, <mark style="color:yellow;">**NT-NS**</mark> and <mark style="color:yellow;">**MDNS**</mark> **poisoning**. It is used in practical scenarios for objectives like hash capture or poisoned answer forwarding supporting various AD attacks. More about it you could read here: [**\[LINK\]**](https://www.hackingarticles.in/a-detailed-guide-on-responder-llmnr-poisoning/)

## <mark style="color:yellow;">**Set up a fake SMB Server**</mark>

```bash
responder -I {INTERFACENAME}
```

With this we could intercept information when machine computer tries to do <mark style="color:yellow;">**Name Resolution (PR)**</mark>, because it couldn't find a share's IP address in **/etc/hosts,** in **DNS cache** and in **local DNS server**. Because of IP address absence, it would make a multicast request, which we could intercept and use credentials for impersonation. This is <mark style="color:yellow;">**NTLM Relay attack**</mark>, where we are intercepting NTLM authentication request.

<pre class="language-bash"><code class="lang-bash">impacket-ntlmrelayx --no-http-server -smb2support -t 13.13.13.13
<strong># ALSO USE -c to execute command
</strong></code></pre>
