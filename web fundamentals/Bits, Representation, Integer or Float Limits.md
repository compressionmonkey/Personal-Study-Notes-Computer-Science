# Simple Concept
This note turns the session format into a practical sparring session for the concept of JavaScript number bugs, unsafe IDs, and money precision. The underlying computer science idea is number representation, especially IEEE 754 floating-point behavior and JavaScript safe integer limits.
# Session goal
By the end of the session, both people should be able to explain why 0.1 + 0.2 !== 0.3, why very large numeric IDs become dangerous in JavaScript, and why money should usually be stored as integer minor units such as cents instead of floating-point values

# Concepts to run through 
- Computers store numbers in bits, not in perfect decimal form.

- JavaScript Number uses double-precision floating point, so many decimals such as 0.1 cannot be represented exactly.

- JavaScript can safely represent integers only up to Number.MAX_SAFE_INTEGER, which is 9007199254740991 or 2^53 - 1.

- If an integer is larger than that, comparisons and stored IDs can become unreliable.

# Mental Modal 
A JavaScript number is like a measuring cup with limited markings. Some values fit exactly; others are rounded to the nearest mark.


# Implementation Example to run
```
```
  console.log(Number.MAX_SAFE_INTEGER);
  console.log(Number.MAX_SAFE_INTEGER + 1);
  console.log(Number.MAX_SAFE_INTEGER + 2);
  console.log((0.1 + 0.2) === 0.3);
  console.log(0.1 + 0.2);
  const json = '{"id":9007199254740993}';
  const parsed = JSON.parse(json);
  console.log(parsed.id);

  const price1 = 0.1;
  const price2 = 0.2;
  console.log(price1 + price2);
  
  const cents1 = 10;
  const cents2 = 20;
  console.log((cents1 + cents2) / 100);

## What to inspect:

MAX_SAFE_INTEGER + 1 and MAX_SAFE_INTEGER + 2 may collapse into the same value because integers beyond the safe range are not represented reliably.

0.1 + 0.2 gives a floating-point artifact instead of exact 0.3 because decimal fractions are approximated in binary floating point.

Large IDs in JSON are risky when parsed as JavaScript numbers, because the numeric value may already be rounded.

Money is safer as integer cents than as floating-point dollars.

# What-if attack
Take turns attacking the model with questions such as:

What if the backend sends database IDs as numbers larger than 2^53 - 1?

What if the checkout total uses floats for tax and discounts?

What if two different user IDs become equal after parsing in JavaScript?

What if a React key or cache key uses an unsafe numeric ID?

What if BigInt is used for IDs but the API still returns plain JSON numbers?

Push for practical decisions:

Should IDs be strings across the API boundary?

Should money be stored in cents?

Should tests include large integer edge cases?

Where exactly does rounding first appear?

# Repair the model
Build a corrected shared model:

## Rule 1: Not every decimal is exactly representable in binary floating point.

## Rule 2: JavaScript Number is fine for many values, but not for arbitrary-precision integers.

## Rule 3: IDs should often be strings if they may exceed the safe integer range.

## Rule 4: Currency values should usually be stored and computed in the smallest unit, such as cents.

## Rule 5: Good learning comes from recall, explanation, and spaced review, not just rereading notes.

