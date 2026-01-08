---
icon: merge
---

# UNION-BASED

## <mark style="color:yellow;">ABOUT</mark>

When an application is vulnerable to SQL injection, and the results of the query are returned within the application's responses, you can use the UNION keyword to retrieve data from other tables within the database. This is commonly known as a SQL injection UNION attack.

The UNION keyword enables you to execute one or more additional SELECT queries and append the results to the original query. For example:

```sql
SELECT a, b FROM table1 UNION SELECT c, d FROM table2
```

## <mark style="color:yellow;">WHERE TO LOOK</mark>

## <mark style="color:yellow;">APPROACH</mark>

This SQL query returns a single result set with two columns, containing values from columns **a** and **b** in **table1** and columns **c** and **d** in **table2**.

{% hint style="warning" %}
For a UNION query to work, <mark style="color:red;">**two key requirements**</mark> must be met:

* <mark style="color:orange;">**The individual queries must return the same number of columns.**</mark>
* <mark style="color:orange;">**The data types in each column must be compatible between the individual queries.**</mark>
{% endhint %}

{% hint style="success" %}
To carry out a **SQL injection UNION attack**, make sure that your attack meets these <mark style="color:red;">**two requirements**</mark>. This normally involves finding out:

* <mark style="color:orange;">**How many columns are being returned from the original query.**</mark>
* <mark style="color:orange;">**Which columns returned from the original query are of a suitable data type to hold the results from the injected query.**</mark>&#x20;
{% endhint %}

### <mark style="color:blue;">**1. Determining column count**</mark>

{% hint style="info" %}
It required for UNION operator to have same number of columns in each part of query, because otherwise it could not have proper table output, where one part is 3 columns, other is 2, and the other is 7.
{% endhint %}

There are two effective methods to determine how many columns are being returned from the original query:

<details>

<summary><mark style="color:green;"><strong>ORDER BY</strong></mark></summary>

<mark style="color:orange;">**One method**</mark> involves injecting a series of <mark style="color:green;">**ORDER BY**</mark> clauses and incrementing the specified column index <mark style="color:purple;">**until an error occurs**</mark>. For example, if the injection point is a quoted string within the WHERE clause of the original query, you would submit:

```sql
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
```

This series of payloads modifies the original query to order the results by different columns in the result set. The column in an ORDER BY clause can be specified by its index, so you <mark style="color:purple;">**don't need to know the names of any columns**</mark>. When the specified column index exceeds the number of actual columns in the result set, the database returns an error, such as:

`The ORDER BY position number 3 is out of range of the number of items in the select list.`

The application might actually return the database error in its HTTP response, but it may also issue a generic error response. In other cases, it may simply return no results at all. Either way, as long as you can detect some difference in the response, you can infer how many columns are being returned from the query.

</details>

<details>

<summary><mark style="color:green;"><strong>UNION SELECT</strong></mark></summary>

The <mark style="color:orange;">**second method**</mark> involves submitting a series of <mark style="color:green;">**UNION SELECT**</mark> payloads specifying a different number of null values:

```sql
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
```

If the number of nulls **does not match** the number of columns, the database returns an error, such as:

`All queries combined using a UNION, INTERSECT or EXCEPT operator must have an equal number of expressions in their target lists.`

{% hint style="info" %}
We use NULL as the values returned from the injected SELECT query because the data types in each column must be compatible between the original and the injected queries. NULL is convertible to every common data type, so it maximizes the chance that the payload will succeed when the column count is correct.
{% endhint %}

</details>

{% hint style="warning" %}
Those two methods are not gonna necessarily work, it would depend on an application (as always). If the output is present, you can move forward to use UNION to get some useful information. If the difference is in time delay, that's probably TIME-BASED Injection. If the difference is different error output, theoretically it could be ERROR-BASED Injection. If nothing of it works, it still could be BLIND Injection
{% endhint %}

### <mark style="color:blue;">2. Examining the database</mark>

When you have determined the number of columns returned by the original query and found which columns can hold string data, you are in a position to retrieve data, just for that you need to know <mark style="color:purple;">**type of database, it's version, the tables, columns and their data types**</mark>.

{% hint style="info" %}
You can potentially identify both the database type and version by injecting provider-specific queries to see if one works
{% endhint %}

| Database type | Query                                                                                           |
| ------------- | ----------------------------------------------------------------------------------------------- |
| Oracle        | <p><code>SELECT banner FROM v$version</code><br><code>SELECT version FROM v$instance</code></p> |
| Microsoft     | `SELECT @@version`                                                                              |
| PostgreSQL    | `SELECT version()`                                                                              |
| MySQL         | `SELECT @@version`                                                                              |

Most database types (except Oracle) have a set of views called the information schema. This provides information about the database.

For example, you can query **information\_schema.tables** to list the tables in the database:

<pre class="language-sql"><code class="lang-sql">SELECT * FROM information_schema.tables
<strong>'This returns output like the following:'
</strong>TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  TABLE_TYPE
=====================================================
MyDatabase     dbo           Products    BASE TABLE
MyDatabase     dbo           Users       BASE TABLE
MyDatabase     dbo           Feedback    BASE TABLE
</code></pre>

