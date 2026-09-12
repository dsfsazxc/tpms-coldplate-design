# Method overview

## 1. Define the cooling problem

The design core measures 72 x 72 x 12 mm. A 12 x 12 in-plane field controls the local porosity coordinate, with the same design repeated through the two unit-cell layers. The reference numerical dataset uses 10.4 W total heating, 1 L/min coolant flow, and a 298.15 K inlet temperature. Heat-source positions and inlet/outlet arrangements vary between problems.

This reference load defines a numerical comparison; it is not presented as a high-power electronics qualification test.

## 2. Connect cellular geometry to plate-scale physics

The local TPMS geometry determines effective hydraulic and thermal properties. Unit-cell results are tabulated and used by a homogenized model, so optimization does not require resolving every pore at every iteration.

The thermal model distinguishes solid and fluid temperatures using a local thermal nonequilibrium formulation. Flow and thermal fields determine the objective and constraints. Adjoint sensitivities provide gradients for material redistribution, and the method of moving asymptotes (MMA) updates the design.

## 3. Predict an initial design

The design network receives the heat map, port information, current design, and progress coordinate. A shared CNN with dilated convolutions updates the design four times. At each stage, a fixed U-Net flow surrogate supplies eight flow-feature channels computed from the current design.

All four stages are differentiated together during training, allowing the final prediction error to influence earlier updates. There are no intermediate PDE solves during this neural rollout. The design CNN has 48,292 parameters and the flow surrogate has 40,697 parameters. Training and evaluation use a fixed 12 x 12 grid; no resolution-independent operator claim is made.

## 4. Transfer and refine

The final proposal must satisfy bounds and the material-volume constraint after the solver's design filter. The physical porosity field used by the solver can therefore differ from the direct neural output. Adjoint-MMA refinement then operates on the transferred design.

The comparison measures the simulation work needed to reach a prescribed numerical target, rather than assuming that a lower design prediction error implies a faster optimization.

## 5. Verify beyond the reduced model

Resolved TPMS CFD and fabricated specimens address questions that the homogenized model alone cannot settle: local flow details, peak-temperature mesh sensitivity, pressure loss in the realized geometry, and experimental thermal performance. Those validation stages must not be inferred from the neural prediction results.
