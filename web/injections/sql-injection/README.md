---
description: >-
  IN SOME EXAMPLES I WOULD USE SCREENSHOTS FROM OBSIDIAN, BECAUSE IT CORRECTLY
  INTERPRETS SQL REQUESTS
---

# SQL Injection

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**SQL injection (SQLi)**</mark> is a <mark style="color:purple;">**critical web security vulnerability**</mark> that allows an attacker to interfere with the queries that an application makes to its database. This manipulation can enable an attacker to view data they are not normally able to retrieve, such as data belonging to other users or any other information the application can access. In many operational scenarios, an attacker can <mark style="color:purple;">**modify or delete this data**</mark>, causing persistent changes to the application's content or behavior, which fundamentally compromises the integrity of the system.

{% hint style="warning" %}
&#x20;**Start small, then steadily build toward greater impact**
{% endhint %}

## <mark style="color:yellow;">WHERE TO LOOK</mark>

Most SQL injection vulnerabilities occur within the **WHERE** clause of a **SELECT** query. Most experienced testers are familiar with this type of SQL injection. However, SQL injection vulnerabilities can occur at any location within the query, and within different query types. Some other common locations where SQL injection arises are:

* In **UPDATE** statements, within the updated values or the **WHERE** clause.
* In **INSERT** statements, within the inserted values.
* In **SELECT** statements, within the table or column name.
* In **SELECT** statements, within the **ORDER BY** clause.&#x20;

{% hint style="info" %}
So the main idea is to learn application and search for where is most likely SQL database requests in back-end, and test payloads there
{% endhint %}

## <mark style="color:yellow;">APPROACH</mark>

How to detect SQL injection vulnerabilities

You can detect SQL injection manually using a systematic set of tests against every entry point in the application. To do this, you would typically submit:

* The single quote character `'` and <mark style="color:orange;">**look for errors or other anomalies**</mark>.
* Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and to a different value, and <mark style="color:orange;">**look for systematic differences in the application responses.**</mark>
* <mark style="color:orange;">**Boolean conditions**</mark> such as `OR 1=1` and `OR 1=2`, and look for differences in the application's responses.
* Payloads designed to trigger <mark style="color:orange;">**time delays**</mark> when executed within a SQL query, and look for differences in the time taken to respond.
* OAST payloads designed to <mark style="color:orange;">**trigger an out-of-band network interaction**</mark> when executed within a SQL query, and monitor any resulting interactions.&#x20;

{% hint style="info" %}
Alternatively, you can find the majority of SQL injection vulnerabilities quickly and reliably using Burp Scanner.
{% endhint %}

## <mark style="color:yellow;">EXAMPLES</mark>

The following payloads demonstrate basic retrieval techniques used in standard testing scenarios. The first payload utilizes a comment indicator (`--`) to remove the trailing SQL constraints, effectively displaying unreleased products. The second payload injects a boolean tautology (`OR 1=1`) to force the database to return every record in the table, bypassing specific category filters.

On the back-end SQL query probably looks like this:

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

In first payload we use -- comment indicator to cut off the next part of request.

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

We can see here SQL syntax interpretation: part after **Gifts** is seen as a comment.

The other way we can add out payload is by using logical operators, like `OR`

<figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

In this scenario we use OR 1=1, and because 1=1 is always true. Database would show us everything&#x20;

{% hint style="danger" %}
Yes we are using OR 1=1 as example. but that payload is considered aggressive, because it can be seen by other non-seen part of request which can delete some tables as example. And together you an have devastating consequences, so don't be a gonk and don't use that anywhere except training.
{% endhint %}

## <mark style="color:yellow;">PREVENTION</mark>

The most effective method to prevent SQL injection is the use of parameterized queries, also known as prepared statements, instead of string concatenation within the query. For example, vulnerable Java code that concatenates user input directly into a string is highly susceptible to attack. Secure implementation involves defining the query structure with placeholders and then setting the value using specific methods, which ensures the database treats the input strictly as data and not as executable code.

## <mark style="color:yellow;">ADDITIONAL NOTES</mark>

It is important to note that SQL injection attacks can be performed using any controllable input processed as a SQL query by the application, including input formats like JSON or XML. Different formats may provide unique methods to obfuscate attacks that might otherwise be blocked by WAFs. For instance, an XML-based injection can use escape sequences to encode specific characters, such as encoding the "S" in `SELECT(999 &#x53;ELECT...)`, which is decoded server-side before execution19.

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://portswigger.net/web-security/sql-injection/cheat-sheet" %}
