# Concepts / Glossary

## Domain-Inspired

**Domain-Inspired** refers to incorporating specific knowledge, characteristics, or principles from the application domain into the sharpness-aware minimization process.

## <mark style="background: #FFB86CA6;">Sharpness-Aware Minimization (SAM)</mark>

A method to improve generalization by minimizing not only the training loss but also the sharpness of the loss surface, which is a measure of how flat the minima are.[[#Problem Identification]]
1. **Loss Landscape Sharpness**:
    

    - The sharpness of the loss landscape is a measure of how quickly the loss changes in the neighborhood of a minimum. A sharper landscape means that small changes in parameters can result in large changes in the loss.
        
2. **Flat vs. Sharp Minima**:
    
    - Flat minima are regions in the loss landscape where the loss remai[[#Algorithm Description]]ns relatively low and stable over a broad range of parameter values. Conversely, sharp minima are narrow and sensitive to parameter changes.
        
    - Flat minima are often associated with better generalization performance because they indicate that the model's performance remains stable even when there is slight perturbation in the parameters.

## Domain Shifts

Domain Shifts refers to the scenario where there is a change or difference between the training and testing data distributions. Domain shift, also known as domain adaptation or transfer learning in some contexts, presents a significant challenge in ensuring that models generalize well.

# Summary of Key Points

## Problem Identification

The paper identifies that **Sharpness-Aware Minimization** (SAM) can have a detrimental impact on training when there are domain shifts, as it may lead to inconsistent convergence across different domains.
## Proposed Solution

The authors introduce Domain-Inspired Sharpness-Aware Minimization (DISAM), an algorithm that adjusts SAM's perturbations basedation process across domains.

## Algorithm Description

DISAM introduces <mark style="background: #FFB86CA6;">a variance minimization constraint on domain loss during sharpness estimation</mark>, allowing for adaptive gradient calibration based on each domain's optimization level.
## Theoretical Contributions

The paper provides theoretical analysis showing that DISAM can achieve faster overall convergence and improved generalization under inconsistent convergence scenarios.

## Empirical Results

Extensive experiments on domain generalization benchmarks demonstrate DISAM's superiority over state-of-the-art methods, including improved efficiency in parameter-efficient fine-tuning.


## Elastic Gradient Calibration

**elastic**: it implies a method that can dynamically adjust and adapt to different situations or data distributions.