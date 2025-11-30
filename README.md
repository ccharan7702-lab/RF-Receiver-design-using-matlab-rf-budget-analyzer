Overview
This project implements a superheterodyne RF receiver model in MATLAB using RF Toolbox and the RF Budget Analyzer app. The design builds a cascade of RF blocks, evaluates cascaded gain, noise figure, and linearity, and exports the chain to RF Blockset for time‑domain simulation.​

Features
Multi‑stage RF receiver chain with LNA, RF bandpass filters, down‑converting mixer, IF filter, IF amplifier, and output stage/power detector.​

RF budget analysis for stage‑wise and overall gain, noise figure, SNR, and IP3/OIP3.​

Export of the RF budget object to a Simulink/RF Blockset testbench for behavioral simulation and verification.​

MATLAB scripts to generate plots of cascaded gain, NF, and output power along the receiver chain.​

System Description
The receiver is targeted for an RF center frequency around 2.45 GHz with a given signal bandwidth and sensitivity at the antenna input. System‑level specifications are split across the LNA, RF filters, mixer, and IF stages so that the final chain meets required SNR, noise figure, and linearity margins.​
RF Budget Analyzer is used to adjust gains, NFs, and intercept points of individual elements until the overall performance satisfies the design constraints.​

MATLAB Code Explanation
The main MATLAB script first creates an array called elements in which each entry is an RF block such as an amplifier, RF filter, or modulator (mixer). Each block is defined with parameters like Gain, NF, OIP3, Fcenter, Bwpas (bandwidth), FilterType, FilterOrder, and local oscillator frequency for the down‑converter, matching the RF Budget Analyzer configuration.​
These elements are then passed into an rfbudget (or similar RF chain) object called, for example, superhet, together with the input frequency, input power, and signal bandwidth. After constructing the budget object, commands such as rfplot(superhet,'GainT'), rfplot(superhet,'NF'), view(superhet), and show(superhet) are used to visualize cascaded gain, noise figure, and stage‑wise results in plots and tabular views directly from MATLAB.​

Project Structure
theoretical calculation and explaination.m – Hand calculations for link budget, required gain distribution, and theoretical NF/IP3 of the cascade.​

code.m / rf.m / source code.m – Main MATLAB script creating the elements array, building the RF budget object, plotting gain/NF, and displaying the chain configuration.​​
cascade out.png, gain out.png, noise figure out.png, power out.png, rf testbench out.png, simulink out.png – Image files containing plots and screenshots of cascaded gain, noise figure, output power, RF testbench, and Simulink model results exported from MATLAB/RF Budget Analyzer.​

Other *.png / *.jpg – Additional screenshots of MATLAB code, RF Budget Analyzer windows, and simulation waveforms used for documentation.
project usage
This project not only models a generic RF receiver but was also used at the National Atmospheric Research Laboratory (NARL) to visualize real‑time signals from an operational receiver chain. At NARL, the MATLAB model helped validate the hardware front end and provided an interactive environment to observe how live atmospheric or satellite signals propagate through each RF stage.​

NARL real‑time application
At NARL, the receiver outputs (from LNA to IF/baseband) were connected to data‑acquisition hardware and streamed into MATLAB/Simulink, where the same RF chain structure as this project was implemented. This allowed engineers to compare measured gain, noise figure, and spectrum at each stage with the predictions from the RF Budget Analyzer model, making it easier to debug mismatches and tune hardware parameters.​
Real‑time scopes, spectrum analyzers, and signal‑logging tools in MATLAB/Simulink were used to visualize time‑domain waveforms, power levels, and spectral content, enabling continuous monitoring of receiver performance during experiments.​

Role of this project at NARL
This repository served as the core reference model for the NARL setup: the same element gains, NFs, and IP3 values were used as targets when configuring and testing the physical receiver. By running the scripts and RF Budget Analyzer configuration in parallel with measurements, the team could quickly check whether the live system met design specifications for sensitivity, dynamic range, and linearity.
The project also provided a teaching and documentation resource for interns and researchers at NARL, demonstrating how to go from theoretical link‑budget calculations to a full MATLAB implementation, and then to real‑time visualization of scientific RF signals.

