# GPU Notes & Known Issues

MorphoCloud's GPU instances run on JetStream2, a shared national research cloud. This
page helps you choose the right GPU instance type, change it if needed, and avoid known
limitations. For the full specs of every type, see the
[instance types table](../README.md#instance-types).

## How to choose a GPU instance?

GPU types differ in **GPU memory**, **GPU speed**, **vCPUs**, and **availability** —
bigger GPU memory does not mean faster. Escalate through them in this order:

1. **Start with `g3.large`** (the default — ½ A100, 20 GB). It handles almost all
   3D Slicer / SlicerMorph work.
   - **When no `g3.large` is free**, `g3.medium` (¼ A100, 10 GB, 30 GB RAM) is an
     alternative for datasets up to about 3 GB. Larger datasets are likely to run
     out of memory on it.
2. **Step up to `g4.xl` only if you hit a wall** on g3.large — i.e. you need **more GPU
   memory** or **more system RAM**. Its L40S has the most GPU memory (48 GB), but it has
   the **fewest vCPUs (12)** and is **not** as fast as a full A100, so choose it for
   *capacity*, not speed.
3. **Use `g3.xl` for the heaviest / fastest GPU work** — a full 40 GB A100 with 32 vCPUs,
   about **twice as fast as g4.xl** across the board. Availability is lower than
   g3.large, so reserve it for jobs that truly need the speed.

> **Rule of thumb:** need more GPU *memory* → `g4.xl`; need more GPU *speed* → `g3.xl`;
> everything else → `g3.large`.

Non-GPU types (`m3.xl`, `r3.large`, `r3.xl`) are slow at rendering 3D data. If that
slowdown is acceptable, they perform better for tasks that need large memory (such as
segmenting big scans) or heavily multi-threaded work like image registration. `r3.large` and `r3.xl` are
only for members of the large-memory team.

## Changing your instance type

You can't change the type of an instance in place. Instead:

1. Press **Delete** on your instance's card on the [portal](https://portal.morphocloud.org).
2. Choose the new type and press **Create instance**.

Your storage (MyDrive) comes back on the new instance, so your files in Desktop,
Documents, Downloads and the rest of MyDrive are kept. Anything saved only on the
old instance, such as the Slicer extensions you installed, is lost.

## Known issues

### nnInteractive: choose Full, then restart Slicer once

The first time you open **nnInteractive** on an instance, a dialog asks what to
install. Click **Full (local + remote)**. The highlighted default, **Client only
(remote)**, needs a separate server, so do not just press Enter. The installation
takes about two minutes.

When it finishes, **quit Slicer and start it again** before you segment. The
installation replaces Python packages that the running Slicer has already loaded,
so without the restart nnInteractive does not start: it can stop responding, or
fail with:

> Could not start nnInteractive (local mode): 'numpy.ufunc' object has no attribute '\_\_module\_\_'

After the restart it works on every GPU type. You only need to do this once per
instance. Step-by-step:
[nnInteractive tutorial](https://github.com/SlicerMorph/Tutorials/blob/main/MorphoCloud/NNInteractive.MD).

### Large-volume rendering stalls GPU instances (≥ 4096 voxels)

**On GPU instances, 3D Slicer's interactivity drops dramatically — sometimes to the
point of being unusable — when you volume-render a 3D volume whose dimension along
*any* axis is ≥ 4096 voxels.** This is a known behavior of volume rendering on these
GPUs, not a problem with your instance.

**What to do:**

- For routine data (dimensions below 4096), the GPU types are fast — no action needed.
- For very large volumes, **crop or downsample** before volume rendering, or use a
  **large-memory, non-GPU type** (`m3.xl`, `r3.large`, `r3.xl`) where CPU rendering
  handles the large array without the GPU bottleneck. (Switching type? See
  [Changing your instance type](#changing-your-instance-type) above.)

### TurboVNC stops resizing the desktop

If the desktop no longer resizes when you resize the TurboVNC window, restart the
instance: save your work, then run `sudo reboot` in a terminal on the instance or
over SSH. The address stays the same; connect again after a few minutes.

### Availability can block creating or unshelving

JetStream2 is a **shared national resource**, so a given type is **not guaranteed to
be free** at any moment — and this is not only a one-time concern at creation. **Every
Unshelve must find a free machine of the instance's type**; if none is free, the
Unshelve (or Create) **fails or waits** until one frees up. Your files in MyDrive are
safe — only the running instance is affected.

- **Scarcer/larger types are riskier.** A `g3.xl` (full A100) is in higher demand and
  shorter supply than `g3.large`, so an instance you created on `g3.xl` can still **fail
  to unshelve later** if no A100 is free at that moment.
- **Check before you create or unshelve:** the line at the top of the
  [portal](https://portal.morphocloud.org) shows how many machines of each type are free.
- If a type is scarce, try again later, or use a more available type when your task
  allows.
- **For courses,** simultaneous access for a whole class at one meeting time is not
  guaranteed — MorphoCloud is best used as an *asynchronous* classroom tool.

---

*[Back to the User Guide](README.md) | See also: [Connecting to your instance](connecting.md) ·
[Transferring files](file-transfer.md)*
