# Split Operator Fourier Transform (SOFT)

In this exercise we will see a *rare* example of algorithms for solving the quantum dynamical problem exactly.
Let's consider a time-independent Hamiltonian and its associated time-dependent Schroedinger equation for a system of one particle in one dimension
\[
i\hbar\frac{d}{dt}|\psi> = \hat{H}|\psi> \quad \text{where} \quad \hat{H} = \frac{\hat{P}^2}{2m} + E(\hat{X})
\]
We know that this equation admits at least a formal solution of the kind
\[
|\psi(t)> = \exp\biggl[-\frac{i}{\hbar}\hat{H}t\biggr]|\psi(0)>
\]
that projected on the coordinate basis gives the (still formal) solution
\[
\psi(x_t,t) = \int dx_0 K(x_t, t; x_0, 0)\psi(x_0,0)
\]
where
\[
K(x_t, t; x_0, 0) = <x_t|\exp\biggl[-\frac{i}{\hbar}\hat{H}t\biggr]|x_0>
\]
Note that $x_t$ and $x_0$ are just labels for the coordinates, as if it we had $x$ and $x'$, but we will need more in what follows and the notation with indexes would become cumbersome.
The solution is still *formal* as we have no idea on how to write the kernel $K(x_t, t; x_0, 0)$ in the general case. Nonetheless, we can use the same strategy we adopted in the classical dynamics case to solve the Louvillians. The strategy is articulated in two steps:

1. Use the time composition property to write an expression for $K(x_t, t; x_0, 0)$ as a sum of short timesteps (this is exact).

2. Use Trotter expansion to obtain a computable expression for the short-time propagator (this is an approximation).

First of all let us divide the interval $[0,t]$ in $N$ intervals of length $\varepsilon$ so that $t = N\varepsilon$. The kernel $K$ with this trick can be written as
\[
K(x_t, t; x_0, 0) = <x_t|\exp\biggl[-\frac{i}{\hbar}\hat{H}t\biggr]|x_0> = <x_t|\exp\biggl[-\frac{i}{\hbar}\hat{H}\frac{t}{N}\biggr]\dots\exp\biggl[-\frac{i}{\hbar}\hat{H}\frac{t}{N}\biggr]|x_0>
\]
where the dots implies the product of a total of $N$ terms.

**Question: Can we do that?**

We can now introduce $N$ resolutions of the identity between subsequent products of operators so to have
\[
\begin{aligned}
K(x_t, t; x_0, 0) = &\int dx_{N-1}\dots dx_{1}<x_N|\exp\biggl[-\frac{i}{\hbar}\hat{H}\varepsilon\biggr]|x_{N-1}> \times \\
&\times <x_{N-1}|\exp\biggl[-\frac{i}{\hbar}\hat{H}\varepsilon\biggr]|x_{N-2}>\dots<x_1|\exp\biggl[-\frac{i}{\hbar}\hat{H}\varepsilon\biggr]|x_0>
\end{aligned}
\]
where we have used $\varepsilon = \frac{t}{N}$.
