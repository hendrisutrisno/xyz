# Object-Picking Dataset

This dataset contains 40 maps: eight maps for each N = 10, 20, 40, 60 and 80. Each size has four item-height distributions and two scattered layouts per distribution.

| File indices | Height distribution | Definition |
|---|---|---|
| 1, 2 | Uniform | Equal probabilities across all height classes |
| 3, 4 | Normal | Discretized, truncated normal: mean parameter 7 cm, SD parameter 1.5 cm |
| 5, 6 | Exponential | Discretized, truncated exponential on h - 4; rate 0.5 per cm |
| 7, 8 | Reverse exponential | Mirror of exponential: h_reverse = 14 - h; taller items are more frequent |

Heights are 4, 4.2, ..., 10 cm. Class probabilities are proportional to 1, exp(-0.5*((h-7)/1.5)^2), exp(-0.5*(h-4)), or exp(-0.5*(10-h)), respectively. For each N, midpoint quantiles (k+0.5)/N are mapped through the discrete cumulative distribution. Counts therefore approximate these distributions at finite N; each class cannot be present in an N=10 map with 31 possible heights. The reverse-exponential histogram is the exact mirror of the exponential histogram.

## Spatial design

Two scattered coordinate layouts are used at each N. Odd indices share layout 1; even indices share layout 2. Coordinates and required destinations are paired across the four height profiles within a layout. Height multisets are the same across the two layouts, with independently shuffled assignments. Destination labels are balanced (N/2 A and N/2 B) and shuffled separately from heights.

There are no color-specific or height-specific regions. Assignments are randomized with seed 20261106 and accepted only when absolute Pearson correlations of the attribute with x and y are at most 0.50 for N=10 and 0.25 otherwise. Each quadrant containing at least four items has an attribute mean within 0.8 population standard deviations of the full-map mean. These finite-sample mixing checks do not imply perfect statistical independence or remove every chance local grouping.

The allowed workspace consists of annular sectors: radius 0.26 to 0.65 m and theta = atan2(x,-y) in [15,165] or [195,345] degrees after normalization. Full 5 x 5 cm footprints lie inside this workspace and do not overlap. Center spacing is at least 0.07 m subject to 0.0015 m input-rounding tolerance.

## File format

Files are named N10_1.txt through N10_8.txt, similarly for the other sizes. The first line is the filename stem prefixed by #, for example #N10_1. Remaining lines contain six whitespace-separated columns:

```text
object_id x_m y_m z_center_m height_cm destination_id
```

XYZ coordinates use meters; individual height uses centimeters. Preserve leading zeros in object IDs. Objects rest on z=0 and z_center_m=height_cm/200. Receiving stations are A=(0,-0.45,0) m and B=(0,0.45,0) m. The receiving surface and pickup surface share the same elevation. Repeated deliveries require automatic station clearing. A 0.2 cm height quantum represents every object height exactly.

CATALOG.json records file checksums and assignments; COLLECTION_VALIDATION.json records geometry, histogram and spatial mixing checks. These 40 maps are the complete dataset collection. No robot reachability, collision, payload or stability certificate is implied by the dataset.
