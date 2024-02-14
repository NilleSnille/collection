# Probabilistic Generative Models

This repository is dedicated to exploring Probabilistic Generative Models. It includes focused studies on Variational Auto Encoders (VAEs), Restricted Boltzmann Machines (RBMs), and Real-Valued Non-Volume Preserving (Real NVP) Flow models. Each model category has its dedicated folder containing a simple but explanatory implementation and a theoretical justification of the methodologies used. Each implementation and training is low on compute and can thus be a good starting point to explore these methods more.

## Directory Structure

- **[Variational Auto Encoder](Variational%20Auto%20Encoder)**: VAE with implementations that highlight their unique approach to generating new data instances similar to the input data - here we shoq how new images can be generated according to a given underlying generating distribution.
- **[Restricted Boltzmann Machines](Restricted%20Boltzmann%20Machines)**: Explore RBMs through simple implementations that showcase their ability to learn a probability distribution over the input set, showecased on an example where a gaussian mixture model is not satisfactoy.
- **[Real Valued Non Volume Preserving (Real NVP) Flow models](Non%20Volume%20Preserving%20Flows)**: Understand Real NVP models with examples demonstrating their capacity for detailed, complex data distribution modeling. This also showcases these models fundamental differences from VAEs and RBMs, and their much simpler implementation.

## Purpose

The goal of this repository is to provide an accessible entry point for those interested in generative modeling, and to showcase some small projects in the area.
