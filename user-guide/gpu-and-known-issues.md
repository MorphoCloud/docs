# GPU Notes & Known Issues

MorphoCloud's GPU instances run on JetStream2, a shared national research cloud.
This page covers GPU-specific behavior and known limitations so you can pick the
right instance and avoid surprises.

## GPU instance types

| Flavor | GPU | Notes |
|--------|-----|-------|
| `g3.large` | A100, **½ card (20 GB)** | Default. Covers most 3D Slicer / SlicerMorph workflows. |
| `g3.xl` | A100, **full card (40 GB)** | Heavier GPU workloads needing more GPU memory. |
| `g4.xl` | L40S (48 GB) | Photogrammetry, NNInteractive, AI-assisted segmentation, large GPU workloads. |

Non-GPU flavors (`m3.xl`, `r3.large`, `r3.xl`) trade the GPU for large RAM/CPU and
are the right choice for the large-volume case below. See the full flavor table in
the [User Guide overview](../README.md#instance-types).

---

## Known issues

### Large-volume rendering stalls GPU instances (≥ 4096 voxels)

**On GPU instances (`g3.large`, `g3.xl`), 3D Slicer's interactivity drops
dramatically — sometimes to the point of being unusable — when you volume-render a
3D volume whose dimension along *any* axis is ≥ 4096 voxels.** This is a known
behavior of volume rendering on these GPUs, not a problem with your instance.

**What to do:**
- For routine data (dimensions below 4096), the GPU flavors are fast — no action needed.
- For very large volumes, either **crop or downsample** before volume rendering, or
  use a **large-memory, non-GPU flavor** (`m3.xl`, `r3.large`, `r3.xl`) where CPU
  rendering handles the large array without the GPU bottleneck.
- You cannot change a flavor in place — if you need a different one, open a new
  instance request issue with that flavor (see [Commands](commands.md)).

---

## Resource availability (not a bug, but plan for it)

JetStream2 is shared nationally, so a given GPU flavor is **not guaranteed to be
free** at any moment. `/create` or `/unshelve` can wait (or stall) when the
requested flavor is at capacity.

- **Check before you create or unshelve:**
  [real-time JetStream2 availability →](https://morphocloud.org)
- If a flavor is scarce, try again later, or consider whether a more-available
  flavor fits your task.
- For **courses**, simultaneous access for a whole class at one meeting time is not
  guaranteed — MorphoCloud is best used as an *asynchronous* classroom tool.

---

*[Back to the User Guide](README.md) | See also: [Connecting to your instance](connecting.md) ·
[Transferring files](file-transfer.md)*
