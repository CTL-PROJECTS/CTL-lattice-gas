General information about the CTL course available at https://ctl.polyphys.mat.ethz.ch/

# :wave: PROJECT lattice gas

## Part I. Diffusion in regular 2D grid model where particles try to hop randomly, and only hop if the site is empty

Consider $n$ random walkers, i.e., a nonzero concentration of $n/N^2$ random walkers (particle) on a square $N\times N$ lattice. Each lattice site can either be occupied by a particle (value $1$), or empty (value $0$); the status of each site is therefore represented by a single bit. Each of the $n$ particles moves (one after the other) at random to empty nearest-neighbor sites but double occupancy of a site is forbidden. Otherwise, the particles are non-interacting. Such model is an example of a ``lattice gas''. Note that the motion of an individual particle is correlated with the motion of the other particles. The physical motivation of this model arises from metal physics where diffusion is caused by thermal vacancies with a concentration that depends on the temperature. The main quantity of interest is the self-diffusion constant $D$ of an individual particle. 

The algorithm for a Monte Carlo simulation can be stated as follows:

1. create an empty $N\times N$ array (LAT), and turn $n$ sites (=particles) from 0 to 1 (occupied) at random. Assign a unique particle number $j=1,2,..,n$ to each of the occupied sites. Each lattice site has a position, particle $j$ is therefore initially at some position ${\bf r}_j(0)$. Set time $t=0$.
2. Increase $t$ by $1$. 
3. pick one of $n$ particles at random, and one of its 4 neighboring sites at random. Particles at the border of the $N\times N$ region have their neighbors over the boundary. For example, if the corners of the square lattice are at $(1,1)$, $(1,N)$, $(N,1)$, and $(N,N)$, a particle located at grid position $(3,N)$ has neighbors at $(3,1)$, $(3,N-1)$, $(2,N)$, and $(4,N)$. If the neighboring site is empty, the particle is moved to this site, otherwise, the particle remains in the present position. Do all this $N$ times in a row (not in parallel), i.e., pick $N$ times in total. You end up with new positions ${\bf r}_j(t)$ for all particles. Calculate $D(t)$ (defined below) and return this value
4. Continue with 2. until some user-defined time (such as $t=100$) has been reached

The measure of time in this context is arbitrary. The usual definition is that one unit of time corresponds to one Monte Carlo step per particle. During each of these steps, each particle attempts one jump on the average. The diffusion coefficient $D$ is obtained as the limit $t\rightarrow \infty$ of $D(t)$, where $D(t)$ is given by $D(t) = \langle [{\bf r}_j(t)-{\bf r}_j(0)]^2 \rangle / 2td$, with $d$ denoting the dimension of space (here, $d=2$). 
The average brackets $\langle..\rangle$ stand for an average over all particles $j\in \{1,..,n\}$.

### Task 1

Plot $D(t)$ versus time $t$ and extract a steady state value $D$ (for parameters $N=10$, $n=20$). 

### Task 2

Determine steady state values $D$ for various concentrations and plot $D$ versus concentration. 


## Part II. The one-dimensional 1D3Px lattice-gas model



Here we consider the simplest lattice-gas model of a one-dimensional fluid with two conserved
quantities: mass and momentum. This is called the 1D3Px lattice-gas model. This model was first studied by Qian in 1990
[1,2]. The lattice gas is residing on one-dimensional grid with $N=1024$ sites (subject to periodic boundary conditions), where each site $j\in\{1,..,N\}$ is encoded by three bits, $(n_{-1},n_0,n_1)$. Each of the three bits can be either $0$ or $1$. If $n_0=1$, the site carries a rest particle with mass two, if $n_{-1}=1$, the site carries a particle with mass one and negative unit speed, if $n_{1}=1$, the site carries a particle with mass one and positive unit speed. The mass at a site is $m=2n_0+n_{-1}+n_1$ and the momentum of a site is $p=n_1-n_{-1}$. There are exactly two local configurations both with mass $2$ and zero total momentum: $(0,1,0)$ and $(1,0,1)$. 

The algorithm proceeds as follows: 

1. Initialize each of the $N=1024$ sites randomly with three bits $\in\{0,1\}$ while making sure that the total momentum is zero. Calculate the total mass. 
2. Apply a collision rule to each of the sites simulataneously: If the state of the site is $(0,1,1)$, convert it to $(1,0,0)$. If the state is $(1,0,0)$, convert it to $(0,1,1)$.
3. Apply a streaming rule to each of the sites simultaneously: If a site carries a particle with negative velocity, move this particle to the left neighboring site, with unchanged velocity. Similarly, if a site carries a particle with positive velocity, move this particle to the right neighboring site at unchanged velocity. If the left or right neighboring site exceeds the grid, use the opposing boundary instead.
4. Calculate the total momentum and total mass and check if they remained at their initial values (from 1.). Deactivate this part of your code if it passed this test successfully.
5. Calculate a coarse-grained mass density profile with 8 values. Each value is an average over 128 adjacent sites from the grid with $N=1024 = 8 \times 128$ sites.
6. Continue at 2. until a number of iterations (say, 100 iterations) has been done. 


[1] Yue Hong Qian. Gaz sur Reseaux et Théorie Cinétique sur Réseaux Appliquée a l'Equation de Navier-Stokes. PhD thesis, Universite De Paris, L’Ecole Normale Superieure, Departement De Physique, 1990.

[2] https://apps.dtic.mil/sti/pdfs/ADA455835.pdf
