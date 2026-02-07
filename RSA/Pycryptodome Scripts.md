## Install the necessary Python library
pip install pycryptodome

Filename: id_rsa.pub
Outputs: n and e  (Variables)
```
from Crypto.PublicKey import RSA

# Open the public key file and import it
with open("id_rsa.pub", "rb") as f:
    key = RSA.import_key(f.read())
    # Print the modulus (n) and the public exponent (e)
    print("n =", key.n)
    print("e =", key.e)
```

```
from gmpy2 import isqrt
from math import lcm

def factorize(n):
    if (n & 1) == 0:
        return (n/2, 2)

    a = isqrt(n)

    if a * a == n:
        return a, a

    while True:
        a = a + 1
        bsq = a * a - n
        b = isqrt(bsq)
        if b * b == bsq:
            break

    return a + b, a - b

print(factorize("Replace Here"))
```

```
from Crypto.PublicKey import RSA
from Crypto.Util.number import inverse

# Replace these with your actual values!
n = ...  # The modulus you found earlier
e = ...  # The public exponent (usually 65537)
p = ...  # The first prime factor you found
q = ...  # The second prime factor you found

# Calculate phi, which is a necessary step for finding 'd'
phi = (p - 1) * (q - 1)

# Calculate 'd', the modular multiplicative inverse of e mod phi
d = inverse(e, phi)

# Construct the full private key from all its components
key = RSA.construct((n, e, d, p, q))

# Save our shiny new private key to a file
with open("private_key.pem", "wb") as f:
    f.write(key.export_key("PEM"))

print("Private key 'private_key.pem' has been generated successfully!")
```
