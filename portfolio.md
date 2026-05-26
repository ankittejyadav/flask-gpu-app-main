---
tagline: "Architecting and deploying GPU-accelerated AI inference services with ephemeral cloud compute."
role: "Lead Full-Stack Engineer / Solo Developer"
status: "completed"
stack:
  - Python
  - Flask
  - Jupyter Notebook
  - Google Colab
  - ngrok
  - HTML/CSS
highlights:
  - "Architected a GPU-accelerated inference pipeline, leveraging Google Colab for cost-effective, high-performance model execution."
  - "Designed and implemented secure public exposure for an ephemeral cloud application using `ngrok` tunneling, ensuring HTTPS and controlled access."
  - "Developed a modular Flask application demonstrating decoupled compute and presentation layers for AI/ML model serving."
description: "This repository showcases the architectural design and engineering practices for deploying a web-based, GPU-accelerated application within an ephemeral cloud environment. It highlights strategies for leveraging free-tier cloud resources (Google Colab) for computationally intensive tasks, securely exposing internal services to the public internet via tunneling, and structuring a Python Flask application for AI/ML inference. The focus is on demonstrating robust system design, secure access patterns, and efficient resource utilization for rapid prototyping and proof-of-concept deployments."
---

## 🌟 Architectural Vision & System Design

This project implements a modular monolith architecture, where a Python Flask application serves as the primary web interface and orchestrator for GPU-accelerated machine learning inference. The core architectural decision was to leverage Google Colab as an ephemeral, GPU-enabled compute environment, decoupling the high-performance computational requirements from traditional web hosting infrastructure. This design choice prioritized rapid prototyping, cost-efficiency, and accessibility for demonstrating complex AI models.

Data flows from the client browser, through a secure `ngrok` tunnel, to the Flask application running within the Google Colab environment. The Flask application