---
icon: binary-slash
---

# ERROR-BASED

## <mark style="color:$primary;">ABOUT</mark>

Classic error-based SQL injection occurs when you deliberately break the query syntax, the database throws a verbose error, and that error message leaks useful information: parts of the original query, database type/version, table/column names, or even data fragments. No CAST tricks, no conditional branching, no type mismatches engineered to leak values—just raw syntax errors exposing internals because the application fails to suppress or sanitize error output.

This is pure in-band: the data you want comes back in the response body. Works best on legacy PHP apps (MySQL/MSSQL/PostgreSQL), old CMS plugins, custom dev environments where display\_errors=On and error\_reporting is not masked, or misconfigured production servers that still echo stack traces.

## <mark style="color:$primary;">WHERE TO LOOK</mark>

Focus on parameters that land directly in dynamic SQL without prepared statements or proper escaping, and where the backend returns a full 500 page with database diagnostics instead of a generic “Internal Server Error”.

## <mark style="color:$primary;">EXAMPLES</mark>

<details>

<summary>CAST Operator Usage</summary>

You can use the `CAST()` function to achieve generating an error message in application that contains some of the data that is returned by the query.. It enables you to convert one data type to another. For example, imagine a query containing the following statement:

```sql
CAST((SELECT example_column FROM example_table) AS int)
```

Often, the data that you're trying to read is a string. Attempting to convert this to an incompatible data type, such as an int, may cause an error similar to the following:&#x20;

`ERROR: invalid input syntax for type integer: "Example data"`

This type of query may also be useful if a character limit prevents you from triggering conditional responses.

<figure><img src="../../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

```sql
'AND+1=CAST((SELECT+password+FROM+users LIMIT 1)AS+int)--
```

`LIMIT 1` is there to force the subquery to return exactly one row — a single value.

`= 1` is not there to “compare types” and it’s not there to fix a string problem. It’s there to turn a non-boolean expression into a boolean one. `1 = <something>` returns `boolean`. That satisfies `AND`.

</details>
