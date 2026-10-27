# LFP in Brain Space

An interactive browser viewer for a selected 50-probe LFP cohort. It places 24 contiguous depth groups per probe in Allen atlas space and lets you explore LFP amplitude across each saved 100-second excerpt.

Open `index.html` directly in a modern browser. The viewer is a self-contained file and does not make network requests.

## What the display contains

- 50 probes from 26 recording sessions and 21 subjects.
- 24 measured depth groups per probe, each comprising 16 consecutive cached channels.
- A 100-second, 500 Hz cached LFP excerpt per probe.
- One amplitude value per group per 0.5-second window: the mean of the 16 channels' RMS amplitudes.
- A two-second signed-voltage trace for the channel nearest the middle depth of the selected probe.

The all-probe display overlays distinct sessions in atlas space. Their shared elapsed-time slider does **not** represent simultaneous brain-wide activity. Select an individual recording before comparing its probes in time.

## Data and anatomical context

The viewer uses cached, destriped LFP that was FIR-decimated to 500 Hz with a two-second edge guard. It does not contain native 2,500 Hz acquisition data, LFPack reconstructions, behavioral predictions, or a new clock-alignment analysis. The atlas outline is a decimated orientation guide derived from the Allen Common Coordinate Framework; it is not an individual-subject brain mesh.

Coordinates are in millimeters relative to IBL bregma, with medial-lateral positive to the right, anterior-posterior positive anteriorly, and dorsal-ventral positive dorsally. Depth labels refer to distance along the probe shaft from its tip, not anatomical dorsal-ventral position.

`root` and `void` in the regional labels mean that the source group was not assigned a specific brain region.

## Reproducibility notes

The embedded amplitude values are quantized for compact delivery: the maximum absolute RMS rounding error is 0.004593 µV, with no clipping or imputation. The viewing file contains all visualization data needed to run it.

This repository deliberately does not assign a reuse license. Please contact the repository owner before reusing the code or embedded data.
