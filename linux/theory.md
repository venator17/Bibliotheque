---
icon: book-open
description: Linux have one big rule "everything is a file"
---

# Theory

## <mark style="color:yellow;">Crontab</mark>

**`Cron` jobs in Linux allow users to run commands at the specific date and time. To list all scheduled tasks for the user**

* <mark style="color:green;">**`crontab -l`**</mark> **Look for your crontab file**
* <mark style="color:green;">**`crontab -e`**</mark> **To edit your crontab file**

**If this command is run at the first time user will be asked to choose text editor for editing this file.To create a scheduled command user needs to create a records based on the following template**

* <mark style="color:yellow;">**`m h dom mon dow command`**</mark>

**Also you could check privileges for files like this, to locate cron jobs:**

* <mark style="color:green;">`/etc/crontab`</mark>
* <mark style="color:green;">`/etc/cron.d`</mark>
* <mark style="color:green;">`/var/spool/cron/crontabs/root`</mark>

[**\[Link to make cron date\]**](https://crontab.guru/#25_18_8_11_0)

## <mark style="color:yellow;">Regex Basics</mark>

<mark style="color:red;">**Regular expressions**</mark>, often referred to as **regex** or **regexp**, are a powerful <mark style="color:purple;">**tool**</mark> for pattern matching and text manipulation. They provide a concise and flexible way to search for, match, and extract specific patterns in text data. Regex is supported in many programming languages and text editors. Here are some of the basics of regex with examples for each feature:

* <mark style="color:blue;">**Literal Characters:**</mark>
  * A regex can represent literal characters. For example, the regex `cat` will match the word "cat" in a text.
* <mark style="color:blue;">**Character Classes:**</mark>
  * Square brackets `[]` are used to define character classes. For example, `[aeiou]` matches any vowel, and `[0-9]` matches any digit.
* <mark style="color:blue;">**Quantifiers:**</mark>
  * Quantifiers specify how many times a character or group of characters should be repeated.
  * `*` matches zero or more of the preceding element. For example, `ca*t` matches "ct," "cat," "caat," and so on.
  * `+` matches one or more of the preceding element. For example, `ca+t` matches "cat," "caat," and so on.
  * `?` matches zero or one of the preceding element. For example, `colou?r` matches "color" and "colour."
* <mark style="color:blue;">**Wildcard:**</mark>
  * The dot `.` represents any character (except a newline character). For example, `c.t` matches "cat," "cut," "c8t," etc.
* <mark style="color:blue;">**Anchors:**</mark>
  * `^` matches the start of a line. For example, `^abc` matches "abc" only if it's at the beginning of a line.
  * `$` matches the end of a line. For example, `xyz$` matches "xyz" only if it's at the end of a line.
* <mark style="color:blue;">**Groups and Alternation:**</mark>
  * Parentheses `()` are used to create groups.
  * `|` represents alternation (OR). For example, `(cat|dog)` matches either "cat" or "dog."
* <mark style="color:blue;">**Character Escapes:**</mark>
  * Some characters have special meanings in regex and need to be escaped with a backslash. For example, `\.` matches a literal period.
* <mark style="color:blue;">**Quantifier Min and Max:**</mark>
  * Curly braces `{}` allow you to specify the minimum and maximum number of repetitions. For example, `a{2,4}` matches "aa," "aaa," and "aaaa."
* <mark style="color:blue;">**Character Shorthands:**</mark>
  * There are shorthands for common character classes:
    * `\d` matches any digit (equivalent to `[0-9]`).
    * `\w` matches any word character (equivalent to `[a-zA-Z0-9_]`).
    * `\s` matches any whitespace character (spaces, tabs, line breaks, etc.).
* <mark style="color:blue;">**Negation:**</mark>
  * You can use `^` inside a character class to negate it. For example, `[^0-9]` matches any character that is not a digit.
* <mark style="color:blue;">**Backreferences:**</mark>
  * You can refer to matched groups later in the regex using backreferences. For example, `(abc)\1` matches "abcabc."
* <mark style="color:blue;">**Modifiers:**</mark>
  * Flags like `i` (case-insensitive) can be added after the regex to change its behavior. For example, `/cat/i` matches "cat," "Cat," or "CAT."

Here are some examples of regular expressions and what they match:

* <mark style="color:green;">`/^abc/`</mark> matches "abc" at the beginning of a line.
* <mark style="color:green;">`/[0-9]+/`</mark> matches one or more digits.
* <mark style="color:green;">`/colou?r/`</mark> matches "color" or "colour."
* <mark style="color:green;">`/[A-Za-z]+/`</mark> matches one or more uppercase or lowercase letters.
* <mark style="color:green;">`/[aeiou]{2,4}/`</mark> matches 2 to 4 consecutive vowels.

## <mark style="color:yellow;">Logical Operators</mark>

**Symbols or keywords in Linux that are used to process and compare logical values.**

| **Syntax**                                                   | **Explanation**                                                                                                                                                                                                   |
| ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <mark style="color:yellow;">**&&**</mark>                    | (AND)                                                                                                                                                                                                             |
| <mark style="color:green;">**`Command1 && Command2`**</mark> | Executes Command2 only if Command1 succeeds (returns a zero exit code). If Command1 fails, Command2 is not executed                                                                                               |
| <mark style="color:yellow;">**II**</mark>                    | (OR)                                                                                                                                                                                                              |
| <mark style="color:green;">**`Command1 II Command2`**</mark> | Executes Command2 only if Command1 fails (returns a non-zero exit code). If Command1 succeeds, Command2 is not executed                                                                                           |
| <mark style="color:yellow;">**;**</mark>                     | (Semicolon)                                                                                                                                                                                                       |
| <mark style="color:green;">**`Command1 ; Command2`**</mark>  | Executes Command2 regardless of the success or failure of Command1. Used for sequential execution of commands                                                                                                     |
| <mark style="color:yellow;">**&**</mark>                     | (Background Execution)                                                                                                                                                                                            |
| <mark style="color:green;">**`Command &`**</mark>            | Executes the command in the background, allowing you to continue working in the terminal without waiting for the command to complete. You can use the **bg** or **jobs** commands to control background processes |
| <mark style="color:yellow;">**!**</mark>                     | (NOT)                                                                                                                                                                                                             |
| <mark style="color:green;">**`! Command`**</mark>            | Executes the command and returns the reverse exit code. If Command succeeds, ! Command fails, and vice versa                                                                                                      |
| <mark style="color:yellow;">**I**</mark>                     | (PIPE)                                                                                                                                                                                                            |
| <mark style="color:green;">**`Command1 I Command2`**</mark>  | Redirects the output of Command1 to the input of Command2. Used to transfer data between commands and filter the output                                                                                           |

## <mark style="color:yellow;">Access Rights</mark>

**Linux has its own scheme for displaying access rights using numbers to make it quick and easy to show which rights are where. Each three digits corresponds to three access rights (read, write, execute) for three different categories of users (owner, group, other). Each of these digits can have a value from 0 to 7, where each value represents a combination of three possible access rights:**

> <mark style="color:yellow;">**0 - (no rights). 1 - (execute). 2 - (write). 4 - (read).**</mark>

### <mark style="color:blue;">**File Rights**</mark>

To set permissions using numbers, you simply add the number values for each category together: For example, \`<mark style="color:green;">**`chmod 755 file.txt'`**</mark> sets the following permissions:

1. The owner has read, write, and execute permissions **(4 + 2 + 1 = 7).**
2. Group has read and execute permissions **(4 + 1 = 5).**
3. Other users have read and execute permissions **(4 + 1 = 5).**

### <mark style="color:blue;">**Directory Rights**</mark>

For example, in the directory, it displays <mark style="color:green;">**`drwxr-xr-x`**</mark>. The first character <mark style="color:green;">**`d`**</mark> is the type of object. In this case, <mark style="color:green;">**`d`**</mark> indicates that it is a directory. The rest of the <mark style="color:green;">**`rwxr-xr-x`**</mark> string consists of **nine** characters that represent access rights for different categories of users <mark style="color:yellow;">**(**</mark>_<mark style="color:yellow;">**owner, group, and others**</mark>_<mark style="color:yellow;">**)**</mark>. This part of the string can be considered as three sets of three characters each.

The first set <mark style="color:green;">**`rwx`**</mark> represents the access rights for the _**object owner**_:

1. <mark style="color:green;">**`r`**</mark> _**Owner**_ has the right to read the file or view the contents of the directory.
2. <mark style="color:green;">**`-`**</mark> _**Owner**_ has the right to write or edit the file or create new files in the directory.
3. <mark style="color:green;">**`x`**</mark> _**Owner**_ has the right to execute the file (for directories, this means the ability to access it as a directory).

The second set of <mark style="color:green;">**`r-x`**</mark> represents the access rights for a _**user group**_:

1. <mark style="color:green;">**`r`**</mark> _**Group**_ has the right to read the file or view the contents of the directory.
2. <mark style="color:green;">**`-`**</mark> _**Group**_ does not have the right to write the file or create new files in the directory.
3. <mark style="color:green;">**`x`**</mark> _**Group**_ has the right to execute the file (for directories).

The third set of <mark style="color:green;">**`r-x`**</mark> represents access rights for _**other users**_ (users who are not owners and do not belong to the group):

1. <mark style="color:green;">**`r`**</mark> _**Other users**_ have the right to read the file or view the contents of the directory.
2. <mark style="color:green;">**`-`**</mark> _**Other users**_ do not have the right to write the file or create new files in the directory.
3. <mark style="color:green;">**`x`**</mark> _**Other users**_ have the right to execute the file (for directories).

## <mark style="color:yellow;">Data Streams, Redirects</mark>

In Linux, there is such a thing as _data streams_, which are used to transmit input/output data in programs. Each of them has its own _descriptor_, a numeric identifier that helps to interact with them more easily

* <mark style="color:blue;">`STDIN`</mark> - Descriptor 0. Input stream
* <mark style="color:blue;">`STDOUT`</mark> - Descriptor 1. Output stream
* <mark style="color:blue;">`STDERR`</mark> - Descriptor 2. Error stream
* The output in the output streams is separate and in parallel.

_REDIRECT( > )_ is redirect of the command output to the file <mark style="color:green;">`(ls > dirs.txt)`</mark>. Redirect by default is through the <mark style="color:green;">`stdout`</mark> stream, but it can be changed. <mark style="color:green;">`cat unexistedfile.txt 2> error.txt`</mark> _Reverse redirect ( < )_ is redirect of the output stream through `stdin` so that the input is not through the keyboard but through the file

### Examples

<mark style="color:green;">`2>&1`</mark> _If we redirect the output from <mark style="color:green;">`stderr`</mark>, we output to the same place as the output from `stdout`. And with this we can output both simple output and errors in one file, one stream_.

<mark style="color:green;">`0>&1`</mark> _By using **0>&1**, you are actually telling the shell to read <mark style="color:green;">`stdin`</mark> from the same source as <mark style="color:green;">`stdout`</mark>. This can be useful in cases where you need to merge or copy input and output streams for interactive input, for example in reverse shells_.

## <mark style="color:yellow;">File signatures</mark>

File signatures, commonly referred to as "**magic bytes**", are specific byte sequences at the beginning of a file that identify or verify its content type and format. These bytes often have corresponding **ASCII** characters, allowing for easier human readability when inspected. The identification process helps software applications quickly determine whether a file is in a format they can handle, aiding operational functionality and security measures.

* In cyber security, file signatures are crucial for identifying file types and formats. You'll encounter them in malware analysis, incident response, network traffic inspection, web security checks, and forensics. Knowing how to work with these magic bytes can help you quickly identify malicious or suspicious activity and choose the right tools for deeper analysis.

**Here is a list of some of the most common files and their magic:**

| File Format                 | Magic Bytes             | ASCII |
| --------------------------- | ----------------------- | ----- |
| PNG image file              | 89 50 4E 47 0D 0A 1A 0A | %PNG  |
| GIF image file              | 47 49 46 38             | GIF8  |
| Windows and DOS executables | 4D 5A                   | MZ    |
| Linux ELF executables       | 7F 45 4C 46             | .ELF  |
| MP3 audio file              | 49 44 33                | ID3   |

* You could look all magic bytes here [**\[LINK\]**](https://en.wikipedia.org/wiki/List_of_file_signatures)

## <mark style="color:yellow;">Mount</mark>

<mark style="color:red;">**Mount**</mark> command is used to <mark style="color:purple;">**attach**</mark> (or "mount") file systems to a directory structure, making storage devices like hard drives, USB drives, or network file systems accessible under a specific directory (mount point). The mounting process allows users and the system to read/write data from/to the storage device.

#### Regular Mount

```bash
mount /dev/sda1 /mnt
```

#### Authenticated Mount

```bash
sudo mount -t cifs -o username=ven17,password=superkek123,domain=. //13.13.13.13/Share /mnt/Share
```
