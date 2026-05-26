---
tagline: "A decoupled, hybrid-cloud ML inference pipeline leveraging ephemeral GPU compute and secure reverse-tunneling."
role: "Lead Systems & ML Infrastructure Engineer"
status: "completed"
stack:
  - Python
  - Flask
  - PyTorch / Stable Diffusion
  - Jupyter / Google Colab
  - ngrok
  - HTML5 / CSS3
highlights:
  - "Architected a zero-cost, high-throughput ML inference pipeline bridging ephemeral cloud GPU environments with public-facing web clients."
  - "Designed a secure reverse-tunneling ingress layer using ngrok to bypass complex NAT/firewall constraints without exposing internal network topologies."
  - "Optimized PyTorch memory allocation on shared GPU runtimes, preventing Out-Of-Memory (OOM) crashes during concurrent image generation requests."
description: "A professional-grade demonstration of hybrid-cloud architecture, showcasing how to orchestrate, expose, and serve heavy deep learning models from ephemeral, sandboxed GPU environments to public web clients with minimal latency."
---

## 🌟 Architectural Vision & System Design

The system is designed around a **decoupled, hybrid-cloud execution model**. Instead of provisioning expensive, always-on cloud GPU instances (e.g., AWS EC2 g4dn/g5 instances), this architecture leverages ephemeral, high-performance compute nodes (Google Colab) as on-demand ML workers. 

The core architectural challenge of this approach is network ingress: sandboxed cloud runtimes do not permit inbound public traffic. To resolve this, the system implements a **reverse-tunneling ingress pattern**, establishing a secure outbound connection to an edge proxy (ngrok), which then routes public internet traffic back to the localized Flask application.

```
[ Public Client ] 
       │ (HTTPS Request)
       ▼
[ ngrok Edge Proxy ]
       │ (Secure Reverse Tunnel)
       ▼
[ Google Colab Sandbox (NAT/Firewall) ]
       │
       ├─► [ Flask Web Server (Routing & Payload Serialization) ]
       │
       └─► [ PyTorch / Stable Diffusion Pipeline (GPU Inference) ]
```

### Core Data & System Flow
*   **Ingestion / Input**: The client initiates an HTTP request containing generation parameters (prompts, steps, guidance scale) via a responsive frontend. This request hits the ngrok public edge URL.
*   **Ingestion Routing**: ngrok forwards the payload through the established secure tunnel, bypassing the Colab firewall, directly to the Flask application binding on `localhost`.
*   **Processing / Inference**: Flask parses the request and dispatches the parameters to the PyTorch execution thread. The model performs GPU-accelerated tensor operations on the CUDA device to generate the image.
*   **Persistence & Delivery**: To avoid disk I/O bottlenecks on ephemeral storage, the generated image tensor is serialized directly in-memory to