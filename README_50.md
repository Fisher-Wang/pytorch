# PyTorch 2.3.1 for 50x0 Series GPU

## Build
Ensure you have installed CUDA Toolkit 12.8:
```bash
nvcc --version
```

Create a python venv that matches the target wheel version
```bash
conda create -n py38 python=3.8 -y
conda activate py38
```

```bash
git submodule update --init --recursive
export USE_CUDA=1
export TORCH_CUDA_ARCH_LIST="12.0"
export USE_LAPACK=1
export USE_BLAS=OpenBLAS
export MAX_JOBS=20  # change to number that works on your machine
python setup.py bdist_wheel
```

The built wheel is in `./dist`.

## Verify
```bash
cd ~
python -c "import torch; print(torch.__config__.show())"
```

The output for reference:
```
PyTorch built with:
  - GCC 11.4
  - C++ Version: 201703
  - Intel(R) MKL-DNN v3.3.6 (Git Hash 86e6af5974177e513fd3fee58425e1063e7f1361)
  - OpenMP 201511 (a.k.a. OpenMP 4.5)
  - LAPACK is enabled (usually provided by MKL)
  - NNPACK is enabled
  - CPU capability usage: AVX2
  - CUDA Runtime 12.8
  - NVCC architecture flags: -gencode;arch=compute_120,code=sm_120
  - Build settings: BLAS_INFO=open, BUILD_TYPE=Release, CUDA_VERSION=12.8, CXX_COMPILER=/usr/bin/c++, CXX_FLAGS= -D_GLIBCXX_USE_CXX11_ABI=1 -fvisibility-inlines-hidden -DUSE_PTHREADPOOL -DNDEBUG -DUSE_KINETO -DLIBKINETO_NOROCTRACER -DUSE_FBGEMM -DUSE_QNNPACK -DUSE_PYTORCH_QNNPACK -DUSE_XNNPACK -DSYMBOLICATE_MOBILE_DEBUG_HANDLE -O2 -fPIC -Wall -Wextra -Werror=return-type -Werror=non-virtual-dtor -Werror=range-loop-construct -Werror=bool-operation -Wnarrowing -Wno-missing-field-initializers -Wno-type-limits -Wno-array-bounds -Wno-unknown-pragmas -Wno-unused-parameter -Wno-unused-function -Wno-unused-result -Wno-strict-overflow -Wno-strict-aliasing -Wno-stringop-overflow -Wsuggest-override -Wno-psabi -Wno-error=pedantic -Wno-error=old-style-cast -Wno-missing-braces -fdiagnostics-color=always -faligned-new -Wno-unused-but-set-variable -Wno-maybe-uninitialized -fno-math-errno -fno-trapping-math -Werror=format -Wno-stringop-overflow, LAPACK_INFO=open, PERF_WITH_AVX=1, PERF_WITH_AVX2=1, PERF_WITH_AVX512=1, TORCH_VERSION=2.3.0, USE_CUDA=1, USE_CUDNN=OFF, USE_CUSPARSELT=OFF, USE_EIGEN_FOR_BLAS=ON, USE_EXCEPTION_PTR=1, USE_GFLAGS=OFF, USE_GLOG=OFF, USE_GLOO=ON, USE_MKL=OFF, USE_MKLDNN=ON, USE_MPI=OFF, USE_NCCL=ON, USE_NNPACK=ON, USE_OPENMP=ON, USE_ROCM=OFF, USE_ROCM_KERNEL_ASSERT=OFF,
```

## TorchVision
Work with `0.14.1`, but not with `0.18.1`:
```bash
pip install torchvision==0.14.1 --no-deps`
```

## Reference
- https://blog.csdn.net/m0_56706433/article/details/148902144
