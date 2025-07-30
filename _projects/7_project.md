---
layout: page
title: Matrix Multiplication Optimization
description: Optimizing GEMM performance across GPU and CPU architectures
img: assets/img/matrix-opt.jpg
importance: 1
category: work
---

This project focused on building and tuning high-performance matrix multiplication (GEMM) kernels for both NVIDIA GPUs (using CUDA) and ARM-based CPUs (using SVE intrinsics). The goal was to significantly improve over naive baselines, approach vendor-optimized libraries (cuBLAS, OpenBLAS), and understand the hardware/software co-design required for top GEMM speed.

---

## Techniques Used

#### CUDA Kernel — NVIDIA GPU

- **Shared Memory Tiling**: Reduces global memory calls by packing submatrices of A and B into shared memory tiles, minimizing redundant loads.  
- **Instruction & Thread-Level Parallelism**: Each thread computes multiple C entries (up to 25) via register blocking and unrolled loops for peak arithmetic throughput.  
- **Memory Coalescing**: All memory loads/stores are coordinated to maximize memory bandwidth and minimize transaction overhead.  
- **Dynamic Tile/Block Sizing**: Systematic parameter sweeps across tile/block sizes (including rectangles) to balance shared memory, register use, and occupancy.  
- **Careful Edge-Case Handling**: Padding and conditional logic on tile boundaries to avoid memory faults and keep all threads productive.  

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/cuda.png" title="CUDA" class="img-fluid rounded z-depth-1 w-50"%} <p class="text-center small">CUDA Optimized</p>
</div>

#### ARM SVE Optimization — ARM CPU

- **Packing Routines**: Transform row-major input blocks into cache- and SIMD-friendly layouts for fast vector loads/stores.  
- **4×4 SVE Microkernel**: Vectorized inner kernel using SVE intrinsics (`svld1_f64`, `svmla_f64_m`, `svst1_f64`). Predicate masks (`svbool_t`) prevent out-of-bounds errors.  
- **Loop Unrolling & Minimal Branching**: Maximizes register and instruction utilization while minimizing small-iteration overhead and branch costs.  
- **Cache-Aware Blocking**: Tuning of `Mc`, `Kc`, `Nc`, `Mr`, and `Nr` for high L1/L2 cache residency; best results with `Mc=128`, `Kc=32`, `Nc=128`, `Mr=4`, `Nr=4`.  
- **Automated Parameter Search**: A Python script batch-tested configurations to empirically determine best block sizes for each hardware platform.

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/cpu.png" title="CPU" class="img-fluid rounded z-depth-1 w-50"%} <p class="text-center small">CPU Optimized</p>
</div>

---

## 📝 Pseudocode

#### CUDA: Shared Memory + Register Tiling

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/cuda-code.png" class="img-fluid rounded z-depth-1 w-60"%}
</div>

#### ARM SVE

##### **Packing**

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/packing.png" class="img-fluid rounded z-depth-1 w-60"%}
</div>

This function packs matrix A by converting it from row-major to column-major order. The outer loop runs over rows (m ≤ Mr), and the inner loop over columns (k ≤ Kc). It stores columns of XA as rows in packA, effectively transposing the block for better memory access during computation.

##### **SVE Kernel**

First create a predicate to handle elements from 0 to n

svbool_t pg = svwhilelt_b64_u64(0, n);

Then check whether we are within the range of m (rows). If we are, then load that row of matrix C from memory. We do this four times because our matrix is 4x4.

c0 = (m > 0) ? svld1_f64(pg, c + 0 * ldc) : svdup_f64(0.0);

c1 = (m > 1) ? svld1_f64(pg, c + 1 * ldc) : svdup_f64(0.0);

c2 = (m > 2) ? svld1_f64(pg, c + 2 * ldc) : svdup_f64(0.0);

c3 = (m > 3) ? svld1_f64(pg, c + 3 * ldc) : svdup_f64(0.0);

Next, iterate over k (shared dimension) and load a sve vector from matrix b. This vector is protected by the predicate and multiples the current k with n to get the value in the vector.

svfloat64_t b0 = svld1_f64(pg, b + l * n);

Then, access the first value from matrix A, ensuring it’s in bounds, represented by (a + l *m) followed by a sve multiply-accumulate operation between the scalar from A (represented as a vector), and the vector B. Then update c0 with this value. To move on to the next scalar in A, we do *(currentVal + 1), etc.

double *currentVal = (a + l * m);

if(m>0) {
  
	aval = *currentVal;
	svfloat64_t ax = svdup_f64(aval);
	c0 = svmla_f64_m(pg, c0, b0, ax);

}

Finally, conditionally store the result in matrix C only for the valid rows

if (m > 0) svst1_f64(pg, c + 0 * ldc, c0);

---

## 🧪 Engineering Highlights

#### On GPU (CUDA)

- Optimal block size of **16×16** threads and tile size of **80×80** elements maximize occupancy.
- Rectangular tiles improved occupancy but required careful boundary handling.
- `#pragma unroll` enabled better FMA instruction pipeline utilization.
- Shared memory tiling and memory coalescing significantly reduce global memory latency.

<div style="text-align: center;">
  <img src="/assets/img/thread-blocks.png" alt="CUDA Block Size vs GFLOPS" style="max-width: 100%; height: auto;" />
  <p><em>Figure: CUDA Block Size vs GFLOPS</em></p>
</div>

---

#### On CPU (ARM SVE)

- Best cache blocking parameters: `Mc=128`, `Kc=32`, `Nc=128`.
- Vectorized microkernel doubled performance (from ~6 GFLOPS to ~19 GFLOPS).
- Predicate-based edge-case handling ensured correctness without branch penalties.
- Automated parameter tuning was essential to find the sweet spots.

<div class="text-center">
  <img src="/assets/img/sve_comparison.png" alt="SVE Packing vs Optimized Microkernel" class="img-fluid" style="max-width: 100%; height: auto;"/>
  <p class="small text-muted">Figure: CPU SVE performance comparison</p>
</div>

---

## 📊 Performance Summary

| Architecture & Kernel | Matrix Size (N) | Peak GFLOPS | Configuration           |
|----------------------|-----------------|-------------|-------------------------|
| ARM SVE (C7g.medium) | 256             | 18.6        | Mc=128, Kc=32, Nc=128   |
|                      | 512             | 19.345      | Mc=128, Kc=32, Nc=128   |
|                      | 1024            | 19.14       | Mc=128, Kc=32, Nc=128   |
|                      | 2048            | 18.6        | Mc=128, Kc=32, Nc=128   |
| **---**              | **---**         | **---**     | **---**                 |
| NVIDIA T4 (CUDA)     | 256             | 1121.2      | block=16×16, tile=80×80 |
|                      | 512             | 2253.0      | block=16×16, tile=80×80 |
|                      | 1024            | 3245.7      | block=16×16, tile=80×80 |
|                      | 2048            | 3535.6      | block=16×16, tile=80×80 |

---

## 🚀 Key Insights

- Optimal performance relies on balancing compute/blocking with memory hierarchy, not just making all parameters big.  
- Predicates & packing make SIMD kernels robust to edge cases on CPUs.  
- Systematic tuning (rather than hand-guessing) is crucial for non-trivial kernels across platforms.  
- Speedup: GPU achieved **>100×** over naive, and SVE CPU achieved **>3×** over packing-only.