# Awesome 3DGS Renderer
Collection of 3DGS renderer

## Inria 3DGS

- ✅ CUDA
- ✅ Differentiable
- ✅ Depth
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

<details>
Usage:
    
```py
from diff_gaussian_rasterization import GaussianRasterizationSettings, GaussianRasterizer

raster_settings = GaussianRasterizationSettings(
    image_height=int(viewpoint_camera.image_height),
    image_width=int(viewpoint_camera.image_width),
    tanfovx=tanfovx,
    tanfovy=tanfovy,
    bg=bg_color,
    scale_modifier=scaling_modifier,
    viewmatrix=viewpoint_camera.world_view_transform,
    projmatrix=viewpoint_camera.full_proj_transform,
    sh_degree=pc.active_sh_degree,
    campos=viewpoint_camera.camera_center,
    prefiltered=False,
    debug=pipe.debug,
    antialiasing=pipe.antialiasing
)
rasterizer = GaussianRasterizer(raster_settings=raster_settings)

rendered_image, radii, depth_image = rasterizer(
    means3D = means3D,
    means2D = means2D,
    shs = shs,
    colors_precomp = colors_precomp,
    opacities = opacity,
    scales = scales,
    rotations = rotations,
    cov3D_precomp = cov3D_precomp
)

)
```
</details>

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

<details>
    
Usage:
```py
rendered_image, radii, rendered_depth, rendered_alpha = rasterizer(
    means3D=means3D,
    means2D=means2D,
    shs=shs,
    colors_precomp=colors_precomp,
    opacities=opacity,
    scales=scales,
    rotations=rotations,
    cov3D_precomp=cov3D_precomp,
)
```
</details>

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

<details>
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
</details>
