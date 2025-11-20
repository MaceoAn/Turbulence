Turbulent Channel Flow — DNS vs RANS Comparative Study

A detailed analysis of turbulent channel flow using three modelling approaches:
	•	DNS (Direct Numerical Simulation) — reference dataset at $Re_\tau = 5200$
	•	RANS (k–ε model) — solved with ANSYS Fluent
	•	Mixing-length theory — classical Prandtl model

The goal is to quantitatively compare velocity profiles, Reynolds stresses, turbulence production, and dissipation, in order to evaluate the strengths and limitations of turbulence models.

⸻

📑 Table of Contents
	•	Objectives￼
	•	Scientific Background￼
	•	TKE￼
	•	RANS equations￼
	•	Closure problem￼
	•	Mixing-length model￼
	•	k–ε model￼
	•	DNS Analysis￼
	•	RANS Simulation￼
	•	DNS vs RANS Comparison￼
	•	Repository Structure￼

⸻

🎯 Objectives
	•	Understand turbulent channel flow fundamentals
	•	Use DNS data to compute:
	•	mean velocity profile
	•	Reynolds stresses
	•	turbulence production $P$
	•	dissipation rate $\varepsilon$
	•	Implement the Prandtl mixing-length model
	•	Perform a k–ε RANS simulation
	•	Compare DNS, RANS, and theoretical predictions

⸻

📘 Scientific Background

Turbulent kinetic energy (TKE)

Velocity decomposition:

$$
u_i = \bar{u}_i + u’_i
$$

Mean kinetic energy:

$$
\bar{e}_c = \tfrac{1}{2}\big(\bar{u}_i^2 + \overline{u’_i u’_i}\big)
$$

⸻

RANS equations

Incompressible continuity:

$$
\frac{\partial u_i}{\partial x_i} = 0
$$

Momentum:

$$
\frac{\partial u_i}{\partial t}
	•	u_j \frac{\partial u_i}{\partial x_j}
= -\frac{1}{\rho}\frac{\partial p}{\partial x_i}
	•	\nu \frac{\partial^2 u_i}{\partial x_j^2}
$$

Reynolds-averaged form:

$$
\bar{u}_j \frac{\partial \bar{u}_i}{\partial x_j}
= -\frac{1}{\rho} \frac{\partial \bar{p}}{\partial x_i}
	•	\nu \nabla^2 \bar{u}_i

	•	\frac{\partial \overline{u’_i u’_j}}{\partial x_j}
$$

⸻

Closure problem

The Reynolds stress tensor introduces 6 unknowns, requiring a turbulence model.

⸻

Mixing-length model

$$
\nu_t = l_m^2 \left| \frac{\partial \bar{u}}{\partial y} \right|
$$

$$
l_m = \kappa y
$$

⸻

k–ε model

$$
\nu_t = C_\mu \frac{k^2}{\varepsilon}
$$

⸻

🧪 DNS Analysis

Dataset used: LM_Channel_5200_prof.txt

Friction velocity

$$
u_\tau = 0.78 , \text{m/s}
$$

Mean velocity profile

Expected logarithmic law:

$$
\frac{\bar{u}}{u_\tau}
= \frac{1}{\kappa} \ln\left(\frac{y}{l_\tau}\right) + B
$$

Turbulence production

$$
P = -\overline{u’_x u’_y} , \frac{\partial \bar{u}}{\partial y}
$$

Dissipation

$$
\varepsilon = 2\nu S’{ij} S’{ij}
$$

Figures include:
	•	Velocity profile
	•	TKE production
	•	TKE dissipation

⸻

🛠️ RANS Simulation (k–ε)

Simulation performed in ANSYS Fluent:
	•	Incompressible, fully developed channel flow
	•	2D statistically steady model
	•	No-slip walls
	•	Symmetry at centerline
	•	Normalization with $u_\tau$ and $h$

Validation:
	•	residual convergence
	•	shear stress integral check
	•	verification of fully developed region

Extracted quantities:
	•	mean velocity
	•	Reynolds stresses
	•	turbulent viscosity
	•	$k$, $\varepsilon$, $P$

⸻

📊 DNS vs RANS Comparison

Key findings
	•	Velocity profile: good agreement in log region
	•	Near-wall region: k–ε overpredicts viscosity → flattening of profile
	•	Turbulent viscosity: large deviations for $y^+ < 30$
	•	Production/dissipation peaks: shifted relative to DNS
	•	DNS captures structures absent in RANS due to averaging

⸻

🧰 Repository Structure