This output indicates that there are three tables, called **Products**, **Users**, and **Feedback**.

You can then query **information\_schema.columns** to list the columns in individual tables:&#x20;

```sql
SELECT * FROM information_schema.columns WHERE table_name = 'Users'
'This returns output like the following:'
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  COLUMN_NAME  DATA_TYPE
=================================================================
MyDatabase     dbo           Users       UserId       int
MyDatabase     dbo           Users       Username     varchar
MyDatabase     dbo           Users       Password     varchar
'This output shows the columns in the specified table and the data type of each column.'
```

{% hint style="warning" %}
**Start small, then steadily build toward greater impact**
{% endhint %}

### <mark style="color:blue;">3. Identifying reflected columns</mark>

A UNION query may execute correctly while producing no usable signal if the injected output lands in a column that the application does not render. The frontend determines which parts of the result set become observable. Reflection defines the extraction channel. This step separates syntactic success from operational visibility and prevents false confidence when the backend executes correctly but the UI suppresses output. Understanding rendering behavior also reveals truncation limits, encoding transformations, and formatting constraints.

### <mark style="color:blue;">4. Validating data type compatibility</mark>

Each reflected column imposes semantic constraints on what data can be safely injected and rendered. Numeric columns, strict type systems, implicit coercion rules, and binary representations influence whether extracted data survives intact. Misaligned types cause silent corruption, runtime errors, or invisible output. This step ensures that the extraction channel can faithfully carry the intended information without distortion or instability.

### <mark style="color:blue;">5. Structuring readable output</mark>

Even when extraction is technically possible, raw output may be inefficient, fragmented, or difficult to interpret. Consolidation of multiple values into a single visible channel improves signal density and reduces dependency on UI layout. Delimiters, ordering consistency, and aggregation strategies increase human readability and reduce ambiguity. This step optimizes information throughput under display and rendering constraints.

### <mark style="color:blue;">6. Adapting to engine-specific behavior</mark>

SQL is not uniform across implementations. Function availability, concatenation semantics, aggregation behavior, casting strictness, identifier handling, comment parsing, and mandatory query structure differ between engines. Assumptions valid in one environment may silently fail in another. This step enforces adaptability and prevents overgeneralization from isolated success cases.

### <mark style="color:blue;">7. Accounting for transport and decoding layers</mark>

Input does not travel directly from client to SQL parser. It passes through encoding, decoding, normalization, filtering, and sometimes security middleware. Each layer can transform characters, whitespace, delimiters, and escape sequences. Payload intent must survive these transformations intact. Misunderstanding this chain leads to malformed logic, inconsistent behavior, and false diagnostics. This step maintains alignment between conceptual payload design and actual executed query structure.

## <mark style="color:yellow;">EXAMPLES</mark>

<details>

<summary>UNION SELECT Usage</summary>

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

```sql
Clothing%2c+shoes+and+accessories'+UNION+SELECT+NULL,NULL,NULL--
```

Here we are using quote symbol (') to close WHERE (where we suppose editable variable is), then use (+) as a URL encoded space symbol to combine different operations, and comment (--+) to cut out the continuation of request.

</details>

<details>

<summary>UNION CONCAT Usage</summary>

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

```sql
Corporate%2bgifts'+UNION+SELECT+NULL,CONCAT(password,+'---',+username)+FROM+users--
```

Here we use the `CONCAT()` function to combine multiple columns from the same row into a single output value. This allows multiple fields to be displayed in one visible column when only limited output is available. A delimiter (e.g., `'---'`) can be inserted between values to improve readability.

</details>

<details>

<summary>Listing the database contents on non-Oracle databases</summary>

<figure><img src="../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

```sql
Gifts'+UNION+ALL+SELECT+username_suvbzh,+password_wlssnr+FROM+users_gsoobj--
```

Here we are requesting **all rows** from table `users_gsoobj` and output the two specified columns, aligned into the UNION result set.

</details>

<details>

<summary>information_schema DB extraction</summary>

1. Enumerates all tables and their schemas in the database.

```sql
Gifts'+UNION+SELECT+table_name,+table_schema+FROM+information_schema.tables--
```

2. Enumerates column names for a specific table.

```sql
Gifts'+UNION+SELECT+column_name,+table_name+FROM+information_schema.columns+WHERE+table_name%3d'users_gsoobj'--
```

3. Extracts real data and merges multiple fields into one visible column.

```sql
Gifts'+UNION+ALL+SELECT+NULL,CONCAT(username_suvbzh,+'---',+password_wlssnr,'---',+email)+FROM+users_gsoobj--
```

</details>

## <mark style="color:yellow;">PREVENTION</mark>

{% hint style="danger" %}
**WIP**
{% endhint %}

## <mark style="color:yellow;">ADDITIONAL NOTES</mark>

{% hint style="warning" %}
Use trailing space (`--` ) with a space after it because it's usually required in SQL engines
{% endhint %}
