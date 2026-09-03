# Data layout

The required RAW camera frames are included in the paths below. The notebook resolves every path relative to the repository root, so no machine-specific directory changes are needed.

```text
data/
├── paired_frames/
│   ├── row4_cam3_arducam_21mm_f0008.raw
│   ├── row3_cam8_vimba_50mm_f0008.raw
│   ├── row3_cam4_arducam_21mm_f0008.raw
│   └── row3_cam7_vimba_25mm_f0008.raw
├── polarization/
│   ├── row3_cam3_arducam_4mm_f0008.raw
│   └── row1_cam7_lucid_pol_f0008.raw
├── sweeps/
│   ├── arducam/*.raw
│   └── vimba/*.raw
└── synchronized/
    ├── color/*.raw
    └── mono/*.raw
```

Files in `synchronized/color/` and `synchronized/mono/` are paired by identical filename.

The included RAW dataset is approximately 822 MB. Each individual file is below GitHub's 100 MB hard limit, but Git LFS or an archival data repository is recommended to keep the repository manageable. Add the final data license and permanent archival URL before public release.
