# GPU Notes & Known Issues

MorphoCloud's GPU instances run on JetStream2, a shared national research cloud.
This page covers GPU-specific behavior and known limitations so you can pick the
right instance and avoid surprises.

## GPU instance types

GPU flavors differ in **GPU memory**, **GPU speed**, **vCPUs**, and **availability** —
bigger GPU memory does not mean faster. They're listed below in the order you should
escalate through them:

| Flavor | GPU | vCPU | RAM | When to use |
|--------|-----|-----:|----:|-------------|
| `g3.large` *(default)* | ½ A100 — 20 GB | 16 | 60 GB | **Almost everything.** Best availability, so it's quickest to get and unshelve — start here. |
| `g4.xl` | L40S — 48 GB | 12 | 120 GB | When g3.large runs short on **GPU memory (>20 GB)** or **system RAM (>60 GB)**. More memory than g3.large, but **fewer vCPUs** and a GPU that is **not as fast as a full A100**. |
| `g3.xl` | full A100 — 40 GB | 32 | 120 GB | **Heaviest GPU workloads.** A full A100 is roughly **2× faster than g4.xl** and has **2× its vCPUs**. Pick it when raw GPU speed matters most. |

### Which one should I pick?

1. **Start with `g3.large`** (the default). It handles almost all 3D Slicer / SlicerMorph
   work and has the most JetStream2 availability, so you'll get an instance fastest.
2. **Step up to `g4.xl` only if you hit a wall** on g3.large — i.e. you need **more GPU
   memory** or **more system RAM**. Its L40S has the most GPU memory (48 GB), but it has
   the **fewest vCPUs (12)** and is **not** as fast as a full A100, so choose it for
   *capacity*, not speed.
3. **Use `g3.xl` for the heaviest / fastest GPU work** — a full 40 GB A100 with 32 vCPUs,
   about **twice as fast as g4.xl** across the board. Availability is lower than
   g3.large, so reserve it for jobs that truly need the speed.

> **Rule of thumb:** need more GPU *memory* → `g4.xl`; need more GPU *speed* → `g3.xl`;
> everything else → `g3.large`.

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
