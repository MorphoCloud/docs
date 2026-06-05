# GPU Notes & Known Issues

MorphoCloud's GPU instances run on JetStream2, a shared national research cloud. This
page helps you choose the right GPU flavor, change it if needed, and avoid known
limitations. For the full specs of every flavor, see the
[instance types table](../README.md#instance-types).

## How to choose a GPU instance?

GPU flavors differ in **GPU memory**, **GPU speed**, **vCPUs**, and **availability** —
bigger GPU memory does not mean faster. Escalate through them in this order:

1. **Start with `g3.large`** (the default — ½ A100, 20 GB). It handles almost all
   3D Slicer / SlicerMorph work and has the most JetStream2 availability, so you'll get
   an instance fastest.
2. **Step up to `g4.xl` only if you hit a wall** on g3.large — i.e. you need **more GPU
   memory** or **more system RAM**. Its L40S has the most GPU memory (48 GB), but it has
   the **fewest vCPUs (12)** and is **not** as fast as a full A100, so choose it for
   *capacity*, not speed.
3. **Use `g3.xl` for the heaviest / fastest GPU work** — a full 40 GB A100 with 32 vCPUs,
   about **twice as fast as g4.xl** across the board. Availability is lower than
   g3.large, so reserve it for jobs that truly need the speed.

> **Rule of thumb:** need more GPU *memory* → `g4.xl`; need more GPU *speed* → `g3.xl`;
> everything else → `g3.large`.

Non-GPU flavors (`m3.xl`, `r3.large`, `r3.xl`) are slow at rendering 3D data. If that
slowdown is acceptable, they perform better for tasks that need large memory (such as
segmenting big scans) or heavily multi-threaded work like image registration.

## Changing your instance flavor

You **can't change a flavor in place**, and a change should be **justified** — e.g. the
GPU memory is too small for your data, or you hit out-of-memory (OOM) errors. There are
two ways to switch, and they differ in whether your data survives.

**Recommended — admin-assisted (keeps your persistent storage):**

1. Tag `@MorphoCloud/morphocloud-admins` in a comment on your **existing** issue and
   explain why (e.g. "20 GB GPU isn't enough", "OOM on g3.large").
2. Run `/delete_instance` — this removes the instance but **not** your MyData volume.
3. An admin updates the issue's flavor label to your new flavor.
4. Re-run `/create` on the same issue. The instance is recreated on the new flavor with
   your **MyData volume re-attached — no data is lost**.

**On your own (does NOT carry over your data):**

You can `/delete_all` (instance + volume), close the issue, and open a **new** request
with the new flavor. The new instance comes up with a **fresh, empty MyData volume** —
your previous files are **not** carried over, so [back them up](file-transfer.md) first.

## Known issues

### Large-volume rendering stalls GPU instances (≥ 4096 voxels)

**On GPU instances, 3D Slicer's interactivity drops dramatically — sometimes to the
point of being unusable — when you volume-render a 3D volume whose dimension along
*any* axis is ≥ 4096 voxels.** This is a known behavior of volume rendering on these
GPUs, not a problem with your instance.

**What to do:**

- For routine data (dimensions below 4096), the GPU flavors are fast — no action needed.
- For very large volumes, **crop or downsample** before volume rendering, or use a
  **large-memory, non-GPU flavor** (`m3.xl`, `r3.large`, `r3.xl`) where CPU rendering
  handles the large array without the GPU bottleneck. (Switching flavor? See
  [Changing your instance flavor](#changing-your-instance-flavor) above.)

### Availability can block creating or unshelving

JetStream2 is a **shared national resource**, so a given flavor is **not guaranteed to
be free** at any moment — and this is not only a one-time concern at creation. **Every
`/unshelve` must find a free slot of the instance's flavor**; if none is available, the
unshelve (or `/create`) **fails or stalls** until capacity frees up. Your data on the
MyData volume is safe — only the running instance is affected.

- **Scarcer/larger flavors are riskier.** A `g3.xl` (full A100) is in higher demand and
  shorter supply than `g3.large`, so an instance you created on `g3.xl` can still **fail
  to unshelve later** if no A100 slot is free at that moment.
- **Check before you create or unshelve:**
  [real-time JetStream2 availability →](https://morphocloud.org)
- If a flavor is scarce, try again later, or use a more-available flavor (usually
  `g3.large`) when your task allows.
- **For courses,** simultaneous access for a whole class at one meeting time is not
  guaranteed — MorphoCloud is best used as an *asynchronous* classroom tool.

---

*[Back to the User Guide](README.md) | See also: [Connecting to your instance](connecting.md) ·
[Transferring files](file-transfer.md)*
