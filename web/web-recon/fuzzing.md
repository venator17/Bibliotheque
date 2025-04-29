# Fuzzing

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**Fuzzing**</mark> is a <mark style="color:purple;">**technique**</mark> involves inputting massive amounts of random data, called <mark style="color:yellow;">**fuzz**</mark>, to the test subject in an attempt to make it <mark style="color:blue;">**crash**</mark>, <mark style="color:blue;">**hack**</mark> or <mark style="color:blue;">**behave useful for us**</mark>.

## <mark style="color:yellow;">Ffuf</mark>

| **Command**                                                                                                                                                                                          | **Description**          |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| <mark style="color:green;">**`ffuf -h`**</mark>                                                                                                                                                      | ffuf help                |
| <mark style="color:green;">**`ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ`**</mark>                                                                                                      | Directory Fuzzing        |
| <mark style="color:green;">**`ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/indexFUZZ`**</mark>                                                                                                 | Extension Fuzzing        |
| <mark style="color:green;">**`ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/page/FUZZ.php`**</mark>                                                                                             | Page Fuzzing             |
| <mark style="color:green;">**`ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v`**</mark>                                                             | Recursive Fuzzing        |
| <mark style="color:green;">**`ffuf -w wordlist.txt:FUZZ -u https://FUZZ.amogus.com/`**</mark>                                                                                                        | Sub-domain Fuzzing       |
| <mark style="color:green;">**`ffuf -w wordlist.txt:FUZZ -u http://amogus.com:PORT/ -H 'Host: FUZZ.amogus.com' -fs xxx`**</mark>                                                                      | VHost Fuzzing            |
| <mark style="color:green;">**`ffuf -w wordlist.txt:FUZZ -u http://admin.amogus.com:PORT/admin/admin.php?FUZZ=key -fs xxx`**</mark>                                                                   | Parameter Fuzzing - GET  |
| <mark style="color:green;">**`ffuf -w wordlist.txt:FUZZ -u http://admin.amogus.com:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx`**</mark> | Parameter Fuzzing - POST |
| <mark style="color:green;">**`ffuf -w ids.txt:FUZZ -u http://admin.amogus.com:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx`**</mark>       | Value Fuzzing            |

## <mark style="color:yellow;">Wordlists</mark>

| **Command**                                                                                                     | **Description**         |
| --------------------------------------------------------------------------------------------------------------- | ----------------------- |
| <mark style="color:green;">**`/opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt`**</mark> | Directory/Page Wordlist |
| <mark style="color:green;">**`/opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt`**</mark>           | Extensions Wordlist     |
| <mark style="color:green;">**`/opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt`**</mark>      | Domain Wordlist         |
| <mark style="color:green;">**`/opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt`**</mark>     | Parameters Wordlist     |
