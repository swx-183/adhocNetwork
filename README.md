# adhocNetwork
Create a ad hoc network having 10 nodes and a total number of 32 connections.
At each node, generate the data according to the following model:

$$ y_k(n) = \boldsymbol{\theta}_0^T \mathbf{x}_k(n) + \eta_k(n), 1 \leq k \leq 10, $$

where
* $ \boldsymbol{\theta}_0 \in \mathbb{R}^{60} $ is a constant vector, generated via $ N(0,1) $.
* all input vectors $ \mathbf{x}_k(n) \in \mathbb{R}^{60} $ are i.i.d generated via $ N(0,1) $.
* noise samples $ \eta_k(n) \in \mathbb{R}^1 $ are independently generated from zero mean Gaussians with variances corresponding to different signal-to-noise level, varying from 20-25 dBs in each node.

For the unknown vector estimation employ the following algorithms:
* combine-then-adapt diffusion APSM. Parameters: $ \mu_n = 0.5 \times M_n $, $ \epsilon_k = \sqrt 2 \sigma_k $, $ q = 20 $.
* adapt-then-combine LMS. Parameter: step size = 0.03.
* combine-then-adapt LMS. Parameter: step size = 0.03.
* noncooperative LMS. Parameters: choose $ a_{mk} $ according to Metropolis rule:

$$ a_{mk} = \left\{
\begin{aligned}
&\frac{1}{max(n_k,n_m)}, &k \neq m,\ k,\ m\ are\ neighbors, \\
&0, &m \neq k, \\
&1-\sum_{i \neq k} a_{ik}, &m = k.
\end{aligned}
\right.
$$

Run 100 independent experiments and plot the average MSD per iteration in dBs:

$$ MSD(n) = 10\log_{10} \left( \frac{1}{K} \sum_{k=1}^{K} \Vert \boldsymbol{\theta}_{k}(n) - \boldsymbol{\theta}_0 \Vert^2 \right). $$
