# Changelog

## 2026-06-03 - Interactive Flow Visualization Improvements

### Overview
Major enhancement to the LLM-D architecture visualizer to accurately represent the complete request/response flow across three serving modes: Disaggregated (Prefill/Decode), Unified (Single Pod), and Multi-Node Tensor Parallelism.

### Key Improvements

#### 1. Complete Bidirectional Request/Response Flows
- **Before**: Flows showed simplified one-way paths
- **After**: Every component interaction now has separate numbered arrows for request and response
- **Impact**: Users can now trace the complete journey of a request through the system and back

**Example (Disaggregated Mode):**
- Client → Gateway (①)
- Gateway → EPP (②)
- EPP → Gateway (③) ← *return path now visible*
- Gateway → Sidecar (④)
- Sidecar → Prefill (⑤)
- Prefill → Sidecar (⑥) ← *response path*
- ...continues through Decode, NIXL, and back to Client (14 total arrows)

#### 2. Consistent EPP Routing Across All Modes
- **Before**: Only disaggregated mode showed EPP
- **After**: All three modes route through EPP (Endpoint Picker)
- **Rationale**: EPP is fundamental to llm-d routing regardless of serving mode
- **Benefit**: Shows realistic architecture where EPP handles:
  - Load balancing across multiple pods
  - KV-cache affinity routing
  - Pod selection based on queue depth and latency

#### 3. Realistic Multi-Node Tensor Parallelism
- **Before**: Single Leader + 1 Worker (unrealistic for TP)
- **After**: 1 Leader + 3 Workers + "..." indicator (representing TP=8)
- **Shows**:
  - Leader broadcasts to all workers (parallel fan-out)
  - Workers compute model shards independently
  - Workers return results to Leader (parallel fan-in)
  - Leader aggregates via all_reduce
- **Flow**: 12 arrows demonstrating true distributed serving pattern

#### 4. Unified Mode Load Balancing
- **Before**: Single unified pod
- **After**: 2 replica unified vLLM pods
- **Purpose**: Demonstrates EPP selecting between multiple pod instances
- **Shows**: Real-world deployment pattern with horizontal scaling

#### 5. Visual Alignment and Layout Fixes
- Fixed InferencePool container height (510px → 380px)
- All components properly aligned on horizontal rows:
  - Row 1: Sidecar (y=485)
  - Row 2: Decode, NIXL, Prefill (y=575)
  - Row 3: KV Cache / Unified Pods / Leader (y=695)
  - Row 4: Workers (y=770)
- Consistent box sizing and spacing
- Components properly centered within containers

#### 6. Dynamic Component Visibility
- Components now show/hide based on active flow mode:
  - **Disaggregated**: Sidecar, Prefill, Decode, NIXL, KV Cache
  - **Unified**: 2 Unified vLLM replicas
  - **Multi-node**: Leader + multiple Workers
- Cleaner UI, reduces visual clutter

#### 7. Enhanced Tooltips and Metadata
- Updated tooltips for all components with accurate technical details
- Inspector panel shows complete metadata at each flow step:
  - Routing mode and pod selection
  - Tensor parallelism configuration
  - KV cache size and transfer details
  - Model shard assignments
- Flow step labels distinguish:
  - **Arrows** (numbered): ①, ②, ③...
  - **Processing** (unnumbered): "EPP selects pods", "Prefill processes prompt"

### Technical Details

**Files Modified:**
- `llmd-architecture.html` (432 insertions, 154 deletions)

**Flow Lengths:**
- Disaggregated: 14 arrows + 3 processing steps = 17 total steps
- Unified: 6 arrows + 2 processing steps = 8 total steps
- Multi-node: 12 arrows + 6 processing steps = 18 total steps

**Architecture Patterns Demonstrated:**
1. **Disaggregated Serving**: Cost-optimized separation of compute-intensive prefill (A100) and memory-intensive decode (L4/T4)
2. **KV Cache Transfer**: NIXL (NVIDIA Inference Xfer Library) for high-speed GPU-direct RDMA transfer
3. **Unified Serving**: Simpler deployment with single pod handling both phases
4. **Multi-Node TP**: Distributed tensor parallelism for models too large for single node (70B+)
5. **EPP Routing**: Smart routing based on queue depth, KV-cache affinity, and latency metrics

### User Experience Improvements
- Clearer visual flow representation
- Easier to understand request/response lifecycle
- Accurate representation of real-world deployment patterns
- Better alignment and visual balance across all modes
- Interactive tooltips provide technical depth on-demand

### Next Steps (Potential)
- Add animation speed controls (already implemented: 0.5x, 1x, 2x)
- Add more workers to multi-node view (show all 8?)
- Add control plane visualization (separate from data plane)
- Export flow diagrams as PNG/SVG
- Add performance metrics overlay (latency, throughput)

---

**Commit**: 2792bc7  
**Author**: alexagriffith + Claude Sonnet 4.5  
**Date**: 2026-06-03
