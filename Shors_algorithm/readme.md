# Shor's Algorithm

Shor's algorithm is a **quantum algorithm for integer factorization**. Its main idea is to convert the factoring problem into a **period-finding problem**.

## 1. Main Idea

Instead of directly finding the factors of (N):

[
\boxed{\text{Factoring} \rightarrow \text{Period Finding} \rightarrow \text{Factors}}
]

Choose a number (a) such that:

[
1<a<N
]

and:

[
\gcd(a,N)=1
]

Define:

[
f(x)=a^x\bmod N
]

The goal is to find the smallest (r) such that:

[
\boxed{a^r\equiv1\pmod N}
]

This (r) is called the **order** or **period**.

---

## 2. Example: Factor 15

Take:

[
N=15,\qquad a=2
]

Calculate:

```text
2^0 mod 15 = 1
2^1 mod 15 = 2
2^2 mod 15 = 4
2^3 mod 15 = 8
2^4 mod 15 = 1
```

So the sequence is:

[
1,2,4,8,1,2,4,8,\ldots
]

Therefore:

[
\boxed{r=4}
]

---

## 3. Get the Factors from the Period

Since (r=4) is even:

[
a^{r/2}=2^2=4
]

Calculate:

[
\gcd(4-1,15)=\gcd(3,15)=3
]

[
\gcd(4+1,15)=\gcd(5,15)=5
]

Therefore:

[
\boxed{15=3\times5}
]

The important formula is:

[
\boxed{\gcd(a^{r/2}\pm1,N)}
]

---

## 4. Where is the Quantum Part?

Finding the period (r) is the difficult part.

The quantum computer:

1. Creates a **superposition** of many (x) values.
2. Computes (a^x\bmod N) **coherently**.
3. Uses the **Quantum Fourier Transform (QFT)** to extract the periodic structure.
4. Measures the result.
5. Uses **continued fractions** classically to estimate (r).

### Simplified flow

```text
Choose a
   ↓
f(x) = a^x mod N
   ↓
Superposition
   ↓
Quantum modular exponentiation
   ↓
Periodic information
   ↓
QFT
   ↓
Measurement
   ↓
Continued Fractions
   ↓
Period r
   ↓
GCD
   ↓
Factors
```

---

## 5. Why QFT?

If:

[
f(x)=a^x\bmod N
]

is periodic, the QFT converts the **periodic structure into frequency information**.

[
\boxed{\text{Periodicity} \xrightarrow{\text{QFT}} \text{Frequency information}}
]

This allows us to estimate:

[
\frac{k}{r}
]

from which continued fractions can recover (r).

---

## 6. Connection to QPE

Shor's algorithm is closely related to **Quantum Phase Estimation (QPE)**.

QPE estimates a phase:

[
U|\psi\rangle=e^{2\pi i\theta}|\psi\rangle
]

In Shor, phase information is related to:

[
\frac{k}{r}
]

So you can remember:

[
\boxed{\text{Shor} \rightarrow \text{Order Finding} \rightarrow \text{QFT/QPE}}
]

---

## 7. Important Technical Terms

* **Modular arithmetic** — arithmetic using (\bmod N)
* **Order / Period (r)** — smallest (r) satisfying (a^r\equiv1\pmod N)
* **Superposition** — quantum state containing multiple basis states
* **Quantum interference** — amplitudes combine constructively/destructively
* **Modular exponentiation** — computing (a^x\bmod N)
* **QFT** — Quantum Fourier Transform
* **QPE** — Quantum Phase Estimation
* **Phase kickback** — phase information transferred to a control qubit
* **Continued fractions** — recover (k/r) approximation
* **GCD** — used to extract the factors
* **Order finding** — central quantum subroutine
* **RSA** — cryptosystem whose security relies on factoring being hard

---

## 8. Why Shor Matters for Cryptography

RSA uses:

[
N=pq
]

where factoring (N) is difficult for classical computers.

Shor can theoretically factor (N) efficiently on a sufficiently powerful **fault-tolerant quantum computer**.

Therefore:

[
\boxed{\text{Shor's Algorithm threatens RSA}}
]

This is one of the main reasons for developing **Post-Quantum Cryptography (PQC)**.

---


