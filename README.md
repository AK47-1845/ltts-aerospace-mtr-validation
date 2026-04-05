# Aerospace MTR Validation Engine 🚀

This repository contains the validation architecture used to prove that synthetically generated aerospace data can perfectly mimic real-world flight test data. 

## The Core Problem
Aerospace engineering teams (like at L&T Technology Services) cannot safely generate enough edge-case flight data to train anomaly detection models. Generating synthetic data is easy; proving it is statistically indistinguishable from physical reality is the hardest problem in AI.

## The Gauntlet
This engine ran a **92-run testing gauntlet across 9 different AI model families**. 
We trained models exclusively on synthetic sensor readings and evaluated them against models trained on actual physical flight data.

## Results 🏆
**TSTR (Train on Synthetic, Test on Real) Composite F1 Score: 0.9965**

The engineering team could not statistically distinguish the synthetic data from physical reality. This repository contains the deterministic reconciliation logic that bridged the sim-to-real gap.

> "Validation has to be re-earned for every physical environment, not claimed once and reused."
