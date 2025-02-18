<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
# Shor's Algorithm & Quantum Phase Estimation Implementation

This repository documents a comprehensive lab project on implementing Shor’s algorithm using Qiskit. The project covers the theoretical background alongside detailed quantum circuit implementations for factorization and quantum phase estimation (QPE).

---

## Overview

The work is divided into the following main parts:

1. **Mathematical Background and RSA**  
   - Factorization is key to RSA. An integer is expressed as  
    $$N = p_1^{\alpha_1} p_2^{\alpha_2} \cdots p_s^{\alpha_s}$$
   - For an integer \(a\) coprime with \(N\), Euler’s theorem states that  
     $$a^{\varphi(N)} \equiv 1 \pmod{N}$$
     where $$\(\varphi(N)\)$$ is Euler’s totient function.
   - The *order* \(r\) of \(a\) modulo \(N\) is defined as the smallest positive integer such that  
     $$a^r \equiv 1 \pmod{N}$$
   This property is crucial for the factorization step in Shor’s algorithm.

2. **Quantum Phase Estimation (QPE)**  
   - QPE is used to estimate the phase \(\theta\) in the eigenvalue equation  
     $$U|\psi\rangle = e^{2\pi i\theta}|\psi\rangle$$
   - Two registers are employed:
     - A **precision register** (often called `eig`), initialized in a uniform superposition:
       $$\frac{1}{\sqrt{2^n}} \sum_{k=0}^{2^n-1} |k\rangle$$
     - A second register containing the eigenstate \(|\psi\rangle\) of \(U\).
   - Controlled versions of \(U^{2^j}\) are applied to imprint phase information, producing  
     
     $$\frac{1}{2^{n/2}} \sum_{k=0}^{2^n-1} e^{2\pi i k \theta} |k\rangle$$
     
   - An inverse Quantum Fourier Transform (QFT\(^\text{-1}\)) is applied to extract the approximated value of \(2^n\theta\).

3. **Quantum Circuit Implementations**
   - **Entangled States:** Circuits create states such as the GHZ state:
     $$\frac{1}{\sqrt{2}} \left( |000\rangle + |111\rangle \right)$$
     using Hadamard and CNOT gates.
   - **QPE Circuits:** Circuits implement the phase estimation with different precisions (3, 4, and 5 qubits). For example, when \(U\) has an eigenvalue \(e^{2\pi i \frac{6}{8}}\), the expected binary measurement approximates the phase.
   - **Superposition of Eigenstates:** Experiments also include cases where the initial state is a superposition of two eigenstates, demonstrating the inherent probabilistic nature of QPE.

4. **Modular Multiplication Oracle**
   - A key component of Shor’s algorithm is the oracle that performs modular multiplication. For inputs \(x < N\), the function is defined as:
     $$f(x) = \left(a^p \cdot x\right) \bmod N$$
     and for \(x \geq N\) the function acts as the identity.
   - The provided implementation constructs the corresponding unitary operator using Qiskit’s matrix tools.

5. **Shor’s Algorithm Integration**
   - The complete circuit integrates QPE and the modular multiplication oracle to deduce the order \( r \) (e.g., for \(a=7 \mod 30\) or \(a=20 \mod 29\)).
   - By analyzing the measurement distribution (each integer \(k\) on the precision register corresponds to a real fraction \(\frac{k}{2^n}\)), the periodicity—in turn, the order \(r\)—is inferred.

6. **Circuit Analysis & Complexity**
   - The project includes an analysis of the circuit complexity by counting the number of gates (e.g., `rx`, `ry`, `cx`).
   - Results indicate that the gate count grows exponentially with the number of qubits, emphasizing scalability challenges on current quantum hardware.

---

## Requirements

- Python 3.x
- Qiskit
- NumPy
- Matplotlib

You can install the required packages via pip:

```bash
pip install qiskit numpy matplotlib
