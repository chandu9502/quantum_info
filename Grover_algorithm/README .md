# Grover's Algorithm

## 1. What is Grover's Algorithm?

Grover's algorithm is a quantum algorithm for **unstructured search**.

* Classical search: $O(N)$
* Grover search: $O(\sqrt{N})$
* Speedup: **quadratic**

The main idea is **amplitude amplification**.

---

## 2. Basic Idea

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

---

## 3. Superposition

Start with:

$$
|0\rangle^{\otimes n}
$$

Apply Hadamard gates:

$$
H^{\otimes n}
$$

to create the equal-superposition state:

$$
|s\rangle =
\frac{1}{\sqrt{N}}
\sum_{x=0}^{N-1}|x\rangle
$$

For 2 qubits, $N=4$:

$$
|s\rangle =
\frac{1}{2}
\left(
|00\rangle+|01\rangle+|10\rangle+|11\rangle
\right)
$$

All states initially have equal probability.

---

## 4. Oracle

The oracle does **not** know the answer beforehand.

It only knows how to check whether a candidate is a solution.

The oracle is:

$$
O_f|x\rangle = (-1)^{f(x)}|x\rangle
$$


Therefore:

* Non-solution → unchanged
* Solution → phase flip

### Example

Suppose $|10\rangle$ is the solution.

Before the oracle:

$$
\frac{1}{2}
\left(
|00\rangle+|01\rangle+|10\rangle+|11\rangle
\right)
$$

After the oracle:

$$
\frac{1}{2}
\left(
|00\rangle+|01\rangle-|10\rangle+|11\rangle
\right)
$$

The solution gets a **phase flip**.

Its probability is still:

$$
|-0.5|^2 = 0.25
$$

So the oracle **marks the solution**, but does not yet amplify it.

---

## 5. Diffusion Operator

The diffusion operator amplifies the marked state's amplitude.

$$
D = 2|s\rangle\langle s| - I
$$

It performs **inversion about the mean**.

For an amplitude $a_i$:

$$
a_i' = 2\bar{a} - a_i
$$

where $\bar{a}$ is the average amplitude.

---

## 6. Why Is It Called Diffusion?

"Diffusion" does not mean physical diffusion.

It refers to **inversion about the mean**:

$$
a_i' = 2\bar{a}-a_i
$$

The amplitudes are reflected around their average value.

---

## 7. Mathematical Meaning of $|s\rangle\langle s|$

The expression:

$$
|s\rangle\langle s|
$$

is an **outer product** and represents a projection onto the equal-superposition state.




## 8. Why Does $|s\rangle\langle s|$ Relate to the Average?

For an arbitrary state:

$$
|\psi\rangle =
\sum_i a_i|i\rangle
$$

The average amplitude is:

$$
\bar{a} =
\frac{1}{N}\sum_i a_i
$$

The projection onto $|s\rangle$ is related to this average.

Therefore:

$$
D = 2|s\rangle\langle s|-I
$$

produces:

$$
a_i' = 2\bar{a}-a_i
$$

which is exactly **inversion about the mean**.

---

## 9. Diffusion Operator Implementation

The diffusion operator can be implemented as:

$$
D =
H^{\otimes n}
\left(
2|0\rangle\langle0|-I
\right)
H^{\otimes n}
$$

We know:

$$
|s\rangle =
H^{\otimes n}|0\rangle^{\otimes n}
$$






These are two mathematical descriptions of the **same diffusion operator**.

---

## 10. Circuit Order

The mathematical expression is read from **right to left**:

$$
D =
H^{\otimes n}
\left(
2|0\rangle\langle0|-I
\right)
H^{\otimes n}
$$

Conceptually:

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

### Step 1

Apply:

$$
H^{\otimes n}
$$

### Step 2

Apply:

$$
2|0\rangle\langle0|-I
$$

This keeps $|00...0\rangle$ unchanged and flips the phase of the other computational basis states.

### Step 3

Apply:

$$
H^{\otimes n}
$$

The complete operation performs inversion about the mean.

---

## 11. Oracle vs Diffusion

| Component     | Purpose                                   |
| ------------- | ----------------------------------------- |
| Superposition | Put all candidates into the quantum state |
| Oracle        | Mark the solution                         |
| Phase flip    | Give the solution a different phase       |
| Diffusion     | Amplify the marked solution               |
| Measurement   | Extract the answer                        |

### Oracle

Problem-specific:

$$
O_f|x\rangle = (-1)^{f(x)}|x\rangle
$$

It depends on the problem.

### Diffusion

Problem-independent:

$$
D = 2|s\rangle\langle s|-I
$$

It does not need to know which state is the solution.

---

## 12. Grover Iteration

One Grover iteration is:

$$
\boxed{
G = DO_f
}
$$

Therefore:

$$
\text{Oracle}
\rightarrow
\text{Diffusion}
$$

is repeated approximately:

$$
\boxed{
\frac{\pi}{4}\sqrt{N}
}
$$

times for one marked state.

Finally, measure the qubits.

---

## 13. Complete Algorithm

```text
1. Initialize n qubits to |0...0>

2. Apply H⊗n
       ↓
   Equal superposition

3. Apply Oracle
       ↓
   Solution gets phase flip

4. Apply Diffusion
       ↓
   Solution amplitude increases

5. Repeat Oracle + Diffusion
   approximately π/4 √N times

6. Measure
       ↓
   Solution
```

Mathematically:

$$
|0\rangle^{\otimes n}
\rightarrow
|s\rangle
\rightarrow
O_f|s\rangle
\rightarrow
DO_f|s\rangle
\rightarrow
(DO_f)^2|s\rangle
\rightarrow \cdots
$$

---

## 14. Key Intuition

**Oracle:**

> Mark the solution using phase.

**Diffusion:**

> Amplify the marked solution using interference.

Therefore:

$$
\boxed{
\text{Phase marking}
\rightarrow
\text{Inversion about mean}
\rightarrow
\text{Amplitude amplification}
}
$$

---

## 15. Complexity

Classical search:

$$
\boxed{O(N)}
$$

Grover search:

$$
\boxed{O(\sqrt{N})}
$$

Grover provides a **quadratic speedup** for unstructured search.
