---
name: AI-Powered Ping Pong Agent
tools: [PyTorch, Pygame]
image: ../images/ping_pong_demo.png
description: An autonomous agent trained to play Ping Pong using a Multi-Layer Perceptron (MLP) built with PyTorch and a Pygame physics engine.
---

# AI-Powered Ping Pong Agent

## Detail

| ------------- |:-------------:|
| Project       | AI-Powered Ping Pong Agent |
| Duration      | Jan. 2025  |
| Tech Stack    | Python, PyTorch, Pygame |

<center>
<video width="70%" height="500px" controls>
  <source src="https://github-production-user-asset-6210df.s3.amazonaws.com/53821314/411587273-0bb71b69-ac31-40e5-8b74-7d320a14ba19.mp4?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260104%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260104T130545Z&X-Amz-Expires=300&X-Amz-Signature=6e41dbbd36a1d876f4ecc352f700cd6d913c607f13901488cba0ed0690a42c70&X-Amz-SignedHeaders=host" type="video/mp4">
Your browser does not support the video tag.
</video>
</center>

## Introduction

This project explores the intersection of **Game Development** and **Machine Learning**. Instead of using hard-coded heuristics, I engineered an intelligent agent capable of predicting the ball's trajectory using a **Multi-Layer Perceptron (MLP)**.

Using **Pygame**, I built a custom physics engine to simulate collision detection and velocity vectors. This environment feeds real-time state data—such as ball position and velocity—into a custom **PyTorch** model (`SimpleNN`). The model processes these inputs through a series of fully connected layers to output a precise paddle decision.

<a href="https://github.com/jay1224-jay/Self_Driving_Car_with_Raspberry_pi" target="_blank">View source code on Github</a>

## Challenges

* **Training Stability**

    Early iterations of the model suffered from slow convergence, where the agent struggled to learn stable strategies.
    - **Solution:** 
    
        I optimized the network architecture by integrating **Batch Normalization** (`nn.BatchNorm1d`) between the linear layers. This normalized the inputs to each layer, stabilizing the gradient flow and significantly accelerating the training speed.

* **Network Topology Design**

    Designing a network that was complex enough to learn physics but efficient for real-time inference.
    - **Solution:** 
    
        I designed a **Multi-Layer Perceptron (MLP)** with a "bottleneck" architecture.  The network starts with a high dimensional hidden state (`hidden_size`) and reduces dimensions by half in each subsequent layer (`/2`, then `/4`). This dimensionality reduction forces the model to distill the most essential features of the ball's movement using **ReLU** activation functions for non-linearity.

* **State Vector Representation**
    
    Determining exactly what data the AI needed to "see" to play effectively.
    - **Solution:** 
    
        I condensed the game state into a **4-dimensional input vector** (Ball X, Ball Y, Velocity X, Velocity Y). This minimal input size reduced computational overhead while providing just enough information for the linear layers to calculate the interception point.