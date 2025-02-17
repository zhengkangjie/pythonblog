# **Python Scientific Computing & Acceleration: A Brief Introduction**

## Why I Want to Write This Blog Post

The reason I wanted to write this blog post is because, during the process of helping my girlfriend write a Python script for scientific computing, I had many insights and realizations, and accumulated some simple experiences. I thought it would be helpful to write a brief guide for beginners who want to use Python for scientific computing tasks. However, at the beginning of the article, I would like to clarify that this post is aimed at beginners who are just starting with Python for scientific computing. Also, since I am not specialized in scientific computing (my background is in NLP, and I use Python quite a bit, but my experience in scientific computing is not extensive), if there are any inaccuracies or issues in this article, feel free to point them out or help supplement them. Additionally, since my background is in computer science, this article may provide an introduction to Python's application in scientific computing from the perspective of a CSer. Furthermore, since different scientific computing tasks vary greatly, this article may not be suitable for all types of scientific computing needs. So, before diving in, please make sure that this guide is right for you. Now, let's get started.

## Why Choose Python?

As the saying goes, "To do a good job, one must first sharpen their tools." Since we are doing scientific computing, choosing the right language and platform is crucial. So, what are the advantages and disadvantages of Python compared to other commonly used scientific computing languages?

### Comparison with MATLAB:

**Advantages of MATLAB:**

- MATLAB is widely used in many engineering fields, so if you are working in a domain that already has a lot of mature open-source MATLAB code, it may be easiest to use MATLAB to minimize migration costs.
- MATLAB is great for numerical computations, with various well-encapsulated functions like `solve`, `plot`, etc., making it very convenient!
- The various toolboxes in MATLAB are excellent, and many engineering computing tasks can be accomplished through these toolboxes. This is one of MATLAB's biggest strengths.
- MATLAB is more beginner-friendly as it requires minimal setup, and the help documentation is comprehensive. The Parallel Computing Toolbox is also easy to use; a small modification (e.g., changing `for` to `parfor`) can achieve parallel acceleration.

**Disadvantages of MATLAB:**

- MATLAB is paid software, and many toolboxes are also behind paywalls.
- The community around MATLAB is not as active as Python's. Python's various related packages and open-source code are rapidly developing and maturing.
- MATLAB’s Parallel Computing Toolbox offers a more limited set of acceleration methods compared to Python, which can provide more granular and diverse performance optimization options.
- MATLAB consumes significant resources, taking up considerable space on your hard drive and taking longer to load each time.

### Comparison with C++:

**Advantages of C++:**

- C++ is a classic language that is much closer to the system's core compared to Python and MATLAB. This makes it easier to perform low-level optimizations (such as improving cache coherence).
- C++ has zero additional runtime overhead, so if the code is written well, the performance can be extremely fast.
- C++ supports various abstraction methods (e.g., OOP, template metaprogramming), so if you enjoy writing abstract code, you may find it very satisfying.

**Disadvantages of C++:**

