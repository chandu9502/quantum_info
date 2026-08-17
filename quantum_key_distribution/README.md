# Quantum Key Distribution (QKD)

## What is QKD?

**Quantum Key Distribution (QKD)** is a method for securely distributing a **secret encryption key** between two parties using the principles of **quantum mechanics**.

QKD does not normally encrypt the actual message. Its main purpose is to **securely generate and distribute the key** that can later be used for encryption.

---

## Why is QKD Used?

The main problem in secure communication is:

> **How can Alice and Bob securely share a secret key when Eve may be listening?**

In classical cryptography, key exchange relies on mathematical problems such as:

* RSA
* Diffie-Hellman
* Elliptic Curve Cryptography (ECC)

A sufficiently powerful quantum computer could threaten many of these systems using **Shor's algorithm**.

QKD takes a different approach by using **quantum physics**.

---

## Basic QKD Setup

```text
                 Quantum Channel
        Photons ─────────────────────>

   Alice                                  Bob
    │                                      │
    │                                      │
    └──────── Classical Channel ───────────┘
                  ↑
                  │
                 Eve
          tries to intercept
```

Alice sends quantum states to Bob.

If Eve tries to measure the quantum states, her measurement can **disturb them**, introducing errors that Alice and Bob can detect.

---

## Key Quantum Principles

### 1. Measurement Disturbance

An unknown quantum state cannot generally be measured without potentially changing it.

Therefore, Eve cannot observe the quantum information without risking detection.

### 2. No-Cloning Theorem

An **unknown quantum state cannot be perfectly copied**.

Therefore, Eve cannot simply copy Alice's quantum states and forward identical copies to Bob.

```text
Alice → Quantum State → Eve → Bob
                         │
                         └── Cannot perfectly clone
```

---

# BB84 Protocol

**BB84** is one of the most famous QKD protocols.

It was proposed by **Bennett and Brassard in 1984**.

BB84 uses two different quantum bases:

### Rectilinear Basis

```text
|0⟩
|1⟩
```

### Diagonal Basis

```text
|+⟩ = (|0⟩ + |1⟩) / √2

|−⟩ = (|0⟩ − |1⟩) / √2
```

Alice randomly chooses:

1. A classical bit: `0` or `1`
2. A measurement basis

She then sends the corresponding quantum state to Bob.

Bob randomly chooses a basis for each received state.

---

## BB84 Process

```text
Alice
  │
  │ Random bit + random basis
  ↓
Quantum State
  │
  │
  ├──────────────→ Bob
  │
  │
  └── Eve may try to measure
```

After transmission:

1. Bob measures every photon using a randomly chosen basis.
2. Alice and Bob publicly compare their **bases**.
3. They discard measurements where their bases were different.
4. The remaining bits form the **sifted key**.
5. They compare a small portion of the key to estimate the **Quantum Bit Error Rate (QBER)**.
6. If the error rate is too high, they assume possible eavesdropping and discard the key.
7. Otherwise, they perform **error correction** and **privacy amplification**.

---

## Why Does Eve Get Detected?

Suppose Eve intercepts a photon.

She does not know which basis Alice used.

If Eve chooses the wrong basis, her measurement can change the quantum state.

Bob may then obtain an incorrect result.

This increases the **Quantum Bit Error Rate (QBER)**.

```text
Without Eve:

Alice → Quantum State → Bob
                         ↓
                    Low QBER


With Eve:

Alice → Quantum State → Eve → Bob
                         ↓
                    Disturbance
                         ↓
                    Higher QBER
```

If the error rate exceeds the acceptable security threshold, Alice and Bob reject the key.

---

# QKD Key Generation

The overall process can be summarized as:

```text
Quantum State Preparation
          ↓
Quantum Transmission
          ↓
Measurement
          ↓
Basis Comparison
          ↓
Sifting
          ↓
QBER Estimation
          ↓
Error Correction
          ↓
Privacy Amplification
          ↓
     Secret Key
```

The final key can then be used by a conventional encryption algorithm.

---

# QKD vs Classical Cryptography

| Classical Cryptography                             | QKD                                           |
| -------------------------------------------------- | --------------------------------------------- |
| Uses mathematical algorithms                       | Uses quantum mechanics                        |
| Key exchange can rely on computational assumptions | Security is based on quantum properties       |
| No-cloning is not involved                         | No-cloning theorem is important               |
| Does not require a quantum channel                 | Requires a quantum communication channel      |
| Can run on classical hardware                      | Requires specialized quantum/optical hardware |
| Examples: RSA, ECC, Diffie-Hellman                 | Example: BB84                                 |

---

# QKD and Quantum Computers

Quantum computers threaten some traditional public-key cryptosystems.

For example:

```text
Quantum Computer
       │
       ↓
Shor's Algorithm
       │
       ├── RSA
       ├── Diffie-Hellman
       └── ECC
```

This has motivated two major approaches:

```text
              Quantum Security
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
        PQC                   QKD
          │                   │
 Classical algorithms    Quantum communication
 resistant to quantum    for key distribution
 attacks
```

### Post-Quantum Cryptography (PQC)

Uses **classical computers** but cryptographic algorithms designed to resist quantum attacks.

### Quantum Key Distribution (QKD)

Uses **quantum communication** to establish secret keys.





