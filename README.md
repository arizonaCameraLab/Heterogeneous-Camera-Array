# Heterogeneous Camera Array - Multiscale Viewer

Viewer application for multiscale imagery captured with multi-focal camera arrays (4mm, 8mm, 21mm, 35mm) and polarization sensors.

![Multiscale Viewer Layers](multiscale_layers.png)

## Versions & Downloads

| Version | Operating System | Features | Branch Link |
| :--- | :--- | :--- | :--- |
| **Multiscale Viewer 2** | Windows x64 | Polarization support (DoLP, AoLP, S0, I0-I135), auto deep-zoom, sample datasets | [View `windows-v2-pol`](https://github.com/arizonaCameraLab/Heterogeneous-Camera-Array/tree/windows-v2-pol) |
| **Multiscale Viewer 1** | Windows x64 | Standard multiscale viewer (4mm, 8mm, 21mm, 35mm) + homography generator | [View `windows-v1`](https://github.com/arizonaCameraLab/Heterogeneous-Camera-Array/tree/windows-v1) |
| **Multiscale Viewer 1** | Linux x86_64 | Standard multiscale viewer with bundled dynamic libraries | [View `linux-v1`](https://github.com/arizonaCameraLab/Heterogeneous-Camera-Array/tree/linux-v1) |

## Cloning a Branch

To clone only the branch you need:

```bash
# Windows Viewer 2 (with polarization)
git clone -b windows-v2-pol https://github.com/arizonaCameraLab/Heterogeneous-Camera-Array.git

# Windows Viewer 1
git clone -b windows-v1 https://github.com/arizonaCameraLab/Heterogeneous-Camera-Array.git

# Linux Viewer 1
git clone -b linux-v1 https://github.com/arizonaCameraLab/Heterogeneous-Camera-Array.git
```

## Running the Viewer

### Windows (v1 & v2)
1. Switch to or clone the relevant Windows branch (`windows-v2-pol` or `windows-v1`).
2. If needed, install the Visual C++ runtime (`vc_redist.x64.exe`).
3. Run `viewer.exe` (Viewer 2) or `MultiscaleViewer.exe` (Viewer 1).

### Linux (v1)
1. Switch to or clone the `linux-v1` branch.
2. In your terminal, run:
```bash
chmod +x run_viewer.sh viewer
./run_viewer.sh
```

## Controls

### Mouse Controls
- Mouse Wheel: Zoom In / Zoom Out
- Left Click + Drag: Pan across image

### Layer Selection
- 0: Auto Deep-Zoom Mode (automatically swaps layers based on zoom level)
- 1: Force 4mm Base Layer
- 2: Force 8mm RGB Stitched Layer
- 3: Force 8mm Polarization Layer (Viewer 2 only)
- 4: Force 21mm Stitched Layer
- 5: Force 35mm Stitched Layer

### Polarization Modes (Viewer 2 only, when 8mm layer is active)
- Q: S0 (Total Intensity)
- W: I0 (0-degree)
- E: I45 (45-degree)
- R: I90 (90-degree)
- T: I135 (135-degree)
- Y: DoLP (Degree of Linear Polarization - Viridis colorbar)
- U: AoLP (Angle of Linear Polarization - HSV colorbar)

### Viewport Controls
- Spacebar: Reset View (recenter and default zoom)

---

## Camera Array Processing Examples

This repository also includes reproducible processing examples for the accompanying IEEE Transactions on Computational Imaging manuscript. The notebook covers cross-camera registration, image fusion, polarization overlays, focus/exposure stacking, and local refinement for synchronized captures.

### Processing quick start

1. Clone the repository and enter its root directory.
2. Create and activate a Python environment.
3. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

   The validated environment uses Python 3.10. Conda users can reproduce it with `conda env create -f environment.yml`.

4. Verify the included RAW dataset:

   ```bash
   sha256sum -c data/SHA256SUMS
   ```

5. Start Jupyter from the repository root and open `Camera_Array_Processing_Examples.ipynb`.

   ```bash
   jupyter lab
   ```

The notebook automatically selects CUDA when available and otherwise uses the CPU. If Jupyter must be started from another directory, set `CAMERA_ARRAY_PROJECT_ROOT` to the cloned repository path before launching it.

### Processing tasks

- **Task 1A:** 21 mm color to 50 mm monochrome registration and fusion comparison.
- **Task 1B:** overlap-cropped 21 mm color to 25 mm monochrome fusion with local refinement.
- **Task 2:** global and 3 × 3 piecewise polarization registration and structural overlays.
- **Task 3:** Vimba exposure fusion, Arducam focus stacking, cross-modal registration, and MTF-GLP-HPM fusion.
- **Task 4:** synchronized-pair global alignment, local refinement, and fusion comparison.

Run **Setup** and **Shared utilities** first, followed by the cells for the desired task. Task-specific filenames and patch coordinates are grouped at the beginning of each section.

### Reproducibility notes

- The required RAW files are organized under `data/`; see [`data/README.md`](data/README.md).
- RAW dimensions and normalization constants are centralized in the setup cell.
- All input paths are repository-relative; no user-specific paths are stored in the notebook.
- Notebook outputs and execution counts are cleared to keep the code reviewable.
- `requirements.txt` pins the versions used for successful real-data validation, including the exact LightGlue revision.
- Before the paper artifact is archived, add the dataset DOI, license, and permanent archival URL to `data/README.md`.