- The syntax is complex and has a steep learning curve, making it unfriendly for beginners (unless you're using it as "C with classes").
- Memory management is manual, which can lead to memory leaks and other bugs. This is one of the most criticized aspects of C++.
- Environment setup is complicated, and portability is poor. For instance, on Linux, you often have to manually compile many packages, and when switching to a new machine, you may need to reconfigure everything, adding extra time costs.
- Unlike Python and MATLAB, C++ doesn’t have as many readily available, mature, and easy-to-use packages (for example, plotting can be cumbersome).

### Comparison with Fortran:

Apologies, as I am a CSer, I am not very familiar with Fortran. However, I understand that Fortran is an older language, and most people using it likely do so due to historical reasons. Therefore, I don’t see the need to compare it further. If you do need to use Fortran, I doubt you would be looking at this beginner’s guide.

### Final Summary of Python’s Advantages:

- Python has a simple syntax, a low learning curve, and high development efficiency (especially for non-CS majors, as it shares similarities with MATLAB and is a scripting language).
- Python has a mature package management system and offers a variety of easy-to-use and excellent packages, which makes it very convenient and reduces development time.
- Python supports JIT acceleration, parallel processing, GPU acceleration, and other technologies, making it the go-to choice if you need performance optimization in those areas.
- Python is free and cross-platform. Once you develop something on Windows or macOS, it’s very easy to migrate it to Linux or other environments by using `conda env` to replicate the environment.
- Python is widely used by developers and is suitable for creating various applications (e.g., deep learning models, web backends, GUI programs, web scraping, etc.). Once you learn Python, you can even explore coding challenges like LeetCode or transition to other coding domains.

By now, I believe you have an idea of which language might be the most suitable for your needs. To summarize briefly: if you don’t have a strong need for GPU acceleration or large-scale parallelism, both MATLAB and Python will be sufficient for most tasks. If your field has specific MATLAB toolboxes or open-source code, then MATLAB is the way to go. However, if you want to significantly speed up your programs, Python or C++ are recommended (Fortran is also said to be efficient, but I am not familiar with it — feel free to share your experiences if you know more).

### Summary:

- **Ease of Use**: Python ≈ MATLAB > C++ (The syntax complexity of MATLAB and Python is similar, and using Anaconda to set up Python is as easy as installing MATLAB).
- **Theoretical Maximum Speed and Flexibility**: C++ > Python > MATLAB (However, achieving optimal acceleration in C++ can be tricky, and MATLAB doesn’t support CUDA JIT or other GPU acceleration operations).
- **Richness and Usability of Packages**: Python > MATLAB > C++.
- **Availability and Readability of Documentation**: MATLAB > Python > C++ (Python’s documentation is rich but lacks as much in Chinese).

## Useful Python Packages for Scientific Computing

### NumPy

The reason I put NumPy first is because it’s used in almost every scientific computing program. NumPy supports various matrix operations and numerical algorithms (e.g., linear algebra, FFT, etc.), and its usage is very similar to MATLAB. Many of its function names and usage patterns are the same, so if you're familiar with MATLAB, learning NumPy will be very easy. The NumPy website even offers a comparison with MATLAB, which is very friendly for beginners.

### SciPy

SciPy is a scientific computing package often used alongside NumPy. It provides more advanced algorithms, such as signal processing and optimization algorithms. More importantly, its `scipy.io.loadmat` and `scipy.io.savemat` APIs allow easy reading and writing of MATLAB `.mat` files, making it simple to integrate your Python program with existing MATLAB code and exchange data between them.

### Matplotlib

Matplotlib is one of the most important and commonly used packages for data visualization in Python. Its usage is similar to MATLAB’s `plot` function, and it can serve as a replacement for MATLAB’s plotting functionality to some extent.

### CuPy

CuPy is a package that supports GPU acceleration for NumPy. Its API is almost identical to NumPy’s, so if you have a high-performance NVIDIA GPU, you can easily replace NumPy with CuPy to achieve significant acceleration, especially for compute-intensive tasks. The speedup can be hundreds of times faster.

### Numba

Numba is another popular and easy-to-use package for high-performance numerical computation. Its core feature is JIT (Just-In-Time) compilation, a common acceleration method for interpreted languages like Python. Using it is simple — just add `@numba.jit` to the function you want to speed up. You can even enable parallel acceleration on CPUs by using `@numba.jit(nopython=True, parallel=True)`, which can bring the performance close to C++ code. Numba also supports `@vectorize` to enable vectorized computation, making it easier to process large datasets.

### Jax

Jax is a package developed by Google for accelerating deep learning computations, but it is also useful for other scientific computing tasks. Jax provides a `jax.numpy` module, which can replace NumPy and supports GPU acceleration. It also has `jax.scipy`, which is more efficient than SciPy in many cases. Jax supports automatic differentiation, JIT acceleration, and vmap serialization, which can significantly optimize computation.

### Taichi

Taichi is a package commonly used in graphics computing, developed by @胡渊鸣. It supports GPU acceleration, JIT compilation on both CPU and GPU, automatic differentiation, and visualization. It’s more flexible than Jax, and the documentation and demos are comprehensive (including Chinese resources). If you're new to CUDA and want to accelerate with GPU, Taichi is an excellent choice.

### Pandas

Pandas is a package for handling tabular data. If you need data analysis or statistical analysis, this is a highly useful package.

### **Sklearn**
Sklearn integrates various machine learning algorithms for regression, classification, dimensionality reduction, etc., making it a great choice if you're looking to perform machine learning-related computations.

### **Conda**
 The tools mentioned above are various Python packages, whereas Conda is a package management tool used to manage these packages. Most of the time, you can simply install a package using the command `conda install + package name`. More importantly, Conda supports the `conda env` feature, which makes it very easy to migrate Python environments. Exporting and importing environments can be done with just one command:

Export environment (the resulting `env.yaml` file can be copied to any target machine):
 `conda env export > env.yaml`

Import environment:
 `conda env create -f env.yaml`

This makes it very convenient to migrate a Python environment from one system to another without incurring excessive overhead (Docker can also achieve this, but that’s not covered here).

Additionally, Conda also supports managing CUDA Toolkit, so when installing packages that require CUDA (e.g., CuPy, JAX), you no longer need to manually install CUDA.

## **Configuring the Python Environment**
 The most recommended method is to directly download Anaconda and install it with the default settings. Once installed, you’ll have Python set up, along with commonly used libraries like NumPy, SciPy, Pandas, Sklearn, Matplotlib, and Numba, and the package management tool Conda will also be available on your system. So, if you want to install packages like JAX or CuPy later, you can simply search for the Conda install command for these packages on their official websites, and in most cases, one command will do the trick.

## **How to Start Learning Python and the Required Packages**
 For learning Python, you can refer to the numerous online tutorials available (e.g., "菜鸟教程", "廖雪峰教程"), which are easy to find with a quick search. Python syntax forms the foundation of everything, so I recommend getting comfortable with the syntax first before diving into learning how to use various packages. While learning Python, I suggest focusing on the essentials, and skipping over sections that aren’t needed, like GUI programming or network programming, unless they are directly relevant to your needs.

As for getting started with each package, the best approach is to visit the official websites or GitHub repositories of the packages, where you'll find documentation, tutorials, demos, and other resources (I've added the links to the official websites in the second section, so feel free to check them out). The Python community is very active, and there’s a wealth of learning material available. With patience and persistence, you’ll surely gain a lot.

