---
icon: clock
---

# TIME-BASED

## <mark style="color:$primary;">ABOUT</mark>

Classic time-based SQL injection works by forcing the database to <mark style="color:purple;">**deliberately pause execution for a controlled amount of time**</mark>, then inferring truth from the delay observed in the HTTP response. No errors, no output, no visible data—just time as the side channel. You embed conditional logic that triggers a sleep, wait, or heavy computation only when a predicate is true, then measure the difference. This is blind in-band: the data never appears in the response body, only in response timing. It survives hardened error handling, suppressed output, and generic error pages. Common in modern apps with prepared statements partially applied, verbose errors disabled, and WAFs tuned to block obvious UNION or error-based payloads but not logic abuse.

## <mark style="color:$primary;">WHERE TO LOOK</mark>

Focus on parameters that influence query logic but return identical responses regardless of input, especially where responses are consistently 200/302 and content length doesn’t change. Targets include login flows, filters, search endpoints, feature flags, and API parameters backed by synchronous database queries. Works best where network latency is stable enough to distinguish intentional delays from noise, and where the backend database exposes sleep primitives or can be coerced into measurable execution stalls.

## <mark style="color:$primary;">EXAMPLES</mark>

<details>

<summary>Classic Blind Time-Based SQLI</summary>

```sql
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

The main difference here is usage of pg\_sleep(time) operator, and the main core is good old bool sqli, because we can't get info from it with anything else than true/false. Though it takes longer because of time pauses to complete, so these types of SQLI's are the grinders and usually fall on automation hands

</details>
