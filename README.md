# LFP in Brain Space

An interactive browser viewer for a selected 50-probe LFP cohort. It places 24 contiguous depth groups per probe in Allen atlas space and lets you explore LFP amplitude across each saved 100-second excerpt.

Open `index.html` directly in a modern browser. The viewer is a self-contained file and does not make network requests.

## What the display contains

- 50 probes from 26 recording sessions and 21 subjects.
- 24 measured depth groups per probe, each comprising 16 consecutive cached channels.
- A 100-second, 500 Hz cached LFP excerpt per probe.
- One amplitude value per group per 0.5-second window: the mean of the 16 channels' RMS amplitudes.
- A signed-voltage trace for the channel nearest the middle depth of the selected probe, synchronized to the selected 0.5-second time window.

The all-probe display overlays distinct sessions in atlas space. Their shared elapsed-time slider does **not** represent simultaneous brain-wide activity. Select an individual recording before comparing its probes in time.

## Data and anatomical context

The viewer uses cached, destriped LFP that was FIR-decimated to 500 Hz with a two-second edge guard. It does not contain native 2,500 Hz acquisition data, LFPack reconstructions, behavioral predictions, or a new clock-alignment analysis. The atlas outline is a decimated orientation guide derived from the Allen Common Coordinate Framework; it is not an individual-subject brain mesh.

Coordinates are in millimeters relative to IBL bregma, with medial-lateral positive to the right, anterior-posterior positive anteriorly, and dorsal-ventral positive dorsally. Depth labels refer to distance along the probe shaft from its tip, not anatomical dorsal-ventral position.

`root` and `void` in the regional labels mean that the source group was not assigned a specific brain region.

## Reproducibility notes

The embedded amplitude values are quantized for compact delivery: the maximum absolute RMS rounding error is 0.004593 µV, with no clipping or imputation. The viewing file contains all visualization data needed to run it.

## LFP by brain state

`lfp-by-state/index.html` is a second self-contained viewer for the same 50 probes. It colors the same 24 depth groups per probe by the LFP amplitude on trials where the mouse was in one of three behavioral states (engaged, biased left, biased right), and by the difference between biased and engaged trials.

- States come from a 3-state GLM-HMM fitted to each mouse's choices. For 19 of the 21 subjects the model was refit without the recorded sessions, so the states of the recorded trials come from a model that never saw them.
- 15,749 trials: 12,551 engaged, 1,258 biased left and 1,940 biased right. 42 of the 50 probes have at least 10 biased trials.
- LFP for the whole task period of each probe, filtered and referenced like the excerpts above, in seven frequency bands and 50 ms steps from 1 s before to 1.5 s after stimulus onset.
- The difference view compares each biased trial with the engaged trials within 50 trials of it, so slow drift over a session does not count as a state effect. The chance range comes from rotating each session's state sequence in time 1,000 times.

In the 1 s before the stimulus the three states look almost the same: amplitude on biased trials is within about 1 to 3% of engaged trials at a typical probe, which is the size of chance fluctuations.

This repository deliberately does not assign a reuse license. Please contact the repository owner before reusing the code or embedded data.