## **Other Python Optimization Tips**
 What we've discussed so far are acceleration methods based on existing packages or libraries. In fact, using PyPy or Cython (which can be seen as two different interpreters or compilers for Python) can also achieve similar acceleration effects. However, due to space limitations and the fact that these solutions have some limitations, I won’t go into further detail here. If you're interested, you can search for more information on your own.

In addition, when writing Python programs for scientific computation, following these principles can often lead to significant performance improvements (the following tips are based on my own experience, and feel free to add to them in the comments section if incomplete):

- Generally, a combination of Python3 + NumPy + SciPy + Numba should be enough to meet most scientific computing tasks’ computational and acceleration needs. If you need to use GPU for some functions or operations, you can also try libraries like CuPy, JAX, etc. Due to the GIL mechanism, Python's native `multiprocessing` has limited efficiency. So, if you want to implement large-scale parallel programs, I recommend using Numba’s parallel computation functions.
- Try to avoid implementing certain algorithms or operations yourself in Python. If there's a library function available in NumPy or a similar package (e.g., to calculate the Euclidean distance between two vectors, use the `norm` function instead of implementing it with a `for` loop), use it instead. These library functions are optimized for performance, so using them not only saves you time but also improves execution speed.
- NumPy + MKL is faster than plain NumPy, so if you can use the MKL version of NumPy, do so.
- Try to avoid using `for` loops in Python. If your program inevitably requires a lot of loops, consider using `jit` or vectorization techniques for acceleration. Often, adding `@numba.jit` to existing functions will significantly speed up your program (remember to set the `nopython=True` option, or use `numba.njit` instead of `numba.jit`). Also, if your `for` loop can be parallelized, use `prange` in Numba and set the `parallel=True` option in `jit`.
- GPU acceleration is a game-changer. Generally, the GPU computation power at the same price point far exceeds that of a CPU (speedup can be dozens or even hundreds of times). If your program has many parallelizable operations (e.g., matrix multiplication, vector operations, FFT, image filtering, convolutions, etc.), and you happen to have a GPU, I highly recommend exploring GPU acceleration to boost your program’s speed (e.g., using CuPy instead of NumPy, using `cuda.jit` from Numba for GPU JIT functions, using GPU acceleration in JAX or Taichi, etc.). You’ll be amazed by the efficiency of GPU acceleration when you try it for the first time.
- When writing GPU-accelerated programs, avoid frequent data copying between memory and VRAM. Due to bandwidth and latency reasons, excessive data copying can actually slow down your GPU-accelerated program’s performance.
- Sometimes, simply replacing the default CPython interpreter with PyPy can give computation-heavy programs several times the speed boost.
- Please note that the optimization solutions presented here are not suitable for all scientific computing scenarios, such as implementing high-performance low-level computing libraries or large-scale CPU parallel computing on supercomputers or large clusters. As a "glue" language, Python is most suitable for quickly implementing scientific computing scripts using mature, reliable, high-performance computing libraries, thereby reducing development time and difficulty. Developers don’t need to focus too much on low-level system details. However, this also means Python is not as capable as C++ in managing fine-grained low-level resource scheduling. If you need such control, I recommend using lower-level languages like C++.

Finally, I wish you all the best on your Python scientific computing journey!
