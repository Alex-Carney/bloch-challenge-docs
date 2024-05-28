<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

# PHYS 116 Final Report - Qublitz Challenge Mode

### Alex Carney, Prof. Whitfield, PHYS 116, Dartmouth College

#### Forward

This documentation serves as my report for PY116 final project. This report will be shorter than the traditional 
3-page standard report due to the additional work writing the code for additional Qublitz features. 

For this project, I implemented a "Bloch Sphere Playground" app, which is deployed online
and accessible here: [https://alex-carney.github.io/bloch-sphere-challenge/](https://alex-carney.github.io/bloch-sphere-challenge/). For developers who are interested, the GitHub
repository is here: [https://github.com/Alex-Carney/bloch-sphere-challenge](https://github.com/Alex-Carney/bloch-sphere-challenge).

The purpose of this app is to prototype certain features that will be integrated into the Qublitz app, which is a more sophisticated Bloch sphere animation tool. It enables the visualization of quantum gates as animations that move the state vector across the sphere. Initially, this version of the application focuses solely on the basic operations without the integrated Challenge Mode, providing users with a foundational understanding of quantum mechanics through simple gate operations.


The link to the deployed version of Qublitz is here: [https://qublitz-qubit-lab.streamlit.app/](https://qublitz-qubit-lab.streamlit.app/), but this focuses on Bloch sphere visualizations. 

### Introduction to Qublitz / Bloch Sphere Challenge Documentation

#### Background
Qublitz is a web-based educational tool developed in the FitzLab, aimed at facilitating the learning of basic quantum engineering concepts. This application allows users to interactively design qubit pulses—controlling parameters like intensity and duration—and observe the resulting effects on a qubit state through simulations represented on a Bloch sphere.

Originally designed to simulate a qubit environment without uncertainty, Qublitz is now advancing towards integrating real-time interactions with actual quantum hardware using the OpenPulse API and AWS BraKet. However, a recently awarded microgrant has shifted the project's immediate focus towards enhancing its educational and gamification aspects.

This report outlines the development and implementation of the Qublitz Challenge Mode, a web-based educational tool designed to aid in the understanding of quantum computing concepts through interactive simulations on the Bloch Sphere.

### List of Features

- Static Bloch Sphere Visualization
- [Basic Quantum Gates](#basic-quantum-gates) animating simple state vector rotations on the surface of the Bloch sphere (unitary gates)
- [Phase Gates](#phase-gates) animating simple state vector rotations on the surface of the Bloch sphere (unitary phase gates)
- [Challenge Mode](#challenge-mode) engaging users in applying quantum gates to achieve specific target states on the Bloch Sphere
- [Frame Changes](#frame-changes) allowing users to switch between the lab frame and rotating frame, with configurable drive frequency
- [Quantum Channels](#quantum-channels-and-their-mathematical-representation) Advanced topic, useful even at the graduate level. Implemented as superoperators with Kraus operators for amplitude damping, phase damping, depolarizing, phase flip, bit flip, and bit-phase flip channels. Shows the effect of each channel on the Bloch sphere, warping the state vector in real-time.
- T1 and T2 Process Animation: The T1 process is animated on the Bloch sphere, showing the relaxation of the qubit state over time. The T2 process is also animated, showing the dephasing of the qubit state over time, with configurable T1/T2 times

## Quantum Gates and Their Representations

### Basic Quantum Gates

- **X-Gate (Pauli-X, NOT gate)**  
  **Angle-Axis Representation**: \( \theta = \pi, \hat{n} = (1, 0, 0) \)
- **Y-Gate (Pauli-Y)**  
  **Angle-Axis Representation**: \( \theta = \pi, \hat{n} = (0, 1, 0) \)
- **Z-Gate (Pauli-Z)**  
  **Angle-Axis Representation**: \( \theta = \pi, \hat{n} = (0, 0, 1) \)
- **Hadamard Gate (H)**  
  **Angle-Axis Representation**: This gate rotates around the axis \(\hat{n} = (1, 0, 1)/\sqrt{2}\) by an angle of \(\pi\).

### Phase Gates

- **S-Gate**  
  **Angle-Axis Representation**: \( \theta = \pi/2, \hat{n} = (0, 0, 1) \)
- **T-Gate**  
  **Angle-Axis Representation**: \( \theta = \pi/4, \hat{n} = (0, 0, 1) \)
- **S^\dagger-Gate (S-dagger)**  
  **Angle-Axis Representation**: \( \theta = -\pi/2, \hat{n} = (0, 0, 1) \)
- **T^\dagger-Gate (T-dagger)**  
  **Angle-Axis Representation**: \( \theta = -\pi/4, \hat{n} = (0, 0, 1) \)

## Challenge Mode

Challenge Mode engages users in applying quantum gates to achieve specific target states on the Bloch Sphere, with three levels of difficulty:

- **Level 1**: Basic single gate applications.
- **Level 2**: Requires sequences of gates.
- **Level 3**: Advanced level including noise and the requirement to switch between frames for certain coins.

### Frame Changes

- **Lab Frame**: Here the qubit precesses at the drive frequency, $\omega_0$.
- **Rotating Frame**: In this frame, the frame rotates with the drive so that the qubit appears stationary unless acted upon by a pulse.

## Quantum Channels and Their Mathematical Representation

Quantum channels were implemented using the superoperator formalism, with the following Kraus operators for each channel:

### Amplitude Damping Channel
This channel models energy loss from a quantum system.

- \( E_0 = \begin{pmatrix} 1 & 0 \\ 0 & \sqrt{1 - \gamma} \end{pmatrix} \)
- \( E_1 = \begin{pmatrix} 0 & \sqrt{\gamma} \\ 0 & 0 \end{pmatrix} \)

On the Bloch sphere, this is represented as the vector transformation:

$$
(x, y, z) \to (x \sqrt{1 - \gamma}, y \sqrt{1 - \gamma}, z \sqrt{1 - \gamma} + \gamma)
$$

When $\gamma$ is replaced with a time-varying function like $\gamma(t) = 1 - e^{-t/T1}$, the channel represents energy relaxation,
or a "T1" process, which can be animated on the simulation for a given T1 time. 

### Phase Damping Channel
This channel describes loss of quantum information without loss of energy.

- \( E_0 = \begin{pmatrix} 1 & 0 \\ 0 & \sqrt{1 - \lambda} \end{pmatrix} \)
- \( E_1 = \begin{pmatrix} 0 & 0 \\ 0 & \sqrt{\lambda} \end{pmatrix} \)

On the Bloch sphere, this is represented as the vector transformation:

$$
(x, y, z) \to (x \sqrt{1 - \lambda}, y \sqrt{1 - \lambda}, z )
$$

When $\sqrt{1-\lambda}$ is replaced with a function of time, like $e^{-t/(2*T2)}$, the channel represents dephasing, or a "T2" process, which can be animated on the simulation for a given T2 time.

### Depolarizing Channel
This channel represents isotropic noise that affects all states equally.

- \( E_0 = \sqrt{1 - p} I \)
- \( E_1 = \sqrt{p/3} \sigma_x \)
- \( E_2 = \sqrt{p/3} \sigma_y \)
- \( E_3 = \sqrt{p/3} \sigma_z \)

Where \( \sigma_x, \sigma_y, \sigma_z \) are Pauli matrices and \( p \) represents the probability of each error type occurring.

### Phase Flip Channel (also known as Z-Channel)
This channel flips the phase of the quantum state.

- \( E_0 = \sqrt{p} I \)
- \( E_1 = \sqrt{1-p} \sigma_z \)

### Bit Flip Channel
This channel flips the state of a qubit from |0⟩ to |1⟩ and vice versa.

- \( E_0 = \sqrt{p} I \)
- \( E_1 = \sqrt{1-p} \sigma_x \)

### Bit-Phase Flip Channel
This channel combines the effects of both bit flip and phase flip.

- \( E_0 = \sqrt{p} I \)
- \( E_1 = \sqrt{1-p} \sigma_y \)

These Kraus operators define the effect of each channel on a qubit's state, providing a tool for simulating how environmental noise and other quantum errors might affect quantum information processing tasks.

## Challenges and Discoveries

Multiple challenges were encountered during the development of the Qublitz Challenge Mode, particularly in the behavior of quaternions in rotations. It was discovered that Bloch sphere gates can be realized with left-quaternion algebra but are anti-unitary, which affects the simulation fidelity. 
Without understanding the distinction between left and right Quaternion multiplication, the draft version of the application was implemented using this
completely different, anti-unitary algebra, which led to incorrect gate behavior.

For a deeper dive into quaternions and Bloch sphere transformations, refer to this paper: [Quaternion Algebra in Quantum Computing](https://arxiv.org/pdf/1411.4999).

## Conclusion

As Qublitz continues to evolve, the primary goal remains to provide an interactive and educational platform that not only simulates quantum mechanics but also inspires and educates future quantum engineers. With the introduction of Challenge Mode and the potential integration with actual quantum hardware, Qublitz is poised to become an essential tool in quantum technology education, particularly for courses like ENGS 53: Introduction to Quantum Technologies.

This documentation serves as a preliminary guide to the current functionalities of Qublitz, outlining the ongoing challenges and the strategic decisions that lie ahead in its development. As we progress, updates and enhancements will be documented to keep users informed and engaged with the latest advancements in quantum education technology.

## Additional Resources and Acknowledgments

- [IBM Quantum Experience](https://quantum-computing.ibm.com/)
- [Nielsen and Chuang: Quantum Computation and Quantum Information](http://www.cambridge.org/us/academic/subjects/physics/quantum-physics-quantum-information-and-quantum-computation/quantum-computation-and-quantum-information)

Special thanks to Prof. Whitfield and Dartmouth College for the guidance and support provided throughout this project.