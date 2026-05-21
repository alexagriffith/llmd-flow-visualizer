# LLM-D — Interactive Architecture Visualizer

![Kubernetes](https://img.shields.io/badge/kubernetes-native-326CE5?style=flat-square&logo=kubernetes)
![CNCF Sandbox](https://img.shields.io/badge/CNCF-Sandbox-blue?style=flat-square)
![License](https://img.shields.io/badge/license-Apache%202.0-blue?style=flat-square)

> **Interactive animated architecture flows for LLM-D distributed inference on Kubernetes**

This site visualizes how **llm-d** (CNCF Sandbox) enables Kubernetes-native distributed LLM inference.

## What is llm-d?

**llm-d** is a cloud-native distributed inference orchestration system for serving large language models in production on Kubernetes. It provides:

1. **llm-d Inference Scheduler (v0.7.1)** — GPU topology-aware pod placement
2. **llm-d Workload Variant Autoscaler (v0.6.0)** — Queue-based autoscaling for prefill/decode

llm-d integrates with:
- **KServe (v0.17.0)** — User-facing LLMInferenceService CRD
- **LeaderWorkerSet** — Kubernetes-native leader+worker pod orchestration (kubernetes-sigs)
- **vLLM (v0.18.0)** — High-performance inference engine with Ray distributed backend
- **Istio + Gateway API** — Service mesh and ingress routing

## Features

### Interactive Flows

- **Disaggregated Serving** — Prefill/decode split with KV cache reuse
- **Unified Serving** — Single-pod inference with tensor parallelism
- **Multi-Node Tensor Parallelism** — Leader+worker pods via LeaderWorkerSet

### Clickable Components

Click any component in the visualizer to see:
- Role and responsibilities
- Configuration details
- Integration with other components
- Version information

### Design Fidelity

Visual style matches the AI Gateway Flow Visualizers (RHAI 3.4 GA) with:
- GitHub-inspired dark mode
- Animated request flows
- Step-by-step inspector
- Clean, technical aesthetic

## Architecture

### Component Stack (RHAI on Kubernetes)

```
┌─────────────────────────────────────────────────────────┐
│ User API: LLMInferenceService CRD (KServe)              │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ Control Plane: KServe llmisvc-controller                 │
│ Translates to → LeaderWorkerSet + Service + HTTPRoute   │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ Orchestration:                                           │
│  - llm-d Inference Scheduler (GPU topology aware)       │
│  - llm-d Workload Variant Autoscaler (queue-based)      │
│  - LeaderWorkerSet Controller (leader+worker pods)      │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ Service Mesh: Istio + Gateway API (HTTPRoute)           │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ Runtime: vLLM (v0.18.0) with Ray distributed backend    │
└─────────────────────────────────────────────────────────┘
```

### Request Flow (Unified)

```
Client → Gateway → vLLM Leader Pod → (Ray) → Worker Pods → Aggregated Response
```

### Request Flow (Disaggregated)

```
Client → Gateway → llm-d Router → Prefill Pod → KV Cache Storage
                                                        ↓
                                                   Decode Pod → Response
```

## Local Development

This is a static HTML site with no build process:

```bash
# Option 1: Open directly
open index.html

# Option 2: Simple HTTP server
python3 -m http.server 8000

# Option 3: npm script
npm run dev
```

## Deployment

### Vercel (Recommended)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Deploy to production
vercel --prod
```

### GitHub Pages

1. Push to GitHub
2. Go to Settings → Pages
3. Select branch `main`
4. Site live at `https://your-username.github.io/repo-name`

See [DEPLOYMENT.md](DEPLOYMENT.md) for more options (Netlify, Cloudflare Pages).

## Project Structure

```
.
├── index.html                  # Landing page with cards
├── llmd-architecture.html      # Interactive flow visualizer
├── llmd-flow.html              # Original simple visualizer
├── README.md                   # This file
├── DEPLOYMENT.md               # Deployment guide
├── CONTRIBUTING.md             # Contribution guide
├── LICENSE                     # Apache 2.0
├── package.json                # npm scripts
└── vercel.json                 # Vercel config
```

## Related Projects

- **llm-d**: [https://github.com/llm-d](https://github.com/llm-d) (CNCF Sandbox)
- **KServe**: [https://kserve.github.io](https://kserve.github.io)
- **LeaderWorkerSet**: [https://lws.sigs.k8s.io](https://lws.sigs.k8s.io)
- **vLLM**: [https://docs.vllm.ai](https://docs.vllm.ai)
- **OpenDataHub**: [https://opendatahub.io](https://opendatahub.io)

## License

Apache 2.0

---

**Website:** This repo  
**Docs:** See [llm-d GitHub](https://github.com/llm-d)  
**RHAI**: Red Hat AI on Kubernetes (includes llm-d integration)
