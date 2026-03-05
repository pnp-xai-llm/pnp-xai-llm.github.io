---
id: AHA-HeadCoverage
title: Head Coverage
order: 3
---


# Attention Head Coverage 

## 1. Introduction 

Transformer-based language models contain multiple attention heads in each layer, and these heads shape the model’s predictions through interactions between input tokens. However, it is difficult to directly observe from outside the model what specific function each individual head performs, or whether it is specialized for encoding certain types of knowledge or patterns. Understanding this internal structure is therefore a key challenge for improving the **interpretability** of Transformer models.

Previous interpretability studies have attempted to infer the functions of attention heads indirectly through attention weight visualization or probing classifiers. However, such approaches typically reveal **correlation** rather than demonstrating **causality**.

**Attention Head Coverage** proposes an experimental framework that quantitatively measures the **causal influence** of specific attention heads (or sets of heads) on the model’s **next-token prediction**. The framework intervenes directly in the model’s internal representations by replacing the hidden representation of a particular head with that from another input sample, and then observing how the output distribution changes.

The core assumption is as follows: 
> If a specific head plays a meaningful role in the model’s prediction process, replacing the representation of that head should cause the output to change in a consistent direction.

To interpret **what kind of information a head encodes**, we analyze **how much the output changes under intervention**, and infer the functional role of the head from these effects.

Furthermore, instead of relying on a single pair of prompts, we measure **statistical consistency across multiple prompts within the same category**. This allows us to distinguish accidental changes from structurally meaningful effects. The ultimate goal is to **automatically discover candidate attention heads that consistently influence predictions within a particular topic or prompt category.**

### Core Idea: Activation Patching via Head Slicing

The core mechanism of Attention Head Coverage is **activation patching**. Each experiment proceeds in three stages:

 1. **Baseline Measurement**

    Each prompt is fed into the model, and the **baseline top-1 token** of the next-token prediction along with its probability is recorded.

 2. **Intervention**

    The hidden representation of a specific layer/head (more precisely, the **head slice of the `attention.dense` input**) is **replaced** with the corresponding head slice from a donor prompt.

 3. **Effect Measurement**

    The change in output probabilities before and after the replacement is quantified in two directions:
       - decrease in the probability of the baseline top-1 token
       - increase in the probability of the donor prompt’s top-1 token
    
    These changes are measured to evaluate the influence of the head.

### Research Questions

This project aims to quantitatively answer the following three questions.

 - **Q1. Disruption** - When a specific head is patched, **to what extent does the baseline prompt’s top-1 prediction collapse?**
  
 - **Q2. Injection** - At the same time, **to what extent is the donor prompt’s top-1 prediction injected into the output?**

 - **Q3. Coverage** - **Is this phenomenon consistently reproduced across a large portion of the dataset within a specific category?**

<br>

## 2. Definition 

## 3. Experiments

## 4. Results