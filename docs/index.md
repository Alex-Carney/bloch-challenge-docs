<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

# PHYS 116 Report - Qublitz Challenge Mode

### Alex Carney, Prof. Whitfield, PHYS 116, Dartmouth College

#### Forward

This documentation serves as my report for PY116 final project. This report will be shorter than the traditional 
3-page standard report due to the additional work writing the code for additional Qublitz features. 

For this project, I am implemetning a prototype version of the "Bloch Sphere Challenge Mode", which is deployed online
and accessible here: [https://alex-carney.github.io/bloch-sphere-challenge/](https://alex-carney.github.io/bloch-sphere-challenge/). For developers who are interested, the GitHub
repository is here: [https://github.com/Alex-Carney/bloch-sphere-challenge](https://github.com/Alex-Carney/bloch-sphere-challenge).

**Note:** As of 4/28, for the draft report submission, the gate buttons are not working properly, more information in the 
main body of the report. These will be fixed for the final report. Feedback and advice is appreciated!

The link to the deployed version of Qublitz is here: [https://qublitz-qubit-lab.streamlit.app/](https://qublitz-qubit-lab.streamlit.app/), but this project focuses on challenge mode: 

### Introduction to Qublitz / Bloch Sphere Challenge Documentation

#### Background
Qublitz is a web-based educational tool developed in the FitzLab, aimed at facilitating the learning of basic quantum engineering concepts. This application allows users to interactively design qubit pulses—controlling parameters like intensity and duration—and observe the resulting effects on a qubit state through simulations represented on a Bloch sphere.

Originally designed to simulate a qubit environment without uncertainty, Qublitz is now advancing towards integrating real-time interactions with actual quantum hardware using the OpenPulse API and AWS BraKet. However, a recently awarded microgrant has shifted the project's immediate focus towards enhancing its educational and gamification aspects.

#### Transition to Challenge Mode
Following the receipt of a microgrant specifically aimed at enriching the educational experience through gamification, the Qublitz project team has decided to prioritize the development of a new feature called "Challenge Mode". This pivot is intended to make learning more engaging by introducing a game-like element to the application. Challenge Mode will challenge users to apply qubit gate pulses that move the system from the |0⟩ state to target states on the Bloch sphere, incorporating real-world considerations like T1 errors and dephasing time, which add complexity and realism to the simulations. 
Future additions will incorporate engineering microwave pulses, rather than gates, for additional complexity and realism. 

### Core Application Overview
At its core, Qublitz serves as a sophisticated Bloch sphere animation tool. It enables the visualization of quantum gates as animations that move the state vector across the sphere. Initially, this version of the application focuses solely on the basic operations without the integrated Challenge Mode, providing users with a foundational understanding of quantum mechanics through simple gate operations.

### Current Challenges and Development Focus
The development of Qublitz has encountered significant challenges, particularly in the realm of quaternion algebra. The accurate representation and animation of quantum gates, especially the Z gate, have proven problematic, with ongoing issues in achieving correct rotational behaviors. This has led to a pivotal decision point in the project's development:

#### Quaternion Algebra vs. Density Matrix Formalism
We are currently evaluating whether to continue utilizing quaternion algebra for representing all gates as pure rotations or to adopt a general density matrix formalism. In the latter approach, gates would be applied as matrix operations to a density matrix, with conversions to quaternions performed solely for animation purposes. This decision will significantly influence the mathematical accuracy and educational effectiveness of the simulations.

### Conclusion and Future Directions
As Qublitz continues to evolve, the primary goal remains to provide an interactive and educational platform that not only simulates quantum mechanics but also inspires and educates future quantum engineers. With the introduction of Challenge Mode and the potential integration with actual quantum hardware, Qublitz is poised to become an essential tool in quantum technology education, particularly for courses like ENGS 53: Introduction to Quantum Technologies.

This documentation serves as a preliminary guide to the current functionalities of Qublitz, outlining the ongoing challenges and the strategic decisions that lie ahead in its development. As we progress, updates and enhancements will be documented to keep users informed and engaged with the latest advancements in quantum education technology.