---
layout: post
title: The Phase Space Formulation <small>(Part I)</small>
date: 2022-08-21
categories: physics
---

In the first of two expository posts, we will discuss the connection between classical and quantum mechanics through the what is known as the _phase space formulation_. Specifically, we will focus on the Weyl-Wigner transform and introduce an analogue of the Poisson bracket used in classical mechanics. Furthermore, we briefly discuss how the theory depends on the parameter $\hbar$, introducing the notion of _deformation quantization_.
<!--more-->
There exists a plethora of equivalent formulations of classical mechanics; of these, the Hamiltonian formulation is one of the most widely used, offering an elegant description of classical systems. As classical mechanics is only an approximation to an underlying theory, quantum mechanics, one may ask if it is possible to recover the Hamiltonian formulation as a classical "limit" of quantum mechanics. To do this, we take the typical setting of quantum mechanics, Hilbert space, and define a transformation to _phase space_, which is the setting for the Hamiltonian formulation of classical mechanics. In both formulations, one can develop the fundamental notions of state, observables, and time evolution. We show how each of these concepts in the usual formulation of quantum mechanics are realized in the phase space formulation.

## Hamilton Mechanics

In Hamiltonian mechanics, the state of a system is described by a point in phase space. In the simplest case, a particle in one dimension, we may write phase space as $M = \mathbb{R} \times \mathbb{R}$, so that a point $(q, p) \in M$ describes a particle with position $q$ and momentum $p$. For general systems, a point in phase space describes all the positions and momenta of each particle. The concept of momentum used in the Hamiltonian formulation differs from the concept of kinematic momentum seen in Newtonian mechanics. Momentum in Hamiltonian mechanics is usually referred to as _canonical_ momentum, and is commonly defined through the Lagrangian formulation of mechanics. Instead of considering a state as a single point, we enlarge the concept of state by considering a ensemble of many identical systems. The one must consider a _phase space distribution_ $\rho(q,p)$, which is defined so that the probability of a randomly chosen state lying within a volume(area) element $\mathrm{d}q\mathrm{d}p$ is $\rho(q,p)\,\mathrm{d}q\mathrm{d}p$. Thus, we consider a state to be a distribution function $\rho$, rather than a single point of phase space. An observable is given by a function $A \colon M \to \mathbb{R}$. In particular, position and momentum can be realized as observables taking $(q,p) \mapsto q$ and $(q,p) \mapsto p$ respectively. For a definite state $(q,p)$, the value of an observable $A$ on the state is well-defined and is simply $A(q,p)$. For a general state $\rho$, one can only calculate the expected value
\begin{equation}
    \langle A \rangle\_{\rho} \bydef \int\_{M} \rho A
\end{equation}
To each observable $A$, we associate a continuous family _canonical transformations_ $\Phi_A(t) \colon M \to M$ for each $t \in R$, which are defined by the following conditions:
1. $\Phi_A(0) = \mathrm{id}$ and $\Phi\_A(s) \circ \Phi\_A(t) = \Phi\_A(s + t).$ (additivity)
2. $A \circ \Phi\_A(t) = A$. (conservation of $A$)

The first two properties imply that $\Phi\_A$ is a _flow_ generated by a vector field $X\_A$ satisfying $\nabla\_{X\_A} A = 0$. We demand that the assignment between observables and their corresponding flow is linear, that is,
3. $X\_{\lambda A} = \lambda X\_{A}$ and $X\_{f + g} = X\_{f} + X\_{g}$ (linearity).
{:start="3"}

To complete the definition, we simultaneously define the _Poisson bracket_ $\\{f,g\\} \bydef \nabla\_{X_g} f$ and impose the following conditions on it:
4. $\\{f,g\\} \circ \Phi\_A(t) = \{f \circ \Phi\_A(t), g \circ \Phi\_A(t)\}$.
5. $\\{q,p\\} = 1$.
{:start="4"}

