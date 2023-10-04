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

\begin{equation*}
\Huge \varrho_t+\nabla\cdot(\varrho\,u)=0
\end{equation*}


and the eikonal equation (known from optics) which computes the minimal amount of time required to travel to the boundary (in our case: exit) where the speed only depends on the local densitiy of the crowd:

\begin{equation*}
-|\nabla \Phi| = \frac{1}{f(\varrho)} 
\end{equation*}


where $f(\varrho)$ is a (given) function which relates density to speed (as scalar).

It is called "fundamental diagram", and there exist a lot of different propositions in the literature how it looks like, none of them fully accepted, but some of them verified in important scenarios. The scalar field Φ can be interpreted as a potential which describes the time it takes to reach from a given location (x,y) the boundary of the domain. The velocity field of the crowd is then given by 

\begin{equation*}
u=−f(\varrho)\,\frac{\nabla \Phi}{|\nabla\Phi|}
\end{equation*}
