# RLAIF: A Bio-Inspired Cellular Architecture for Robot Learning

This repository contains the scientific formulation and conceptual framework for a novel, bio-inspired learning architecture for robotic control. The project proposes a complete Reinforcement Learning from AI Feedback (RLAIF) loop where a Vision-Language Model (VLM) acts as an external "teacher" to guide a distributed, cellular "brain."

The full research proposal is permanently archived on Zenodo: **[DOI will be generated here after publishing on Zenodo]**

## Project Overview & Architecture

The entire project, from its core concepts to the proposed algorithm, is outlined in the mind map below. This diagram serves as the central guide to all components of the research.

[![Project Mind Map](https://github.com/zorino96/VLM-Robot-Director/raw/main/Project_Mind_Map.png)](https://github.com/zorino96/VLM-Robot-Director/blob/main/Project_Mind_Map.png)

### Key Components:

*   **Core Concepts & Paradigm Shifts:** We introduce two main shifts: moving from programmed rewards to "understood" rewards provided by a VLM, and from monolithic neural networks to distributed, cellular architectures.
*   **Scientific Formulation ([FORMULA.md](FORMULA.md)):** This file contains the detailed mathematical equations that govern the proposed learning process, including the policy, the evaluation function, and the update rule.
*   **Algorithm ([ALGORITHM.md](ALGORITHM.md)):** This file provides a step-by-step pseudocode breakdown of the proposed training loop, demonstrating how the components interact.

## Experimental Validation

A proof-of-concept experiment was conducted based on this framework ("15 Minutes of Evolution"). In this test, a humanoid robot in a PyBullet simulation was tasked with learning to stand and balance. The system successfully demonstrated that the VLM could provide meaningful feedback, which was used to update the cellular brain's parameters. This validated the core principles of the proposed RLAIF loop. The implementation details are omitted to focus on the theoretical framework.

## Author

*   Zrng Mahdi Tahir

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