The fourth condition essentially states that the rate of change of $f$ along the flow induced by $g$ is preserved as one moves along the flow induced by $A$. It implies the Jacobi identity for the Poisson bracket, as we will shorty see. The fifth condition amounts to asking for $X_p$ and $X_q$ to be uniform; we say then that $p$ and $q$ are _conjugate_. Note that by the fourth condition, if one defines new coordinates $q' = q \circ \Phi\_A(t)$ and $p' = p \circ \Phi\_A(t)$, then $\{q', p'\} = 1$ as well, so canonical transformations preserve conjugate variables.

It turns out that these five conditions completely and uniquely characterize the canonical transformation associated to an observable and the Poisson bracket. For future comparison, we demonstrate that the Poisson bracket satisfies the Jacobi Identity. Let $A,B,C$ be observables. Then
\begin{align}
    \\{B , C \\} \circ \Phi\_A(t) - \\{B, C\\} &= \\{B \circ \Phi\_A(t), C \circ \Phi\_A(t)\\} - \\{B, C\\} \newline
    &= \\{B \circ \Phi\_A(t) - B , C \circ \Phi\_A(t)\\} + \\{B, C \circ \Phi\_A(t) - C\\}.
\end{align}

Therefore, one may calculate by dividing by $t$, and taking a limit as $t \to 0$,
\begin{equation}
    \\{A, \\{B,C\\}\\} = \\{\\{A, B\\}, C\\} + \\{B, \\{A,C\\}\\}.
\end{equation}

The final ingredient in the Hamiltonian formulation is the rule for dynamical evolution. One has that the dynamics of the system are given by
\begin{equation}
    (q(t), p(t)) = \Phi\_H^t(q,p),
\end{equation}
where $H$ is an observable corresponding to the energy of the system, referred to as the Hamiltonian. In other words, points in phase space flow along a vector field tangent to level surfaces of constant energy. By differentiating, this may be rewritten using Poisson brackets as
\begin{align}
    \dot{q} &= \\{q, H\\}, \newline
    \dot{p} &= \\{p, H\\}.
\end{align}
In general, if $f(q,p)$ is an observable, differentiating with respect to $t$ yields $\dot{f} = \{f, H\}$. If $f = f(q,p,t)$ depends on time, then one may write
\begin{equation}
    \frac{\mathrm{d} f}{\mathrm{d} t} = \frac{\partial f }{\partial t} + \\{f, H\\}.
\end{equation}
As a consequence of the fourth defining condition of the Poisson bracket(proof omitted), one has that time evolution preserves phase space volume, ultimately implying that $\mathrm{d} \rho / \mathrm{d} t = 0$. To see, [proof]. One may view $\rho$ as an observable giving the "density" at a point in phase space, yielding _Liouville's equation_
\begin{equation}
    \frac{\partial \rho}{\partial t} + \\{\rho, H\\} = 0
\end{equation}
governing the time evolution of a classical state.

## The Weyl-Wigner Transform

As before, we shall consider a single particle in one dimension, but in the Schrödinger picture of quantum mechanics. Given a (normalized) pure state $\ket{\psi}$, one may define the _density operator_ $\ketbra{\psi}{\psi}$. The action of the density operator on a (normalized) state $\phi$ scales the state vector $\ket{\psi}$ by the overlap $\braket{\psi}{\phi}$. In this way, the expected value of the density operator on a state $\phi$ is $\langle \hat{\rho} \rangle\_\phi = |\\!\braket{\psi|\phi}|^2$, which can be interpreted as the probability $\psi$ will be found in the same state as $\phi$ upon measurement. The Schrödinger equation implies that the density operator evolves in time by
\begin{align}
    \frac{\partial \hat{\rho}}{\partial t} = \frac{\partial \ket{\psi}}{\partial t} \bra{\psi} + \ket{\psi}\frac{\partial \bra{\psi}}{\partial t} = \frac{1}{i\hbar} \left[\hat{H} \hat{\rho} - \hat{\rho} \hat{H}\right] = \frac{1}{i\hbar} [\hat{H}, \hat{\rho}].
