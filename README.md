# Awesome 3DGS Renderer
Collection of differentiable 3DGS CUDA renderer with simple installation and usage examples.

Overview:
| Renderer | Depth | Alpha | Extrinsics Gradient | Batch Rendering |
|---|---|---|---|---|---|---|
| Inria 3DGS | ✅ | ❌ | ❌ | ❌ |
| Faster-GS  | ❌ | ❌ | ❌ | ❌ |
| ashawkey   | ✅ | ✅ | ❌ | ❌ |
| gsplat     | ✅ | ✅ | ✅ | ✅ |



| Renderer | Inference Speed | Training Speed |
|---|---|---|
| Inria 3DGS     | tbd | tbd |
| Faster-GS      | tbd | tbd |
| ashawkey       | tbd | tbd |
| gsplat         | tbd | tbd |


## Inria 3DGS

Repo: https://github.com/graphdeco-inria/diff-gaussian-rasterization/tree/main

<details>
<summary>Installation</summary>

```
git clone --recursive https://github.com/graphdeco-inria/diff-gaussian-rasterization/tree/main
pip install diff-gaussian-rasterization --no-build-isolation
```
</details>

<details>
<summary>Usage</summary>
    
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

Repo: https://github.com/fhahlbohm/gaussian-splatting

<details>
<summary>Installation</summary>
    
```
pip install git+https://github.com/nerficg-project/faster-gaussian-splatting/#subdirectory=FasterGSCudaBackend --no-build-isolation
```
</details>

<details>
<summary>Usage</summary>
    
```py
from FasterGSCudaBackend.torch_bindings import diff_rasterize, RasterizerSettings

raster_settings = RasterizerSettings(
    w2c=viewpoint_camera.world_view_transform.T.contiguous(),  # FasterGSCudaBackend uses row-major matrices
    cam_position=viewpoint_camera.camera_center.contiguous(),
    bg_color=bg_color.contiguous(),
    active_sh_bases=(pc.active_sh_degree + 1) ** 2,
    width=int(viewpoint_camera.image_width),
    height=int(viewpoint_camera.image_height),
    focal_x=1 / math.tan(viewpoint_camera.FoVx / 2) * (viewpoint_camera.image_width / 2),
    focal_y=1 / math.tan(viewpoint_camera.FoVy / 2) * (viewpoint_camera.image_height / 2),
    center_x=viewpoint_camera.image_width / 2,
    center_y=viewpoint_camera.image_height / 2,
    near_plane=0.2,
    far_plane=10000.0,
    proper_antialiasing=pipe.antialiasing,
)

rendered_image = diff_rasterize(
    means=means,
    scales=scales,
    rotations=rotations,
    opacities=opacities,
    sh_coefficients_0=sh_coefficients_0,
    sh_coefficients_rest=sh_coefficients_rest,
    densification_info=densification_info,
    rasterizer_settings=raster_settings,
)

```
</details>

## ashawkey

Repo: https://github.com/ashawkey/diff-gaussian-rasterization

<details>
<summary>Installation</summary>
    
```
git clone --recursive https://github.com/ashawkey/diff-gaussian-rasterization.git
pip install diff-gaussian-rasterization --no-build-isolation
```
</details>
<details>
<summary>Usage</summary>
    
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

Repo: https://github.com/fhahlbohm/gaussian-splatting

<details>
<summary>Installation</summary>
    
```
pip install gsplat
```
</details>
<details>
<summary>Usage</summary>

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
