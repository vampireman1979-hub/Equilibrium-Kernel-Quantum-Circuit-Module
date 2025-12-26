Equilibrium Kernel + Quantum Circuit

1. Equilibrium Kernel

Temperature Models
Both subsystems relax exponentially toward an environmental baseline:

\[
T_A(\chi) = 300 + 20\,e^{-\chi/10^4}
\]
\[
T_B(\chi) = 300 - 15\,e^{-\chi/8\cdot10^3}
\]

Scaling Field
A smooth, bounded, non‑zero field:

\[
\Phi(\chi) = 1 + 0.1\,\tanh(\chi/10^4)
\]

Equilibrium Score
\[
Es(\chi) = \frac{TA(\chi) + T_B(\chi)}{2\,\Phi(\chi)}
\]

Includes:
- domain validation  
- numerical guard for \(\Phi(\chi)\approx 0\)

---

2. Angle Mapping

The equilibrium score is converted into a phase angle:

1. Extract fractional part:  
   \[
   f = E_s(\chi) \bmod 1
   \]
2. Map to \([0, 2\pi)\):  
   \[
   \theta(\chi) = f \cdot 2\pi
   \]

This ensures:
- boundedness  
- determinism  
- compatibility with quantum rotation gates  

---

3. Quantum Circuit Construction

If Qiskit is installed, the module builds a 3‑qubit GHZ‑like circuit:

- H on qubit 2  
- CX(2 → 0)  
- CX(2 → 1)  
- RZ(theta) on qubits 0 and 1  
- barrier() for clarity  

This circuit demonstrates how a classical scalar model can parameterize entangled quantum operations.

---

4. Example Usage

`python
from equilibriumkernel import equilibriumscore, anglefromequilibrium, buildequilibriumcircuit

chi = 60106.0
Es = equilibrium_score(chi)
theta = anglefromequilibrium(chi)

qc, thetaused = buildequilibrium_circuit(chi)
print(qc.draw(output="text"))
`

---

5. Dependencies
- Python 3.8+
- NumPy  
- Qiskit (optional, required for circuit construction)

---

6. Purpose
This module is intended for:

- hybrid classical–quantum modeling  
- parameterized circuit experiments  
- reproducible scalar‑to‑phase mapping  
- benchmarking and educational demonstrations  

It is not a quantum simulator; it is a deterministic preprocessing and parameterization tool.

