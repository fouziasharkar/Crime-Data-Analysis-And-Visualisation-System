# Crime Data Analysis and Visualisation System

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
the same data and support the same set of tasks, so the only thing that differs is
the design. This makes it possible to evaluate which design choices work best for
each task.

The data is the Los Angeles Crime Incidents dataset (reported crimes, 2020–2025).
It contains roughly one million records across 28 attributes — a moderately large,
high-dimensional dataset combining categorical, quantitative, spatial, and temporal
attributes. For the dashboards it was cleaned and reduced to a sample of 10,000
incidents.

The tasks the systems support are:

1. **Identify temporal trends** — patterns and changes in reported crime over time.
2. **Compare crime categories and victim characteristics** — how crime types relate to victim age and sex.
3. **Investigate a subset of incidents** — filter to a specific group and locate patterns within it.
4. **Identify spatial patterns** — geographic clusters and hotspots.
5. **Explain multiview trends** — combine spatial, temporal, and categorical views to find relationships.

## The three systems

Each system is a multiview dashboard with coordinated (linked) charts. Selecting or
brushing in one view updates the others.

| | Spatial view | Temporal view | Categories | Demographics |
|---|---|---|---|---|
| **System A** | Binned density heatmap | Monthly line chart | Aggregated category bars | Age histogram and sex bars |
| **System B** | Individual point map + area summary | Year × month heatmap | Crime-description dot plot | Age groups and sex bars |
| **System C** | Point map with filter controls | Area chart | Ranked bars with group filter | Age × crime-group heatmap and share bars |

All three dashboards are self-contained HTML files. The data is embedded and the
required libraries load from a CDN, so they run in any browser with no setup.

## Generalised selection (System B)

System B includes a generalised-selection feature. The dataset has a natural
two-level hierarchy — each incident (identified by its DR_NO) belongs to one LAPD
reporting area. After clicking a single incident on the map, the user can
"generalise" the selection to include every incident in that same area, then switch
back again.

Since Vega-Lite does not support this directly, it was implemented by:

- building a `DR_NO → AREA NAME` lookup to represent the hierarchy,
- using a boolean parameter to switch the active chart layers, and
- injecting the parent area into the area selection through the Vega view API so all
  linked views respond together.

This is true generalised selection — moving one level up a hierarchy from a selected
item — rather than a global filter applied to the whole dataset.

## My contribution

This was a group of five. My responsibilities were:

- **Data cleaning and preprocessing** — the shared pipeline used by all three
  systems, including handling missing values, validating victim age and sex,
  classifying crime categories, parsing dates, and producing the cleaned 10,000-row
  sample.
- **System B coding** — the incident-based visualisation logic, brushing and
  linking, and the generalised-selection mechanism described above. The overall
  dashboard layout and integration were built by another team member.
- **Evaluation analysis and write-up** — analysed the user-study results and wrote
  the Evaluation and Future Work sections of the report. The evaluation form and
  data collection were carried out by another team member.

Systems A and C were built by other members of the group.


## Technologies

Python, Altair (which compiles to Vega-Lite), pandas, NumPy, and vl-convert.