\end{align}
This yields the _Liouville von-Neumann equation_
\begin{equation}
    \frac{\partial \hat{\rho}}{\partial t} + \frac{1}{ih}[\hat{\rho}, \hat{H}] = 0.
\end{equation}
Noting the similarity with the classical Liouville equation; this suggests the possiblity of a linear transformation or correspondence $\Theta$ from operators on Hilbert space to observables on phase space satisfying
\begin{equation}
    \frac{1}{i\hbar}[\hat{A},\hat{B}] \longmapsto \{A,  B\}, \tag{$\star$}
\end{equation}
where $A,B$ are the classical observables corresponding to the operators $\hat{A}, \hat{B}$, respectively. If this were the case, then the evolution of system in the quantum formalism can be completely reduced to the evolution of a classical system in Hamiltonian mechanics. As the quantum theory "supersedes" classical mechanics, such a scheme now seems unlikely; indeed, _Groeneowld's theorem_ states that there is no such "simple" correspondence satisfying $(\star)$. By "simple", we refer to a linear correspondence $\Theta$ satsifying:
1. $\Theta(\hat{q}) = q$ and $\Theta(\hat{p}) = p$,
2. $\Theta \left(\frac{1}{i\hbar} [\hat{A}, \hat{B}]\right) = \\{\Theta(\hat{A}), \Theta(\hat{B})\\}$.

The proof is simple. Note that
\begin{equation}
    \left[\hat{q}^3, \hat{p}^3\right] + \frac{1}{12} \Big[\\!\left[\hat{p}^2, \hat{q}^3\right], \left[\hat{q}^2, \hat{p}^3\right]\Big] = -3\hbar^2 \cdot \mathbf{1},
\end{equation}
while a purported correspondence $\Theta$ would map the above to
\begin{equation}
    \left\\{\hat{q}^3, \hat{p}^3\right\\} + \frac{1}{12} \Big\\{\\!\left\\{\hat{p}^2, \hat{q}^3\right\\}, \left\\{\hat{q}^2, \hat{p}^3\right\\}\Big\\} = 0.
\end{equation}
By substituting $\hat{A} = \hat{q}$ and $\hat{B} = \hat{q}$ into the second condition, one obtains that $\Theta(\mathbf{1}) = 1$, which contradicts the previous conclusion that $\Theta(-3\hbar^2 \cdot \mathbf{1}) = 0$.

### Weyl Quantization

However, an appropriate linear correspondence _does_ exist, via _Weyl quantization_. We motivate this particular correspondence as follows. In classical phase space, one may consider the "definite state"
\begin{equation}
    \rho\_{q,p} = \delta\_q\delta\_p,
\end{equation}
Where $\delta\_q(q\_0) = \delta(q - q\_0)$ and $\delta\_p(p\_0) = \delta(p - p\_0)$ are Dirac delta "functions". Similarly, in quantum mechanics we have states of definite position or definite momentum represented by operators $\hat{\delta}\_q = \ketbra{q}{q}$ and $\hat{\delta}\_p = \ketbra{p}{p}$. Note however, that there is no state associated to a definite position _and- momentum, as a position ket $\ket{q}$ is completely delocalized in momenutum space and vice versa. Nevertheless, one wishes to make a correspondence $\delta\_q\delta\_p \mapsto \hat{\delta}\_q \ast \hat{\delta}\_p$, where $\ast$ is some suitable product of self-adjoint operators yielding a self-adjoint operator.

On classical phase space, one may define the inner product $(\cdot, \cdot)$ on phase space functions given by
\begin{equation}
    (A, B) \bydef \int\_M AB.
\end{equation}
For phase space distributions $\rho\_1, \rho\_2$, one can interpret $(\rho\_1, \rho\_2)$ as the probability $\rho\_1, \rho\_2$ will be observed to have the same value. We would like to compare this with the inner product $\langle \cdot, \cdot \rangle$ on the space of "trace-class operators:
\begin{equation}
    \langle A, B \rangle \bydef \operatorname{Tr} (AB).
