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

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// Function to check if a number is prime
int isPrime(int n) {
    if (n <= 1) return 0;
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0) return 0;
    }
    return 1;
}

// Function to calculate GCD
int gcd(int a, int b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}

// Function to calculate modular exponentiation
long long power(long long base, long long exp, long long mod) {
    long long res = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) res = (res * base) % mod;
        base = (base * base) % mod;
        exp /= 2;
    }
    return res;
}

// Function to calculate modular inverse
int modInverse(int a, int m) {
    for (int x = 1; x < m; x++) {
        if (((a % m) * (x % m)) % m == 1)
            return x;
    }
    return -1;
}

int main() {
    int p, q, e, message;

    // Get input primes
    printf("Enter first prime number (p): ");
    scanf("%d", &p);
    if (!isPrime(p)) {
        printf("Error: %d is not a prime number.\n", p);
        return 1;
    }

    printf("Enter second prime number (q): ");
    scanf("%d", &q);
    if (!isPrime(q)) {
        printf("Error: %d is not a prime number.\n", q);
        return 1;
    }

    int n = p * q;
    int phi = (p - 1) * (q - 1);

    // Get public exponent
    printf("Enter public exponent (e): ");
    scanf("%d", &e);

    if (gcd(e, phi) != 1) {
        printf("Error: e must be co-prime to phi (%d).\n", phi);
        return 1;
    }

    int d = modInverse(e, phi);
    if (d == -1) {
        printf("Error: No modular inverse exists for e = %d and phi = %d\n", e, phi);
        return 1;
    }

    // Get message to encrypt
    printf("Enter message to encrypt (as integer < %d): ", n);
    scanf("%d", &message);
    if (message >= n) {
        printf("Error: Message must be less than n (%d).\n", n);
        return 1;
    }

    // Print keys
    printf("\nPublic Key (e, n): (%d, %d)\n", e, n);
    printf("Private Key (d, n): (%d, %d)\n", d, n);

    // Encrypt
    long long cipher = power(message, e, n);
    printf("Encrypted Ciphertext: %lld\n", cipher);

    // Decrypt
    long long decrypted = power(cipher, d, n);
    printf("Decrypted Message: %lld\n", decrypted);

    return 0;
}


```



## Output:

![image](https://github.com/user-attachments/assets/c56782d4-95d2-4ef2-8ccf-b517b3669870)


## Result:
 The program is executed successfully.
