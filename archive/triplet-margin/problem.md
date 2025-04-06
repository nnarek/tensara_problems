---
slug: "triplet-margin"
title: "Triplet Margin Loss"
difficulty: "MEDIUM"
author: "sarthak"
tags: ["loss-functions"]
parameters:
  - name: "anchor"
    type: "[VAR]"
    pointer: "true"
    const: "true"
  
  - name: "positive"
    type: "[VAR]"
    pointer: "true"
    const: "true"
    
  - name: "negative"
    type: "[VAR]"
    pointer: "true"
    const: "true"
    
  - name: "loss"
    type: "[VAR]"
    pointer: "true"
    const: "false"

  - name: "B"
    type: "size_t"
    pointer: "false"
    constant: "false"

  - name: "E"
    type: "size_t"
    pointer: "false"
    constant: "false"
    
  - name: "margin"
    type: "float"
    pointer: "false"
    constant: "false"
---

Implement Triplet Margin Loss:

$$
\text{Loss}(a, p, n) = \max(0, d(a, p) - d(a, n) + \text{margin})
$$

where:
- $a$ is the anchor embedding
- $p$ is the positive embedding (similar to anchor)
- $n$ is the negative embedding (dissimilar to anchor)
- $d(x, y)$ is the distance function between embeddings $x$ and $y$ (typically L2 distance)
- $\text{margin}$ is a parameter that enforces a minimum distance between the positive and negative pairs

## Input:
- Anchor tensor of shape $(\text{B}, \text{E})$
- Positive tensor of shape $(\text{B}, \text{E})$
- Negative tensor of shape $(\text{B}, \text{E})$
- Margin value (float)

## Output:
- Loss value (scalar)

## Notes:
- Use Euclidean distance (L2 norm) as the distance function between embeddings.
- The loss is calculated for each triplet in the batch, then averaged over the batch.
- A properly implemented triplet loss should ensure that $d(a, p) + \text{margin} < d(a, n)$ for all triplets after training.
- The default margin value is `1.0`, but the implementation should support arbitrary positive margin values.
