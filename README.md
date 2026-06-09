# Crime-Data-Analysis-And-Visualisation-System

An interactive data visualisation project built with Python and Altair. It presents
three multiview dashboards that explore the same Los Angeles crime dataset, each
implementing the same set of analytical tasks through different visual and
interaction designs.

This was a group project (5 students) completed for the MSc Information
Visualisation course at the University of Glasgow.

**Live demo:** [https://fouziasharkar.github.io/Crime-Data-Analysis-And-Visualisation-System/](https://fouziasharkar.github.io/Crime-Data-Analysis-And-Visualisation-System/dashboard.html)

---

## Overview

The aim of the project is to compare visualisation designs. All three systems use
the same data and support the same six tasks, so the only thing that differs is the
design. This makes it possible to evaluate which design choices work best for each
task.

The data is the Los Angeles Police Department's public crime dataset (2020–present),
cleaned and reduced to a sample of 10,000 incidents. The six tasks cover:

1. Temporal trends — patterns and spikes over time.
2. Spatial distribution — geographic hotspots.
3. Crime categories — comparing the frequency of different crime types.
4. Victim demographics — age and sex in relation to crime type.
5. Interactive selection — filtering and brushing to explore subsets.
6. Linked views — comparing a selected subset against the full dataset.

## The three systems

Each system is a multiview dashboard with coordinated (linked) charts. Selecting or
brushing in one view updates the others.

| | Spatial view | Temporal view | Categories | Demographics |
|---|---|---|---|---|
| **System A** | Binned grid heatmap | Area and line chart | Horizontal bars | Age histogram and sex bars |
| **System B** | Point map | Calendar heatmap | Top-15 bars | Age groups and sex bars |
| **System C** | Point map | Area chart | Horizontal bars | Age × crime heatmap and share bars |

All three dashboards are self-contained HTML files. The data is embedded and the
required libraries load from a CDN, so they run in any browser with no setup.

## Generalised selection (System B)

System B includes an additional feature: generalised selection. The dataset has a
natural two-level hierarchy — each incident belongs to one area. After clicking a
single incident on the map, the user can "generalise" the selection to include every
incident in that same area, and switch back again.

Since Vega-Lite does not support this directly, it was implemented by:

- building an incident-to-area lookup to represent the hierarchy,
- using a parameter to switch the active chart layers, and
- updating the area selection through the Vega view API so all linked views respond
  together.

This is true generalised selection (moving up a hierarchy), not a global filter over
the whole dataset.

## My contribution

This was a group of five. My responsibilities were:

- **Data cleaning and preprocessing** — the shared pipeline used by all three
  systems, including handling missing values, validating victim age and sex,
  classifying crime categories, parsing dates, and producing the cleaned 10,000-row
  sample.
- **System B** — designed and built in full, including the generalised-selection
  feature described above.
- **User evaluation** — the comparative study across all three systems.

Systems A and C, and the overall project assembly, were completed by other members
of the group.


## Technologies

Python, Altair (which compiles to Vega-Lite), pandas, NumPy, and vl-convert.
