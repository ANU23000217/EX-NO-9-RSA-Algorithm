# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```
Developed By : ANU RADHA N
Regsiter No: 212223230018

def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

def mod_exp(base, exp, mod):
    result = 1
    base = base % mod
    while exp > 0:
        if exp % 2 == 1:
            result = (result * base) % mod
        exp = exp >> 1
        base = (base * base) % mod
    return result

def mod_inverse(e, phi_n):
    t, new_t = 0, 1
    r, new_r = phi_n, e

    while new_r != 0:
        quotient = r // new_r
        t, new_t = new_t, t - quotient * new_t
        r, new_r = new_r, r - quotient * new_r

    if r > 1:
        return -1  # No inverse
    if t < 0:
        t += phi_n
    return t

def rsa_simulation():
    print("\n***** Simulation of RSA Encryption and Decryption *****\n")

    # Get two prime numbers
    p = int(input("Enter a prime number (p): "))
    q = int(input("Enter another prime number (q): "))

    n = p * q
    phi_n = (p - 1) * (q - 1)

    while True:
        e = int(input(f"Enter a value for public key exponent (e) such that 1 < e < {phi_n}: "))
        if 1 < e < phi_n and gcd(e, phi_n) == 1:
            break
        print("Invalid 'e'. Try again.")

    d = mod_inverse(e, phi_n)
    if d == -1:
        print("Modular inverse does not exist for the given 'e'. Exiting.")
        return

    print(f"Public key: (n = {n}, e = {e})")
    print(f"Private key: (n = {n}, d = {d})")

    message = int(input("Enter the message to encrypt (as an integer): "))
    if message >= n:
        print(f"Message must be less than {n} (n). Exiting.")
        return

    encrypted = mod_exp(message, e, n)
    print(f"Encrypted message: {encrypted}")

    decrypted = mod_exp(encrypted, d, n)
    print(f"Decrypted message: {decrypted}")

rsa_simulation()

```



## Output:

![image](https://github.com/user-attachments/assets/c56782d4-95d2-4ef2-8ccf-b517b3669870)


## Result:
 The program is executed successfully.
