#Mathematical model:

The software is based on a coupled model of the crowd dynamics and the spread of an infectious disease.

##1. Crowd dynamics

The model for the pedestrian motion in evacuation scenarios -- called pFlow -- has been developed in a series of projects since 2012 by Rebekka Axthelm and the industrial partners PerEx GmbH and ASE AG. It is deduced from the pedestrian flow model by R. Hughes (2002) and relies on the following assumptions:

- Persons want to reach the nearest exit (or some other destination). This task determines the direction of the pedestrian flow.
- Persons want to minimize their travel time.
- The speed only depends on the density of the surrounding pedestrians.

The model describes the crowd as a fluid where persons and their behavoir are interchangeable. This idea is derived from thermodynamics where the macroscopic model is deterministic while the microscopic view of single particles is always statistical. This assumes that the pedestrian crowd as a whole behaves rationally and follows the rules stated above while it must not be the case that each individual behaves in this way. The simulation results shall be the better the greater the number of simulated pedestrians.
The crowd dynamics are therefore described by the density ρ at a given time t and location $(x,y)$ and the speed $u=(u_1,u_2)$ (as two-dimensional vector) at a given time $t$ and location $(x,y)$.

The governing equations are the continuity equation (known from fluid mechanics) which states that the net flow of pedestrians into a small region (given by the divergence) equals the accumulation (or loss) of the pedestrians in this region (given by the time derivative)

$ρt+div(ρu)=0$

and the eikonal equation (known from optics) which computes the minimal amount of time required to travel to the boundary (in our case: exit) where the speed only depends on the local densitiy of the crowd:

$-|\nabla \Phi| = \frac{1}{f(\rho)} $

where $f(ρ)$ is a (given) function which relates density to speed (as scalar).



Inline equation: $equation$

- $$x + y$$
- $x - y$
- $x \times y$ 
- $x \div y$
- $\dfrac{x}{y}$
- $\sqrt{x}$

\begin{equation*}
J(\theta) = \frac 1 2 \sum_{i=1}^m (h_\theta(x^{(i)})-y^{(i)})^2
\end{equation*}

\begin{align}
J(\theta) &= \frac 1 2 \sum_{i=1}^m (h_\theta(x^{(i)})-y^{(i)})^2\\
J &= \int\limits_\Omega f~dx
\end{align}

