# Bits, Representation, Integer/Float Limits – Anki (Markdown)

Q: What is `Number.MAX_SAFE_INTEGER` in JavaScript?  
A: `2^53 - 1` (9007199254740991), the largest integer that JavaScript `Number` can represent without losing precision.

Q: What does “safe integer” mean in JavaScript?  
A: An integer that can be represented exactly in a `Number` without rounding, so equality and arithmetic behave reliably up to ±`Number.MAX_SAFE_INTEGER`.

Q: Why can’t JavaScript represent all integers larger than `2^53 - 1` exactly?  
A: `Number` uses 64‑bit IEEE‑754 floating point, where only 53 bits are available for the integer part, so larger integers are quantized and some distinct values collapse together.

Q: Why does `0.1 + 0.2 === 0.3` return false in JavaScript?  
A: `0.1` and `0.2` are not stored as exact decimals in binary floating point, so their sum is a nearby value like 0.30000000000000004, not exactly 0.3.[web:19][web:21]

Q: What is the general rule for comparing floating‑point numbers?  
A: Avoid direct equality checks; compare whether the absolute difference is smaller than a small tolerance (epsilon).[web:21][web:37]

Q: Why are binary floating‑point numbers bad for storing money directly?  
A: They cannot represent many decimal fractions exactly, so repeated operations and equality checks can introduce rounding errors into prices and totals.[web:21][web:25]

Q: What is a safer way to represent currency in code?  
A: Store monetary amounts as integer minor units (like cents or paise) and only convert to decimal when displaying to the user.[web:21][web:26]

Q: Why can large numeric IDs from a database be dangerous in JavaScript?  
A: If an ID exceeds the safe integer range, parsing it as a JavaScript `Number` can round it, so different IDs may become equal in JavaScript.[web:13][web:29]

Q: What is a common way to avoid ID precision problems in APIs?  
A: Send IDs as strings in JSON and keep them as strings on the frontend, or use `BigInt`/big‑integer types when exact large integers are required.[web:19][web:28]

Q: Is this “bits and limits” issue unique to JavaScript?  
A: No. It comes from fixed‑width integers and IEEE‑754 floating point, which affect many languages (Java, C, Ruby, Python, etc.); only the surface APIs differ.[web:19][web:23][web:30]

Q: What happens when an integer value overflows its type range (for example, 32‑bit `int`)?  
A: The value wraps around or saturates depending on the language/runtime, often without an error, leading to incorrect results.[web:17][web:19][web:33]

Q: How does understanding bit limits help prevent bugs?  
A: It helps in choosing correct types and boundaries, adding edge‑case tests, and avoiding floats where exact values are needed, preventing subtle logic and data bugs.[web:17][web:21][web:33]

Q: How can numeric representation affect performance?  
A: Integers are usually cheaper than floats, and smaller fixed types use less memory and cache, so choosing appropriate integer/float types can improve efficiency in tight loops.[web:19][web:34][web:35]

Q: What simple mental model explains floating‑point rounding?  
A: A measuring cup with limited marks: you can only store numbers at specific marks, and any other value is rounded to the nearest mark.[web:21][web:25]

Q: Which ranges of integers are guaranteed to be safe in JavaScript `Number`?  
A: From −9,007,199,254,740,991 to +9,007,199,254,740,991 (inclusive), i.e., ±(2^53 − 1). Within this range, integers are represented exactly.[web:13][web:29]