\end{equation}
For pure density operators $\hat{\rho}\_1, \hat{\rho}\_2$, one can interpret $\langle \hat{\rho}\_1, \hat{\rho}\_2 \rangle$ as the probability that the states associated to $\hat{\rho}\_1, \hat{\rho}\_2$ will be observed to have the same value. Therefore, one wishes to find a correspondence which respects the inner product on both spaces.

A solution satisfying both of these requirements is given by letting $\ast$ be a "Weyl-ordered" product. Specifically, one may write
\begin{align}
    \hat{\delta}\_q &= \delta(q - \hat{q}) = \frac{1}{2\pi\hbar}\int \mathrm{e}^{\frac{i}{\hbar} \alpha (q - \hat{q})} \, \mathrm{d} \alpha \newline
    \hat{\delta}\_p &= \delta(p - \hat{p}) = \frac{1}{2\pi\hbar}\int \mathrm{e}^{\frac{i}{\hbar} \beta (p - \hat{p})} \, \mathrm{d} \beta.
\end{align}
Then define
\begin{equation}
    \hat{\delta}\_q \ast \hat{\delta}\_p \bydef \frac{1}{(2\pi\hbar)^2}\int \exp\left[\frac{i}{\hbar} \left(\alpha(q - \hat{q}) + \beta (p - \hat{p})\right)\right] \, \mathrm{d} \alpha \mathrm{d} \beta.
\end{equation}
Since the integrand is of the form $\exp(i\hat{\Lambda})$, where $\hat{\Lambda}$ is Hermitian, the integrand is unitary. However, by symmetry of the integration domain, taking the Hermitian conjugate leaves $\hat{\delta}_q \ast \hat{\delta}_p$ unchanged; hence $\hat{\delta}_q \ast \hat{\delta}_p$ is self-adjoint (In all honestly, this is not truly a well-defined operator, but rather plays the role of a "delta" function in what is to follow).

Thus one may define the "Weyl quantization" of a function $A \colon M \to \R$ on phase space by
\begin{equation}
    \widehat{\mathbf{W}}(A) =  \frac{1}{(2\pi\hbar)^2}\int A(q,p) (\hat{\delta}_q \ast \hat{\delta}_p) \, \mathrm{d}q \mathrm{d}p.
\end{equation}
Although we omit the proof, Weyl quantization is indeed an isometry (one must show that distinct $\hat{\delta}_q \ast \hat{\delta}_p$ are orthogonal), satisfying
\begin{equation}
    \big\langle\widehat{\mathbf{W}}(A), \widehat{\mathbf{W}}(B)\big\rangle = (A,B).
\end{equation}

