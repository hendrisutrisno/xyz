# Robotic multi-object collection benchmark

This data-only repository contains 40 synthetic instances and a physical demonstration video for robotic multi-object collection with stack assembly and delivery to two receiving stations.

## Contents

- `instances/`: the 40 original text files, their checksum catalog, validation records and detailed format documentation.
- `instances.csv`: a combined table of all 1,680 object records. Read `object_id` as text to retain leading zeros.
- `metadata/operating_settings.json`: baseline operating inputs and one-factor sensitivity levels.
- `metadata/base_angles.json`: the base-coordinate snapshot used by the computational experiments. These angular references do not certify full robot trajectories.
- `media/physical_demonstration.mp4`: a silent 720p video illustrating pickup, stack transport and delivery.
- `SHA256SUMS.txt`: integrity hashes for the repository files.

## Instance design

There are eight instances at each object count: 10, 20, 40, 60 and 80. At each size, four height profiles share two spatial layouts. File suffixes 1–2, 3–4, 5–6 and 7–8 denote uniform, truncated normal, exponential and reflected exponential heights, respectively. Odd and even suffixes identify the two layouts.

Objects have 5 × 5 cm footprints and heights from 4 to 10 cm on a 0.2 cm grid. Half are assigned to each receiver. Coordinates and receiver assignments are paired across height profiles; the collection therefore has ten independent spatial layouts, not 40 independent layouts.

## Reading an instance

The first line contains the instance identifier prefixed by `#`. Each subsequent line contains:

```text
object_id x_m y_m z_center_m height_cm destination_id
```

Coordinates use metres and object heights use centimetres. Objects stand on z = 0, so `z_center_m = height_cm / 200`. Receiver positions are A = (0, −0.45, 0) and B = (0, 0.45, 0). See `instances/README.md` for distribution and spatial-mixing details.

## Operating configurations

The baseline height capacity is 15 cm, the complete load-cycle limit is 90 s and consolidation overhead is 4 s. Sensitivity tests reuse the same 40 instances while changing one operating input at a time. The JSON settings file lists all values and units. Algorithm implementations and experiment outputs are outside this repository.

## Physical demonstration

The video illustrates handling operations and is separate from the 40 synthetic instances. It does not establish measured execution-time savings or repeated-trial reliability. The distribution copy omits audio and identifying metadata. It is stored directly as an MP4, not through Git LFS.

## Scope

The computational instances assume aligned, compatible objects, additive heights, intact delivery and available receivers. The supplied analytical inputs do not establish robot reachability, continuous collision avoidance, payload admissibility or stack stability. Physical deployment requires motion and grasp validation and calibrated durations.

## Integrity and reuse

The original text instances are byte-for-byte copies of the experimental inputs. `instances/CATALOG.json` records their SHA-256 hashes, and `SHA256SUMS.txt` covers all distributed files.

## Licence and attribution

The dataset, metadata, documentation and physical demonstration video in this repository are licensed under the [Creative Commons Attribution 4.0 International licence (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). The full licence is provided in [LICENSE](LICENSE).

You may share and adapt the material, including for commercial purposes, under the licence terms. Give appropriate credit, link to the licence and indicate any changes. The material is provided without warranties as described in the licence.

During double-blind review, the designated attribution is **Anonymous authors**. Suggested attribution:

> Anonymous authors (2026). Robotic multi-object collection benchmark: dataset, documentation and physical demonstration video. CC BY 4.0. https://anonymous.4open.science/r/cmorp-dataset-2641/

Author names and publication details can be added after review.
