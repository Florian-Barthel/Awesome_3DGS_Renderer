# Awesome 3DGS Renderer
Collection of 3DGS renderer

## Inria 3DGS

- ✅ CUDA
- ✅ Differentiable
- ❌ Depth
- ❌ Alpha
- ❌ Extrinsics Gradient
- ❌ Batch Rendering

Inference Speed: tbd
Training Speed:tdb

Repo: https://github.com/graphdeco-inria/diff-gaussian-rasterization/tree/main

Installation: 
```
git clone --recursive https://github.com/graphdeco-inria/diff-gaussian-rasterization/tree/main
pip install diff-gaussian-rasterization --no-build-isolation
```

## Faster-GS

- ✅ CUDA
- ✅ Differentiable
- ❌ Depth
- ❌ Alpha
- ❌ Extrinsics Gradient
- ❌ Batch Rendering

Inference Speed: tbd
Training Speed:tdb

Repo: https://github.com/fhahlbohm/gaussian-splatting

Installation: 
```
pip install git+https://github.com/nerficg-project/faster-gaussian-splatting/#subdirectory=FasterGSCudaBackend --no-build-isolation
```

## ashawkey

- ✅ CUDA
- ✅ Differentiable
- ✅ Depth
- ✅ Alpha
- ❌ Extrinsics Gradient
- ❌ Batch Rendering

Inference Speed: tbd
Training Speed:tdb

Repo: https://github.com/ashawkey/diff-gaussian-rasterization

Installation: 
```
git clone --recursive https://github.com/ashawkey/diff-gaussian-rasterization.git
pip install diff-gaussian-rasterization --no-build-isolation
```

## gsplat

- ✅ CUDA
- ✅ Differentiable
- ✅ Depth
- ✅ Alpha
- ✅ Extrinsics Gradient
- ✅ Batch Rendering

Inference Speed: tbd
Training Speed:tdb

Repo: https://github.com/fhahlbohm/gaussian-splatting

Installation: 
```
pip install gsplat
```

Usage:

```py
from gsplat.rendering import rasterization

render_colors, render_alphas, info = rasterization(
    means=means,                              # [B, N, 3]
    quats=quats,                              # [B, N, 4]
    scales=scales,                            # [B, N, 3]
    opacities=opacities,                      # [B, N]
    colors=colors,                            # [B, N, C, D]
    viewmats=torch.linalg.inv(camtoworlds),   # [B, 4, 4]
    Ks=Ks,                                    # [B, 3, 3]
    width=width,
    height=height,
    render_mode: "RGB",                       # ["RGB", "D", "ED", "RGB+D", "RGB+ED"]
)
```
