# Grover's Algorithm

## 1. What is Grover's Algorithm?

Grover's algorithm is a quantum algorithm for **unstructured search**.

* Classical search: (O(N))
* Grover search: (O(\sqrt N))

It achieves a **quadratic speedup**.

---

## 2. Basic Idea

Grover works using:

```text
Superposition
     ↓
Oracle
     ↓
Diffusion
     ↓
Repeat
     ↓
Measure
```

The key idea is **amplitude amplification**.

---

## 3. Superposition

Start with:

[
|0\rangle^{\otimes n}
]

Apply Hadamard gates:

[
H^{\otimes n}
]

to create:

[
\boxed{
|s\rangle=
\frac{1}{\sqrt N}
\sum_{x=0}^{N-1}|x\rangle
}
]

For 2 qubits:

[
|s\rangle=
\frac12(
|00\rangle+|01\rangle+|10\rangle+|11\rangle)
]

All states initially have equal probability.

---

## 4. Oracle

The oracle **does not know the answer beforehand**.

It only knows how to check whether a candidate is a solution.

The oracle is:

[
\boxed{
O_f|x\rangle=(-1)^{f(x)}|x\rangle
}
]

where:

[
f(x)=
\begin{cases}
1 & \text{solution}\
0 & \text{not solution}
\end{cases}
]

Therefore:

* Non-solution → unchanged
* Solution → phase flip

Example:

[
\frac12(
|00\rangle+|01\rangle+|10\rangle+|11\rangle)
]

If (|10\rangle) is the solution:

[
\frac12(
|00\rangle+|01\rangle-|10\rangle+|11\rangle)
]

The oracle **marks the solution by phase**. It does not increase its probability.

---

## 5. Diffusion Operator

The diffusion operator amplifies the marked state's amplitude.

[
\boxed{
D=2|s\rangle\langle s|-I
}
]

It performs **inversion about the mean**.

For amplitudes (a_i):

[
\boxed{
a_i'=2\bar a-a_i
}
]

where (\bar a) is the average amplitude.

The negative amplitude created by the oracle gets amplified, while the other amplitudes decrease.

---

## 6. Diffusion Implementation

The same operator can be implemented as:

[
\boxed{
D=
H^{\otimes n}
(2|0\rangle\langle0|-I)
H^{\otimes n}
}
]

Why?

Because:

[
\boxed{
|s\rangle=H^{\otimes n}|0\rangle^{\otimes n}
}
]

Therefore:

[
|s\rangle\langle s|
===================

H^{\otimes n}
|0\rangle\langle0|
H^{\otimes n}
]

which gives:

[
D=
H^{\otimes n}
(2|0\rangle\langle0|-I)
H^{\otimes n}
]

### Circuit order

Read right-to-left:

```text
Input
  ↓
H⊗n
  ↓
2|0><0| - I
  ↓
H⊗n
  ↓
Output
```

The middle operation flips the phase of every computational basis state except (|00...0\rangle).

---

## 7. Grover Iteration

One Grover iteration is:

[
\boxed{
G=DO_f
}
]

Therefore:

[
\text{Oracle}
\rightarrow
\text{Diffusion}
]

is repeated approximately:

[
\boxed{
\frac{\pi}{4}\sqrt N
}
]

times.

Finally, measure the qubits.

---

## 8. Key Intuition

Remember:

> **Oracle = mark the solution using phase.**

> **Diffusion = amplify the marked solution using interference.**

So:

[
\boxed{
\text{Phase marking}
\rightarrow
\text{Inversion about mean}
\rightarrow
\text{Amplitude amplification}
}
]

---

## 9. Complexity

Classical:

[
\boxed{O(N)}
]

Grover:

[
\boxed{O(\sqrt N)}
]

This is a **quadratic speedup** for unstructured search.
