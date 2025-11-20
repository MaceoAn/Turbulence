Turbulent Channel Flow — DNS vs RANS Study

This project analyses the turbulent flow between two parallel plates using three approaches:
	•	DNS (Direct Numerical Simulation) using reference data at $Re_\tau = 5200$
	•	RANS (Reynolds-Averaged Navier–Stokes) with the k–ε model using ANSYS Fluent
	•	Mixing-length model (Prandtl, 1925) for theoretical comparison

The objective is to compare velocity profiles, turbulent quantities, and stress distributions between the three approaches, and assess the performance and limitations of turbulence models.

⸻

🎯 Objectives
	•	Understand the fundamentals of turbulent channel flows
	•	Use DNS data as a reference to compute:
	•	velocity profile
	•	Reynolds stresses
	•	turbulence production $P$
	•	dissipation rate $\varepsilon$
	•	Implement the Prandtl mixing-length model
	•	Run a k–ε RANS simulation on Fluent
	•	Compare DNS / RANS / theoretical profiles

⸻

📘 Scientific Background

Turbulent kinetic energy (TKE)

The velocity is decomposed as:

$$
u_i = \bar{u}_i + u’_i
$$

The mean kinetic energy becomes:

$$
\bar{e}_c = \frac{1}{2}(\bar{u}_i^2 + \overline{u’_i u’_i})
$$

⸻

RANS equations

Starting with incompressible Navier–Stokes:

$$
\frac{\partial u_i}{\partial x_i} = 0
$$

$$
\frac{\partial u_i}{\partial t} + u_j \frac{\partial u_i}{\partial x_j}
= -\frac{1}{\rho}\frac{\partial p}{\partial x_i} + \nu \frac{\partial^2 u_i}{\partial x_j^2}
$$

Reynolds decomposition yields:

$$
\bar{u}_j \frac{\partial \bar{u}_i}{\partial x_j}
= -\frac{1}{\rho} \frac{\partial \bar{p}}{\partial x_i}
	•	\nu \nabla^2 \bar{u}_i

	•	\frac{\partial \overline{u’_i u’_j}}{\partial x_j}
$$

⸻

Closure problem

The Reynolds stress tensor introduces 6 new unknowns → turbulence models required.

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

Using the dataset LM_Channel_5200_prof.txt, we compute:

✔ Friction velocity

$$
u_\tau = 0.78 , \text{m/s}
$$

✔ Velocity profile

Expected log-law:

$$
\frac{\bar{u}}{u_\tau} =
\frac{1}{\kappa} \ln\left( \frac{y}{l_\tau} \right) + B
$$

✔ Turbulence production

$$
P = - \overline{u’_x u’_y} \frac{\partial \bar{u}}{\partial y}
$$

✔ Dissipation

$$
\varepsilon = 2 \nu S’{ij} S’{ij}
$$

Figures (DNS):
	•	mean velocity profile
	•	TKE production
	•	TKE dissipation

⸻

🛠️ RANS Simulation (k–ε)

Performed in ANSYS Fluent:
	•	incompressible flow
	•	2D statistically steady channel
	•	wall boundary conditions
	•	symmetry at mid-plane
	•	normalization using $u_\tau$ and $h$

Validation steps:
	•	residual convergence
	•	shear-stress integral convergence
	•	verification of fully developed region

Extracted quantities:
	•	mean velocity
	•	Reynolds stresses
	•	turbulent viscosity
	•	$k$, $\varepsilon$, $P$

⸻

📊 DNS vs RANS Comparison

Key observations:
	•	RANS aligns well with DNS in the logarithmic region
	•	Near-wall behavior deviates due to k–ε limitations
	•	Turbulent viscosity overpredicted at small $y^+$
	•	Production and dissipation peaks displaced between models
	•	DNS resolves structures that RANS cannot capture

⸻

🧰 Repository Structure
