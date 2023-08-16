General information about the CTL course available at https://ctl.polyphys.mat.ethz.ch/

# :wave: PROJECT lattice gas

## Part I. Diffusion in regular grid model where particles try to hop randomly, and only hop if the site is empty

Consider a nonzero concentration of n/N<sup>2</sup> random walkers (particle) on a square N $\times$ N lattice. Each of the n particles moves (one after the other) at random to empty nearest-neighbor sites but double occupancy of a site is forbidden; otherwise, the particles are non-interacting. Such model is an example of a ``lattice gas''. Note that the motion of an individual particle is correlated with the motion of the other particles. The physical motivation of this model arises from metal physics where diffusion is caused by thermal vacancies with a concentration that depends on the temperature. The main quantity of interest is the self-diffusion constant <em>D</em> of an individual particle. 

The algorithm for a Monte Carlo simulation can be stated as follows:
1. create empty N x N array (LAT), and turn n sites (=particles) from 0 to 1 (occupied) at random. Assign a unique particle number $j$ to each of the occupied sites. Each lattice site has a position, particle $j$ is therefore at some position ${\bf r}_j(0)$. Set time $t=0$.
2. Increase $t$ by $1$. 
3. pick a particle at random, and a neighboring site at random. If the neighboring site is empty, the particle is moved to this site, otherwise, the particle remains in the present position. Do all this N times in a row (not in parallel), i.e., pick N times in total. You end up with new positions ${\bf r}_j(t)$ for all particles. Calculate D(t) (defined below) and return this value
4. Continue with 2. until some user-defined time has been reached

The measure of time in this context is arbitrary. The usual definition is that one unit of time corresponds to one Monte Carlo step per particle. During each of these steps, each particle attempts one jump on the average. The diffusion coefficient D is obtained as the limit t $\rightarrow \infty$ of D(t), where D(t) is given by D(t) = $\langle ({\bf r}_j(t)-{\bf r}_j(0))^2 \rangle$ / 2td, with d denoting the dimension of space (here, d=2). 
The average brackets $\langle..\rangle$ stand for an average over all particles j $\in$ {1,..,n}.

### Task 1

Plot D(t) versus time t and extract a steady state value D (for parameters N=10, n=20). 

### Task 2

Determine steady state values D for various concentration and plot D versus concentration. 


## Part II. The one-dimensional 1D3Px lattice-gas model

https://apps.dtic.mil/sti/pdfs/ADA455835.pdf

Here we consider the simplest lattice-gas model of a one-dimensional fluid with two conserved
quantities. This is called the 1D3Px lattice-gas model. This model was first studied by Qian in 1990
[1]. The lattice gas is one dimensional and has three bits (n<sub>j</sub> $\in$ {0,1}) per site (n<sub>-1</sub>,n<sub>0</sub>,n<sub>1</sub>),  
a rest particle (j=0) with mass two and speed ±1 particles (j=-1, j=+1) with mass one. There are exactly two local configurations both with mass 2 and zero total momentum: (0,1,0) and (1,0,1). 

| time | site 1| site 2| site 3 |  | site N |
|---|---|---|---|---|---|
| 1 | (0,1,1) | (1,0,0) | (1,0,0) | ... | (1,0,0) |
| 2 | (0,1,1) | (1,1,0) | () | ... | (1,0,1) |
| 2 | (1,0,0) | (0,1,1) | (0,1,1) | ... | (0,1,1) | 

In each step 

2. https://de.wikipedia.org/wiki/FHP-Modell
3. One-dimensional 1D3Px lattice-gas model



[1] Yue Hong Qian. Gaz sur Reseaux et Théorie Cinétique sur Réseaux Appliquée a l'Equation de Navier-Stokes. PhD thesis, Universite De Paris, L’Ecole Normale Superieure, Departement De Physique, 1990.
