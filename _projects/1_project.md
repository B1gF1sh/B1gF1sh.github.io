---
layout: page
title:  SIMD Optimization Case Study
description: Row–column dot products computed in parallel lanes
img: assets/img/Matrix_Main.jpg
importance: 1
category: work
related_publications: false
display_categories: ["work", "Academic"]
---

A compact study of matrix multiplication in C++ with a focus on <strong>SIMD (AVX)</strong>.  
The page is visual-first and code-light; details are in the report.

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/naive.jpg" title="SIMD lanes" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/matrix_avx.jpg" title="32-byte regs • load → mul/acc → store" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/intel_die.jpg" title="CPU die (thumbnail)" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Left: dot products executed in parallel lanes. Middle: <strong>32-byte</strong> register pipeline. Right: compact die thumbnail.
</div>

---

## AVX Core

{% highlight cpp %}
void* MultiplyWorker(void* arg){
    ThreadData* data = (ThreadData*)arg;
    int start = data->start_row;
    int end   = data->end_row;

    for (int i = start; i < end; ++i) {
        for (int j = 0; j < N; ++j) {
            __m256 sum = _mm256_setzero_ps();

            int k = 0;

            for (; k + 7 < N; k += 8) {
                __m256 a = _mm256_loadu_ps(&A[i * N + k]);
                __m256 b = _mm256_loadu_ps(&B_T[j * N + k]);
                sum = _mm256_add_ps(sum, _mm256_mul_ps(a, b));
            }

            float temp[8];
            _mm256_storeu_ps(temp, sum);

            float total = 0.0f;
            for (int t = 0; t < 8; ++t) {
                total += temp[t];
            }

            for (; k < N; ++k) {
                total += A[i * N + k] * B_T[j * N + k];
            }
            C[i * N + j] = total;
        }
    }

    pthread_exit(nullptr);
    return nullptr;
}
{% endhighlight %}
---

## Build
```bash
g++-O2-mavx-pthread main.cpp-o program
