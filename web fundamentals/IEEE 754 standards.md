# What is IEEE 754?

IEEE 754 is a 1985 standard that makes computer math with decimal numbers behave the same way on different computers.

# What does it do?

It defines how computers store and compute with floating‑point numbers so that things like 0.1 + 0.2 are handled using the same rules on every machine, even if the result is a tiny bit off from the ‘nice’ decimal we expect.

# How to represent IEEE 754 standards

the general pattern is:
1 - 1 sign bit (positive or negative)
2 - Some exponent bits (how big or small the number is) - 8 bit
3 - Some fraction/mantissa bits (the precise digits of the number) generally 23 bits

based on the computer architecture i.e 32 bits or 64 bits

1 - Single precision (float, 32 bits)
1 bit: sign
8 bits: exponent (with a bias)
23 bits: fraction (mantissa)

2 - Double precision (double, 64 bits)
1 bit: sign
11 bits: exponent
52 bits: fraction

* Single and Double Float are generally used by statically typed languages to derive meaning.

## Mathematically
value=(−1) ^sign × 1.fraction bits × 2^ exponent−bias

