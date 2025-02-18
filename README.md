<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

# Shor's Algorithm & Quantum Phase Estimation (QPE) Implementation

This repository documents the implementation of Shor’s algorithm using Qiskit. The project combines theoretical background and practical quantum circuit implementations for factorization and quantum phase estimation (QPE).

---

## Overview

The work is divided into the following main parts:

### 1. Mathematical Background and RSA

- **Factorization and RSA**: Factorization is key to RSA. An integer is expressed as:
  $$
  N = p_1^{\alpha_1} p_2^{\alpha_2} \cdots p_s^{\alpha_s}.
  $$

- **Euler's Theorem**: For an integer $$a$$ coprime with $$N$$, Euler’s theorem states:
  $$
  a^{\varphi(N)} \equiv 1 \pmod{N},
  $$
  where $$\varphi(N)$$ is Euler’s totient function.

- **Order of $$a$$ modulo $$N$$**: The order $$r$$ of $$a$$ modulo $$N$$ is defined as the smallest positive integer such that:
  $$
  a^r \equiv 1 \pmod{N}.
  $$
  This property is crucial for the factorization step in Shor’s algorithm.

---

### 2. Quantum Phase Estimation (QPE)

- **Purpose**: QPE is used to estimate the phase $$\theta$$ in the eigenvalue equation:
  $$
  U|\psi\rangle = e^{2\pi i\theta}|\psi\rangle.
  $$

- **Registers**:
  - A **precision register** initialized in a uniform superposition:
    $$
    \frac{1}{\sqrt{2^n}} \sum_{k=0}^{2^n-1} |k\rangle.
    $$
  - A second register containing the eigenstate $$|\psi\rangle$$ of $$U$$.

- **Process**:
  - Controlled versions of $$U^{2^j}$$ are applied to imprint phase information, producing:
    $$
    \frac{1}{2^{n/2}} \sum_{k=0}^{2^n-1} e^{2\pi i k \theta} |k\rangle.
    $$
  - An inverse Quantum Fourier Transform (QFT$$^\text{-1}$$) is applied to extract the approximated value of $$2^n\theta$$.

---

## Code Snippets

### Quantum Phase Estimation (QPE)

