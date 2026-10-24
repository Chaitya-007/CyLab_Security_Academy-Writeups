# MultiCode

**Problem:** A message is given which is just multiple layers of encoding. We have peel back the layers to get the flag.

**Solution:**

1. Whenever you have decode/encode challenges, the first thing to do is check out [CyberChef](https://gchq.github.io/CyberChef/). It has a ton of built-in encoding/decoding algorithms and is very easy to use.

**Somethings to remember:**

• **Base64**: Characters use A-Z, a-z, 0-9, +, /, and often end with = or == padding.

• **Hexadecimal**: String length is even and uses only characters 0-9 and a-f (or A-F).

• **URL Encoding**: Contains % followed by two hex digits  (e.g., %20, %3A)

• **ROT13**: Simple letter substitution cipher that shifts each letter by 13 positions in the alphabet.

1] Use From Base64

2] Use From Hex

3] Use URL Decode

4] Use ROT13

**Learned:**  How to recognize different encoding schemes and how to decode them. This is a common skill needed in CTFs and real-world scenarios where data may be obfuscated or encoded for various reasons.
