# h's barn

> This is h's barn, a place where he raises and makes experiments with digital creatures.

Welcome to h's barn, a digital terrarium and research project dedicated to exploring the frontiers of artificial life, emergent complexity, and computational intelligence. We use 3D Cellular Automata (CA) as a substrate to grow, observe, and interact with complex digital "creatures." Our primary tool for analysis and simulation is the neural network, which we use not just to observe, but to learn the fundamental "physics" of these digital worlds.

## Current Status: Proof of Concept

The project has a working proof-of-concept script (`main.py`) that successfully implements a complex, multi-value 3D Cellular Automaton based on the **"Beehive Rule"** (`v3k6x1`) from Andrew Wuensche's research.

**Current Features:**
*   **Optimized 3D CA Engine:** A fast, vectorized implementation using Python, NumPy, and SciPy that simulates multi-state CAs with periodic boundary conditions.
*   **Live 3D Visualization:** A lightweight, real-time 3D renderer built with OpenCV that displays the CA grid and allows for smooth rotation, without the overhead of Matplotlib.
*   **2D Slice Analysis:** An observer window that shows the time-series history of a specific 2D cross-section of the 3D world.
*   **Evolving Statistics:** A dynamic dashboard plotting the Shannon entropy of the observed slice and the performance of our predictive neural network over time.
*   **Predictive Neural Network:** A 3D Convolutional Neural Network that is trained periodically on the simulation's history to predict the next state of the observed 2D slice.
*   **Balanced Dataset Training:** The NN training pipeline intelligently buffers simulation data and uses a balanced sampling strategy to avoid bias towards empty states, ensuring it learns to predict meaningful patterns.

**Results from a recent Beehive Rule simulation:**
```
--- Training NN at timestep 500 ---
Buffer size: 480. Training on 480 balanced samples.
(435 non-empty, 45 of 45 empty)
--- Best avg epoch loss: 0.0504 ---

--- Training NN at timestep 1000 ---
Buffer size: 980. Training on 980 balanced samples.
(886 non-empty, 94 of 94 empty)
--- Best avg epoch loss: 0.0058 ---

--- Training NN at timestep 1500 ---
Buffer size: 1480. Training on 1480 balanced samples.
(1338 non-empty, 142 of 142 empty)
--- Best avg epoch loss: 0.0010 ---

Simulation finished.
```
This demonstrates the core loop is functional: the simulation runs, data is collected, and the NN's predictive loss successfully decreases as it is exposed to more of the world's history.

## Core Concepts & The Grand Vision

The goal of h_barn is not just to simulate CAs, but to explore fundamental questions about learning, prediction, and intelligence. Our research is guided by several key experimental ideas.

### 1. The Divining Creature: A Council of Neural Networks

Our current NN predicts the future of a single 2D slice. This is our first "divining creature"—an entity that exists within the simulation's world and attempts to comprehend its local physics.

The next step is to scale this concept:
*   **A Full 3D Oracle:** We will train an independent neural network for *each* 2D slice of the grid. Together, this "council of NNs" will form a complete, parallel simulation of the 3D world. The challenge will be to ensure their predictions remain coherent and in sync.
*   **Modeling Interactions:** Can we train a higher-level network that observes the states of multiple, separate creatures and learns to predict their interactions, collisions, and emergent group behaviors? This moves from predicting physics to predicting ethology.

### 2. The Universal Predictor: Learning Physics Without Rules

Language models can predict text without explicit knowledge of grammar. Can we do the same for physics?

This experiment aims to train a single, robust neural network on a vast and varied dataset of *different* cellular automata.
*   **Rule Generation:** We will programmatically generate thousands of random CA rule sets.
*   **Agnostic Training:** The NN will be trained on sequences from all these different "universes" without being told which rule set is currently active.
*   **The Test:** Can the model learn to make accurate predictions in any given universe? Is it learning the underlying principles of local computation, or just memorizing patterns? This directly probes the limits of pattern recognition versus true rule inference.

### 3. Stability, Chaos, and Self-Correction

What happens when a model's prediction diverges from reality? This is a core question in chaos theory and numerical simulation.

*   **Divergence Analysis:** We will run the "true" CA simulation and our NN-based simulation in parallel from the same initial state. We will develop metrics to quantify exactly when and how their trajectories diverge.
*   **The Divergence Detector:** We will train a separate *classification model* whose only job is to look at the state of the two simulations and predict if a divergence event is about to happen.
*   **Self-Correction:** This detector can act as a trigger. When it fires, we can employ self-correction techniques, such as re-syncing the NN with the true state or training a specialized "corrector" model that learns to fix the errors that lead to instability.

## The Roadmap

Here is a plan for the evolution of the h_barn project.

### Phase 1: Foundational Upgrades
-   [ ] **Transition to Manim:** Replace the current OpenCV-based visualization with the Manim animation engine for high-quality, presentation-ready videos and plots.
-   [ ] **Code Refactoring:** Structure the project into distinct modules for CA engines, neural network models, visualization, and experiment management.

### Phase 2: The Divining Creature Experiments
-   [ ] Implement the "Council of NNs" architecture for full 3D prediction.
-   [ ] Develop synchronization mechanisms between the per-slice NNs.
-   [ ] Design experiments to model and predict the collision outcomes of two or more creatures.

### Phase 3: The Universal CA Predictor
-   [ ] Create a module for generating and managing a library of diverse CA rules.
-   [ ] Build a data pipeline to train a single NN on this heterogeneous dataset.
-   [ ] Evaluate the model's ability to generalize to unseen rules.

### Phase 4: Stability and Self-Correction
-   [ ] Implement the parallel simulation framework (True CA vs. NN CA).
-   [ ] Develop and track divergence metrics.
-   [ ] Train and integrate the "Divergence Detector" model.
-   [ ] Experiment with various self-correction strategies.

### Phase 5: The Meta-Experiment (Genetic Algorithms)
-   [ ] Integrate a genetic algorithm (GA) to *evolve* CA rules.
-   [ ] The fitness function will be guided by metrics that we want to maximize:
    *   **Pattern Repetition:** How ordered or life-like is the system?
    *   **Variability & Complexity:** How diverse are the generated patterns?
    *   **Resilience:** How well do creatures survive in harsh, pre-defined environments?
-   [ ] Use the GA to search the vast space of possible rules for novel forms of complex, self-organizing "life."

## Inspirations and Core Reading

This project stands on the shoulders of giants. A primary source of inspiration is the work done on Differentiable Self-organizing Systems, particularly:

> **[Growing Neural Cellular Automata](https://distill.pub/2020/growing-ca)**
> *Alexander Mordvintsev, Ettore Randazzo, Eyvind Niklasson, Michael Levin*
>
> This paper from Distill demonstrates how differentiable CAs, trained with gradient-based optimization, can "grow" complex patterns from a single seed and even learn to regenerate themselves after being damaged. Many concepts, like the "sample pool" training and the focus on regeneration, are directly applicable to h_barn.

## Technical Questions to Explore
-   **Numerical Precision:** How does the simulation's behavior and the NN's performance change when using different tensor precisions (e.g., 32-bit vs. 16-bit vs. 8-bit)? Can complex life persist with lower-precision physics?
-   **Chaos Theory:** How does the divergence between the true and predicted simulations relate to the Lyapunov exponent of the system? Can we characterize the "predictability horizon" for different CA rules?

## How to Run the Current Experiment

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/h_barn.git
    cd h_barn
    ```
2.  **Install dependencies:**
    ```bash
    pip install numpy torch opencv-python scipy
    ```
3.  **Run the script:**
    ```bash
    python main.py
    ```