The inverse procedure is known as the _Wigner transform_, and is given by
\begin{equation}
    \widetilde{\mathbf{w}}(\hat{A}) = \frac{1}{\pi\hbar} \int_{-\infty}^{\infty} \left\langle q + \tfrac{q'}{2} \right| \hat{A} \left|q - \tfrac{q'}{2} \right\rangle \mathrm{e}^{-ipq'/\hbar} \, \mathrm{d} q'.
\end{equation}
Let us denote the Wigner transform of an operator $\hat{A}$ by $\widetilde{A}$. The transformed state satisfies properties similar to that of a phase space distribution on $M$. Firstly, the Wigner transform yields a real function of phase space, despite the complex integrand. To see, note that $\hat{A}$ is self-adjoint, so
\begin{align}
    \overline{\widetilde{A}(q,p)} &= -\frac{1}{i\hbar} \int_{-\infty}^{\infty} \bra{q - \tfrac{q'}{2}} \hat{A}\ket{q + \tfrac{q'}{2}} \mathrm{e}^{ipq'/\hbar} \, \mathrm{d} q' \newline
    &= -\frac{1}{i\hbar} \int_{-\infty}^{\infty} \bra{q + \tfrac{q'}{2}} \hat{A}\ket{q - \tfrac{q'}{2}} \mathrm{e}^{-ipq'/\hbar} \, \mathrm{d} q' \newline
    &= \widetilde{A}(q,p),
\end{align}
after reversing the domain of integration in the second equality. Additionally, the Wigner transform of a pure density operator $\hat{\rho}$ satisfies
\begin{equation}
    \int_M \widetilde{\rho} = (1, \widetilde{\rho}) = \langle \mathbf{1}, \hat{\rho} \rangle = 1.
\end{equation}
Furthermore, the position and momentum probability distributions given by $\psi$ can be recovered through the "marginal" distributions as follows:
\begin{align}
    |\psi(q)|^2 &= \langle \hat{\delta}\_q, \hat{\rho} \rangle = (\delta\_q, \widetilde{\rho}) = \int \widetilde{\rho}(q, p) \,  \mathrm{d} p, \newline
    |\psi(p)|^2 &= \langle \hat{\delta}\_p, \hat{\rho} \rangle = (\delta\_p, \widetilde{\rho}) = \int \widetilde{\rho}(q, p) \, \mathrm{d} q
\end{align}
The Wigner transform $\widetilde{\rho}$ cannot be simply interpreted as a probability distribution on phase space, simply for the fact $\widetilde{\rho}$ may possibly be negative. Furthermore, as provided by the Heisenberg uncertainty principle, one can not simultaneously be "certain" of a state's position and momentum; this corresponds to a bound on the magnitude of $\widetilde{\rho}$. For example, a "definite" state of the form $\widetilde{\rho}(q,p) = \delta(q - q\_0, p - p\_0)$ is disallowed. This follows from the integral triangle inequality and Cauchy-Schwarz inequality"
\begin{align}
    |\widetilde{\rho}| &\leq \frac{1}{\pi \hbar } \int_{-\infty}^{\infty} \left|\psi\left( q + \tfrac{q'}{2}\right) \psi\left(q - \tfrac{q'}{2}\right) \right| \, \mathrm{d} q' \newline
    &\leq \frac{1}{\pi \hbar} \left[\int_{-\infty}^{\infty} \left|\psi\left( q + \tfrac{q'}{2}\right) \right|^2 \mathrm{d} q'  \int_{-\infty}^{\infty} \left| \psi\left(q - \tfrac{q'}{2}\right) \right|^2 \mathrm{d} q'\right]^{1/2} \newline
    &= \frac{1}{\pi \hbar}.
\end{align}
For these reasons the Wigner transform of a state $\ket{\psi}$ is referred to as a _quasiprobability distribution_.

The Weyl quantization procedure, and thus the Wigner transform were only developed with pure density operators and phase space distributions in mind. Yet, the definition given extends to a correspondence between observables in the classical and quantum pictures. To understand this, note that observables in both pictures are essentially "constructed" from definite states in similar ways: In the classical picture, an observable associates a value $A\_{q,p}$ to each definite state $\rho\_{q,p}$, and is formed by taking a linear combination
\begin{equation}
    A = \int\_M A\_{q,p} \rho\_{q,p}.
\end{equation}
Similarly, in the quantum picture, an observable associates a value $A\_i$ to a orthonormal basis of definite states $\\{\ket{\psi\_i}\\}$, and is formed by taking a linear combination
\begin{equation}
    \hat{A} = \sum\_i A\_i \ketbra{\psi\_i}{\psi\_i}.
\end{equation}
By writing observables in this form, we may interpret them physically by considering the inner products $(A, \rho)$ and $\langle\hat{A}, \hat{\rho} \rangle$. In both pictures, these evaluate to the expected value of the observable on the state. Thus, since the Weyl-Wigner correspondence is an isometry, the physical meaning of observables are preserved in both pictures.

## Time Evolution

So far, we have developed the notion of states and observables in the phase space formulation of quantum mechanics, which leaves us to describe the time evolution of states to "complete" the formulation. This will be the topic of the second part of this post, in which we derive the evolution equations and connect our result to the classical analogue, Hamilton's equation.
