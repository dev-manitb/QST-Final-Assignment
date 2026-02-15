# Quantum State Tomography (QST) with Machine Learning

## 📌 Project Overview
This project implements Quantum State Tomography (QST) using machine learning techniques to reconstruct quantum states from measurement data. The goal was to build a scalable, differentiable model capable of learning quantum state representations (density matrices) that maximize fidelity with respect to a target state.

## 🚀 Methodology
We approached the problem using a **Model-Based Optimization** strategy:
1.  **State Representation:** We parameterized the quantum state $\rho$ using a complex vector $\psi$ such that $\rho = |\psi\rangle\langle\psi|$ (for pure states) or using Cholesky decomposition $\rho = L L^\dagger$ (for mixed states) to ensure physical validity (positivity and normalization).
2.  **Optimization:** We used **PyTorch** to perform gradient-based optimization. The loss function was designed to minimize the distance between the predicted measurement probabilities and the observed data (simulating Maximum Likelihood Estimation).
3.  **Scalability:** We benchmarked the performance across varying qubit sizes ($N=2$ to $N=6$) to analyze the computational cost.

## 📊 Results and Scaling Analysis
The performance of the reconstruction was evaluated using **Fidelity** ($F$) and **Trace Distance** ($D$):

$$
F(\rho, \sigma) = \left( \text{Tr} \sqrt{\sqrt{\rho}\sigma\sqrt{\rho}} \right)^2
$$

### Key Findings:
* **High Fidelity:** For small systems ($N=2, 3$), the model consistently achieved fidelities $> 99\%$.
* **Scaling Limit:** As shown in the scalability experiments, the runtime scales exponentially with the number of qubits ($2^N$).
    * *See `results/scalability_plot.png` for the runtime vs. qubit graph.*
* **Ablation Study:** Increasing the training epochs initially improves fidelity rapidly, but performance plateaus after ~300 epochs, indicating diminishing returns for longer training runs.

## 🛠 Repository Structure
* `notebooks/`: Jupyter notebooks containing the step-by-step implementation (Assignments 1-5).
* `models/`: Saved model checkpoints (pickled dictionaries containing state vectors).
* `results/`: Generated plots (scalability, loss curves) and raw experiment data.
* `src/`: (Optional) Helper scripts for quantum operations.

## 🔮 Future Improvements
1.  **Adaptive Measurements:** Instead of random measurements, an adaptive scheme could select optimal measurement bases to reduce the data required.
2.  **Neural Network Parameterization:** Using a Neural Quantum State (NQS) or Restricted Boltzmann Machine (RBM) could help compress the state representation for $N > 10$ qubits.
3.  **Noise Robustness:** Future work should test the model against noisy hardware data (e.g., from IBM Quantum) rather than ideal simulations.

---
*Project completed as part of the Open Project Winter 2025.*
