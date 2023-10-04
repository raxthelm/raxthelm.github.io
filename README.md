# The mathematical model

The software is based on a coupled model of the crowd dynamics and the spread of an infectious disease.

##1. Crowd dynamics

The model for the pedestrian motion in evacuation scenarios -- called pFlow -- has been developed in a series of projects that were launched 2012 by Rebekka Axthelm and the industrial partner ASE AG. It is deduced from the pedestrian flow model by R. Hughes (2002) and relies on the following assumptions:

---
** _hypotheses_ ** 

- Persons want to reach the nearest exit (or some other destination). This task determines the direction of the pedestrian flow.
- Persons want to minimize their travel time.
- The speed only depends on the density of the surrounding pedestrians.

---

The model describes the crowd as a fluid where persons and their behavoir are interchangeable. This idea is derived from thermodynamics where the macroscopic model is deterministic while the microscopic view of single particles is always statistical. This assumes that the pedestrian crowd as a whole behaves rationally and follows the rules stated above while it must not be the case that each individual behaves in this way. The simulation results shall be the better the greater the number of simulated pedestrians.
The crowd dynamics are therefore described by the density ρ at a given time t and location $(x,y)$ and the speed $u=(u_1,u_2)$ (as two-dimensional vector) at a given time $t$ and location $(x,y)$.

The governing equations are the continuity equation (known from fluid mechanics) which states that the net flow of pedestrians into a small region (given by the divergence) equals the accumulation (or loss) of the pedestrians in this region (given by the time derivative)

---
** _continuity-equation_ ** preservation of human mass

\begin{equation*}
\varrho_t+\nabla\cdot(\varrho\,u)=0
\end{equation*}

---

and the eikonal equation (known from optics) which computes the minimal amount of time required to travel to the boundary (in our case: exit) where the speed only depends on the local densitiy of the crowd:

---
** _eikonal-equation_ ** decision of walk direction

\begin{equation*}
-|\nabla \Phi| = \frac{1}{f(\varrho)} 
\end{equation*}
---


<table width="100%" border="0">
    <tr>
        <td width="50%" align="center"><figure align="center"><img width="100%" src="pics/fd.png" alt="Fundamentaldiagramm"><figcaption>Figure 2: Fundamentaldiagramm</figcaption></figure></td>
        <td width="50%" align="left">where $f(\varrho)$ is a (given) function which relates density to speed (as scalar).

It is called _fundamental diagram_, and there exist a lot of different propositions in the literature how it looks like, none of them fully accepted, but some of them verified in important scenarios. The scalar field $\Phi$ can be interpreted as a potential which describes the time it takes to reach from a given location $(x,y)$ the boundary of the domain. The velocity field of the crowd is then given by 

        </td>
    </tr>
</table>

where $f(\varrho)$ is a (given) function which relates density to speed (as scalar).

It is called _fundamental diagram_, and there exist a lot of different propositions in the literature how it looks like, none of them fully accepted, but some of them verified in important scenarios. The scalar field $\Phi$ can be interpreted as a potential which describes the time it takes to reach from a given location $(x,y)$ the boundary of the domain. The velocity field of the crowd is then given by 

---
** _velocity-field_ ** speed and walking direction of the crowd

\begin{equation*}
u=−f(\varrho)\,\frac{\nabla \Phi}{|\nabla\Phi|}
\end{equation*}
---

During the project the pedestrian flow model must be extended to non-evacuation scenarios and combined with measurements to replace simulation results and/or to fit parameters of the equations.


##2. Spread of infectious disease

The classical model to describe the spread of an infectious disease is a compartmental model called SEIR model. It was originally developed by W. Kermack and A. McKendrick (1927) as SIR-model. The population is divided into four compartments, the susceptible ($S$), the exposed ($E$), the infectious ($I$) and the recovered ($R$), and differential equations govern the flow of people from one compartment to the other:
Let $S(t)$ be the individuals not yet infected, but susceptible to the disease, $E(t)$ the individuals exposed to the disease but not yet infectious, $I(t)$ the infected and infectous individuals and $R(t)$ the recovered (or died) individuals at time $t$. One usually assumes that the number of individuals is constant, that is 

$$N=S(t)+E(t)+I(t)+R(t).$$

It is further assumed that each infectious individual has the same number of contacts per unit time, e.g. each infectious person meets 10 persons per hour. Not all of them are susceptible, but only $S(t)/N$ percent, e.g. 80%. Then each infectious person meets (at average) $10 \cdot 80\% = 8$ susceptible persons. Not each contact leads to an infection, but only fractional part, e.g. only $15\%$ of contacts leads to an infection, so in our example we get that each infectious person infects $15\% \cdot 10 \cdot 80\% = 1.2$ persons. One denotes the product of the probability of infection per contact and the contact rate (number of contact persons per unit time) with $\beta$ (e.g. here $15\%\cdot 10=0.15$), and under these assumptions one obtains that the number of susceptible diminishes in each unit time by $−\beta S(t)/N(t)\cdot I(t)$:

$$S(t+1)−S(t)=−\beta\,\frac{S(t)}{N}\,I(t)$$

In the same way the other three differential equations are derived where $1/a$ is the average latency period (that is the time period between being exposed and being infectious), $\gamma$ is the average recovery rate (or $1/\gamma$ the mean infective period). We assume that the population in the considered time span is constant so that no new, susceptible individuals enter the system:



---
** _SEIR-Modell_ **

\begin{align*}
E′(t)&=\beta\,\frac{S(t)}{N}\,I(t)−a\,E(t)\\
I′(t)&=a\,E(t)−\gamma\,I(t)\\
R′(t)&=\gamma\,I(t).
\end{align*}

---

We see that the population flows from susceptible with rate $beta\,S(t)/N$ to exposed, from exposed with rate a to infectious and from infectious with rate $\gamma$ to recovered. The basic reproduction number would be computed as $R_0=\beta/\gamma$ as fraction from exposition and recovery rate

The system has only one equilibrium state (if there are no new individuals entering the system) that no one is infected, that is $S+R=N$, $E=I=0$.

The classical SEIR model supposes that the contact rate is constant for each infected persons and that the four groups are everywhere homogeneously mixed such that the probability to meet a susceptible person is everywhere for everyone the same. The movements of people do not count. Therefore, the model does not allow to simulate local infections but only the global number of infections of the whole population. As we are interested in the interplay of pedestrian motion and spread of infections we develop a localised version of the SEIR model where for example infectious persons can locally accumulate and the time span that a susceptible persons spends close to an infected person counts. 





##Literature

Kermack, W. O., & McKendrick, A. G. (1927) A contribution to the mathematical theory of epidemics. Royal Sociaty 115, 772. [https://doi.org/10.1098/rspa.1927.0118](https://doi.org/10.1098/rspa.1927.0118)

Hughes: [https://linkinghub.elsevier.com/retrieve/pii/S0191261501000157](https://linkinghub.elsevier.com/retrieve/pii/S0191261501000157)





