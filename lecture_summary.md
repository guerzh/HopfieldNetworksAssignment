# Hopfield Networks: Lecture Summary

*This written summary accompanies the [video lecture](https://youtu.be/mAL8Y4b5U1U).*

## Why Hopfield Networks?

In 2024, John Hopfield and Geoffrey Hinton were awarded the Nobel Prize in Physics for foundational work on neural networks. Hopfield Networks were the first successful attempt to model how networks can store and retrieve memories—an idea that led to Boltzmann Machines and, eventually, modern deep learning.

## The Problem: How Do We Store Memories?

Traditional computers store memories like a library: each piece of data has a specific address. But brains don't work this way. You don't look up "where did I store my friend's face?"—you just recognize them, even from a partial view or a blurry photo.

Hopfield Networks use **distributed representations**: memories are stored across all the connections in the network, not in specific locations. This means:
- You can retrieve memories from partial or corrupted inputs
- The network can store things that "look like" memories (useful for generation)
- Similar memories are stored "nearby" in the network

## How It Works

A Hopfield Network is a graph where:
- **Nodes** represent units that can be "on" (+1) or "off" (−1)
- **Edges** have weights representing connection strengths
- **Memories** are patterns (node configurations) that minimize the network's energy

### The Energy Function

For a 3-node network with weights $w_{01}$, $w_{02}$, $w_{12}$:

$$E = -(x_0 \cdot x_1 \cdot w_{01} + x_0 \cdot x_2 \cdot w_{02} + x_1 \cdot x_2 \cdot w_{12})$$

Where each $x_i \in \{-1, +1\}$.

**Key insight:** Memories are energy minima. When you give the network a partial input, it "rolls downhill" to the nearest minimum—the nearest stored memory.

### Example

With weights $w_{01}=2$, $w_{02}=-1$, $w_{12}=1$:

| $(x_0, x_1, x_2)$ | Energy |
|-------------------|--------|
| $(-1, -1, -1)$ | **−2** (minimum) |
| $(-1, -1, +1)$ | **−2** (minimum) |
| $(-1, +1, -1)$ | +4 |
| $(-1, +1, +1)$ | 0 |
| $(+1, -1, -1)$ | 0 |
| $(+1, -1, +1)$ | +4 |
| $(+1, +1, -1)$ | **−2** (minimum) |
| $(+1, +1, +1)$ | **−2** (minimum) |

The network "remembers" the four patterns with energy −2.

## Storing New Memories: Hebbian Learning

To store a new memory, we adjust weights using a simple rule:
- If $x_i \cdot x_j > 0$, **increase** $w_{ij}$ slightly
- If $x_i \cdot x_j < 0$, **decrease** $w_{ij}$ slightly

This creates a new energy minimum at the desired pattern without (hopefully) destroying existing memories. The classic phrase: "neurons that fire together, wire together."

## Retrieving Memories

Given a corrupted or partial input, find the nearest energy minimum. In our lab, we use exhaustive search (checking all $2^n$ combinations)—a great application of nested loops!

In practice, networks use stochastic algorithms, but exhaustive search is perfect for CS1.

## What Are Hopfield Networks Good For?

1. **Modeling memory:** A plausible model for how brains store associative memories

2. **Pattern completion:** Store faces, then retrieve the full face from partial input

3. **Generating similar patterns:** Find minima—they're either stored memories or "plausible" patterns

4. **Outlier detection:** If a new pattern has high energy, it doesn't match stored memories (possibly fake/anomalous)

## Connection to Modern AI

Hopfield Networks led to:
- **Boltzmann Machines** (Hinton): Added stochastic units for better learning
- **Restricted Boltzmann Machines**: Enabled deep belief networks
- **Modern deep learning**: The training techniques evolved from these foundations

The 2024 Nobel Prize recognized this foundational work.

## Key Takeaways

1. **Memories = Energy minima** in a weighted network
2. **Distributed representations** store patterns across all weights
3. **Hebbian learning** creates new minima incrementally
4. **Exhaustive search** finds all minima (great CS1 practice!)
5. **Nobel Prize-winning work** is accessible with just nested loops

---

*For the full lab assignment and code, see the [lab handout](lab_hopfield.pdf). For deeper context, watch the Nobel lectures by [John Hopfield](https://youtu.be/XDE9DjpcSdI) and [Geoffrey Hinton](https://youtu.be/8SffhDk4mdU).*
