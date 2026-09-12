# Selected numerical results

## Design prediction

The models were trained using a corpus of 817 optimization trajectories, with separate fitting and tuning subsets. Development comparisons use 168 trajectories grouped into 52 near-duplicate-safe problem groups and three training seeds. Results are averaged by group before aggregation.

| Model | Design RMSE |
| :--- | ---: |
| CNN-only, four stages | 0.02846 |
| Flow-informed, one stage | 0.02984 |
| Flow-informed, four stages | **0.02585** |

Flow-informed four-stage prediction reduces error by 9.2% relative to CNN-only four-stage prediction, and by 13.4% relative to the flow-informed one-stage model. The first comparison has a paired mean difference of -0.00261, with a 95% interval of [-0.00338, -0.00181].

These values measure the corrected neural design before the additional solver-side filtering. They are dimensionless porosity-field errors, not temperature errors. The development set was used for model comparisons; it is not a final untouched test set.

## Work to the reference target

Twelve problems were evaluated with the same flow and material-volume conditions and one training seed. All four methods reached the reference target in 11 problems. One problem had no numerically established reference target and remains in the reported 12-problem population.

| Initial design | Target reached | Mean PDE solves to target, including native checks |
| :--- | :---: | ---: |
| Uniform | 11/12 | 104.7 |
| CNN-only, four stages | 11/12 | 36.4 |
| Flow-informed, one stage | 11/12 | 30.0 |
| Flow-informed, four stages | 11/12 | 31.9 |

Means use the same 11 evaluable problems. The target is defined from numerically eligible states of the uniform-start trajectory, not from an assumed exact global optimum. Native checks use the production mesh; no finer-mesh confirmation was completed in this cost study.

The flow-informed four-stage model used fewer solves than the uniform start in all 11 evaluable problems. The mean paired difference was -72.8 solves, with a 95% interval of [-82.4, -63.0]. This is about 69.5% fewer solves relative to the uniform-start mean.

However, its difference from CNN-only initialization was -4.5 [-14.9, +4.3], and from flow-informed one-shot initialization was +1.9 [-9.0, +12.4]. Neither comparison established an additional computational saving. **The demonstrated saving is a benefit of learned initialization generally, not an isolated benefit of the flow surrogate.**

One of the 11 eligible targets is sensitive to unresolved lower-temperature reference states. As a sensitivity check, excluding that problem leaves about 67.5% fewer solves for the flow-informed four-stage model versus uniform initialization. This does not resolve the underlying mesh uncertainty.

## What remains open

- Peak-temperature and numerical-screen mesh sensitivity.
- Resolved-geometry CFD comparisons using matched geometry and boundary conditions.
- Fabrication and experimental comparisons at appropriate heat loads.
- Broader operating conditions and repeated training seeds for the physical-cost study.

The current results support a simulation-assisted design workflow. They do not establish a universal optimum, a manufacturing guarantee, or an experimentally verified cooling improvement.
