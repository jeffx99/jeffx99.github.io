---
layout: post
title: "Differential Forms and Foliations"
date: 2022-06-25
categories: math
---

The following post is somewhat of a rigorous extension to [Dan Piponi's](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.126.1099&rep=rep1&type=pdf) document on an intuitive visualization of differential forms.

[to be continued]
$\DeclareMathOperator{\codim}{codim}$
$\DeclareMathOperator{\sgn}{sgn}$
$\DeclareMathOperator{\Int}{Int}$
$\DeclareMathOperator{\cl}{cl}$
$\newcommand{\transv}{\pitchfork}$

## Foliations

<div class="definition">
Let $M$ be an orientable manifold and $L$ be a orientable manifold with Lebesgue measure $\mu_L$. A <i>foliation</i> along a smooth map $\mathfrak{F} \colon M \to L$ is a collection of subsets $\{\mathfrak{F}_\alpha\}$ of the form $\mathfrak{F}_{\alpha} = \mathfrak{F}^{-1}\{\alpha\}$ for $\alpha \in L$.
</div>

We say that $L$ is the *leaf space* of the foliation. The *codimension* of a foliation $\{\mathfrak{F}\_\alpha\}$ is given by $\codim \mathfrak{F} = \dim L$(which may be greater than the dimension of $M$). Define $L\_{\text{reg}} \subseteq L$ to be the set of regular values of $\mathfrak{F}$; if $\codim \mathfrak{F} \leq \dim M$ then at such indices $\mathfrak{F}\_\alpha$ is either empty or a smooth submanifold with $\dim \mathfrak{F}\_\alpha = \dim M - \codim \mathfrak{F}$. By Sard's theorem, $L_{\text{reg}}$ has full measure. Given orientation forms $o_M$ on $M$ and $o_L$ on $L$, one obtains an orientation form $o_\alpha$(for $\alpha \in L_{\text{reg}}$) on each leaf $\mathfrak{F}\_\alpha$ satisfying $o_M = \mathfrak{F}^{*}o_L \wedge o_\alpha$. This form is also given by the pullback of a $(\codim \mathfrak{F})$-form $o_\mathfrak{F}$ via the inclusion map $\mathfrak{F}_\alpha \hookrightarrow M$.

<div class="lemma">
Let $M$ be an orientable $n$-manifold and $\{\mathfrak{F}_\alpha\}$ be a foliation with leaf space $L$. Furthermore, let $N$ be a submanifold with boundary such that $\dim N = \codim \mathfrak{F}$. Then $\mathfrak{F}_\alpha$ is transverse to $N$ for almost all $\alpha \in L$.
</div>

<div class="proof">
This is simply the well-known "tranversality theorem". If $\alpha$ is a regular value of $\mathfrak{F} \circ \iota$, then the differential $(d\mathfrak{F}|_N)_p \colon T_pN \to T_\alpha L$ is surjective at each $p \in \mathfrak{F}_\alpha \cap N$. Hence if $\alpha$ is a regular value,
\begin{equation*}
    \dim N = \dim T_p N = \dim \ker (d\mathfrak{F}|_N)_p + \dim \im (d\mathfrak{F}|_N)_p = \dim \ker (d\mathfrak{F}|_N)_p + \codim \mathfrak{F}.
\end{equation*}
Since $\dim N = \codim \mathfrak{F}$, one must have $\ker (d\mathfrak{F}|_N)_p = \{0\}$. Then
\begin{equation*}
    T_p\mathfrak{F}_\alpha \cap T_pN \subseteq \ker (d\mathfrak{F})_p \cap T_pN = \ker (d\mathfrak{F}|_N)_p = \{0\}.
\end{equation*}
Since $\dim T_pN + \dim T_p\mathfrak{F}_\alpha = \dim N + \dim \mathfrak{F}_\alpha = \dim M = \dim T_pM$, one has $T_pN +  T_p\mathfrak{F}_\alpha = T_pM$; hence $\mathfrak{F}_\alpha$ is transverse to $N$. The conclusion follows by Sard's theorem.
</div>

<br>

The intersection $N \cap \mathfrak{F}\_\alpha$ of an orientable submanifold $N$(with orientation $o_N$) with a complementary leaf $\mathfrak{F}\_\alpha$ is a $0$-dimensional manifold consisting of isolated points. If $N$ is compact, then $N \cap \mathfrak{F}\_\alpha$ is also compact and hence finite. Thus one may define the *intersection number*
\begin{equation\*}
    \mathrm{I}\_N(\alpha) = \sum_{N \cap \mathfrak{F}\_\alpha} \sgn \inner{ o\_N \wedge o\_\alpha, o\_M},
\end{equation\*}
where $\sgn \colon \R - \\{0\\} \to \\{\pm 1\\}$ is the sign of a nonzero number, and $\inner{\cdot, \cdot}$ is any inner product on $\Lambda^{n}(T^*M)$ --- the specific choice does not matter since the top exterior power is one-dimensional. One checks that this is well-defined by noting that $o_M$ is nonvanishing by definition, and $o_N \wedge o_\alpha$ is nonvanishing by transversality of $N$ and $\mathfrak{F}_\alpha$.

<div class="lemma">
$\mathrm{I}_N$ is measurable.
</div>
<div class="proof">
By completeness of $\mu_L$, it suffices to prove that the restriction of $\mathrm{I}_N$ to a set of full measure is measurable. Since $\dim \partial N < \dim N = \dim L$, it follows that $\mathfrak{F}(\partial N)$ has measure $0$. Since $N$ is compact, the set $L_{\transv}$ of regular values of $\mathfrak{F} \circ \iota$ is open and, by Sard's theorem, has full measure. Thus $L_{\transv} - \mathfrak{F}(\partial N)$ is also open and of full measure.

Let $\alpha \in L_{\transv} - \mathfrak{F}(\partial N)$. Then $N \cap \mathfrak{F}_\alpha$ consists of finitely many points $x_1, \ldots, x_k$. For each $x_i \in N \cap \mathfrak{F}_\alpha$, there exists an  open set $U_i \subseteq \Int(N)$ containing $x_i$ such that $\mathfrak{F}$ maps $U_i$ homeomorphically onto an open set $V_i \subseteq L_{\transv} - \mathfrak{F}(\partial N)$ containing $\alpha$. Let $V = V_1 \cap \cdots \cap V_k$ and $W_i = U_i \cap \mathfrak{F}^{-1}V$; it follows that $\mathfrak{F}$ maps each $W_i$ homeomorphically onto $V$. Let $W = W_1 \cup \cdots \cup W_k$ and $Z = \Int(N) \cap \mathfrak{F}^{-1}V - W$. Then $Z$ is separated from each $p_i$ by $W$, so $x_i \not\in \cl_N(Z)$. Since $\alpha \not\in \mathfrak{F}(\partial N)$ and $N$ is compact, $\alpha \not \in \mathfrak{F}(\cl_N(Z)) = \cl_L(\mathfrak{F}Z)$. Hence one may shrink $V$ to avoid $\cl_L(\mathfrak{F}Z)$, defining $V'$ to be a connected subset of $V - \cl_L(\mathfrak{F}Z)$ and redefining $W_i' = U_i \cap \mathfrak{F}^{-1}V'$. As before, $x_i \in W_i'$, and $\mathfrak{F}$ maps each $W_i'$ homeomorphically onto $V'$. Furthermore, $\mathfrak{F}^{-1}V' \cap Z = \varnothing$, so
\begin{equation*}
    W_1' \cup \cdots \cup W_k' = \Int(N) \cap \mathfrak{F}^{-1}V' - Z = \Int(N) \cap \mathfrak{F}^{-1}V'.
\end{equation*}
Now let $\beta \in V'$. Then $N \cap \mathfrak{F}_\beta$ consists of $k$ points $y_1, \ldots, y_k$, such that $y_i \in W_i'$. By continuity of $\inner{o_N \wedge o_\mathfrak{F}, o_M} \colon W_i' \to \R - \{0\}$ and connectedness, $\inner{o_N \wedge o_\alpha, o_M}_{x_i}$ and $\inner{o_N \wedge o_\beta, o_M}_{y_i}$ share the same sign. It follows that $\mathrm{I}_N(\alpha) = \mathrm{I}_N(\beta$). Thus $\mathrm{I}_N$ is locally constant on $L_{\transv} - \mathfrak{F}(\partial N)$ and hence measurable.
</div>

<br>

The hypothesis that $N$ is a compact submanifold can be relaxed under certain conditions. Namely, the proposition remains true if $N$ is replaced by a precompact submanifold $U$ such that $\mathfrak{F}$ maps $U$ homeomorphically onto an open subset of $L$.
<div class="definition">
Let $M$ be an oriented $n$-manifold and $\{\mathfrak{F}_\alpha\}$ be a foliation with leaf space $L$. Furthermore, let $N$ be an oriented compact submanifold with boundary  such that $\dim N = \codim \mathfrak{F}$. The <i>total intersection</i> between $\{\mathfrak{F}_\alpha\}$ and $N$ is defined by
\begin{equation*}
    \mathrm{I}_N [\mathfrak{F}] = \int_{L} \mathrm{I}_N(\alpha) \, \d \alpha.
\end{equation*}
</div>
In fact, $\mathrm{I}\_N$ is integrable, so that $\mathrm{I}\_N [\mathfrak{F}]$ is finite; this is essentially due to the coarea formula, which we will shortly demonstrate. By the Radon-Nikodym theorem there exists a measurable function $\rho \colon L \to [0, \infty)$ such that for any measurable subset $A \subseteq L$,
\begin{equation\*}
    \mu\_L (A) = \int\_{A} \rho \cdot o\_\mathfrak{F}.
\end{equation\*}
We say that the differential form $\omega\_\mathfrak{F} = \mathfrak{F}^* (\rho \cdot o\_\mathfrak{F})$ is *analogous* to $\{\mathfrak{F}\_\alpha\}$.

<div class="theorem">
Let $M$ be a orientable $n$-manifold and $\{\mathfrak{F}_\alpha\}$ be a foliation with leaf space $L$. Furthermore, let $N$ be an orientable compact submanifold with boundary such that $\dim N = \codim \mathfrak{F}$(or satisfy the alternative hypothesis described earlier). Then
\begin{equation*}
     \mathrm{I}_N [\mathfrak{F}] = \int_{N} \omega_{\mathfrak{F}}, \tag{$\star$}
\end{equation*}
where $\omega_{\mathfrak{F}}$ is the form analogous to $\{\mathfrak{F}_\alpha\}$.
</div>
<div class="proof">
Let $\mathcal{U}$ be the set of oriented, precompact, connected submanifolds $U$ such that $\mathfrak{F}$ maps $U$ homeomorphically onto an open subset $V \subseteq L$. Then for $U \in \mathcal{U}$, the intersection number is well-defined and it follows by continuity and connectedness that $\mathrm{I}_U = \pm\mathbf{1}_{U}$ almost everywhere. Thus,
\begin{equation*}
    \mathrm{I}_U[\mathfrak{F}] = \pm\mu_L(V) = \pm \int_{V} \rho \cdot o_{\mathfrak{F}} = \int_{U} \mathfrak{F}^{*}(\rho \cdot o_\mathfrak{F}).
\end{equation*}
To obtain the last equality, note that the sign of $\mathrm{I}_U$  on $V$ is given by
\begin{equation*}
    \sgn \mathrm{I}_U = \sgn \inner{o_U \wedge o_\mathfrak{F}, o_M} =  \sgn \inner{o_U \wedge o_\mathfrak{F}, \mathfrak{F}^*o_U \wedge o_\mathfrak{F}} = \sgn \inner{o_U, \mathfrak{F}^*o_V}  =\sgn \inner{\mathfrak{F}_* o_U, o_V},
\end{equation*}
which accounts for the relative orientations of $V$ and $U$. Thus the claim is proven for $U \in \mathcal{U}$.
Now cover $N$ by open subsets $U_1, \ldots, U_k \in \mathcal{U}$ with compatible orientations. [to be (easily) continued]
</div>
<br>

In light of this proof, the work done to show that $\mathrm{I}\_N$ was measurable was not entirely necessary, as it suffices to break the surface up into pieces in $\mathcal{U}$. In the later generalization of this theorem, we defer to this simpler strategy.

Some obvious consequences: suppose that $N$ is the boundary of a open submanifold of $M$. If one starts with the well-known fact that $\mathrm{I}\_N$ vanishes everywhere, one obtains that $\mathrm{I}\_{N}[\mathfrak{F}]$ vanishes. This implies that that the analogous form integrates to $0$ over any boundary, and is thus closed. Of course, this is obvious since the analogous form is the pullback of a volume form, which is closed. Conversely, given that the analogous form is closed, one has that $\mathrm{I}\_{N}[\mathfrak{F}]$ vanishes on any boundary $N$. Then concentrating the measure $\mu\_L$ within a neighborhood of some $\alpha \in L$ and applying the theorem yields that $\mathrm{I}\_N(\alpha) = 0$ almost everywhere, which is a weaker version of the well-known result(see Guillemin and Pollack for example).

## Wedge Products and Exterior Derivatives

So far we have developed in a rigorous manner the notion of counting how many "layers" a given curve or tangent vector pass through, as described by Piponi. One would like to work with wedge products and exterior derivatives in this framework, ultimately leading to an analog of Stokes' theorem. For the wedge product, one considers the family of leaf intersections indexed over the product leaf space. In order to take nontrivial exterior derivatives, we must instead work with a "terraced" foliation---a foliation in which the leaves are submanifolds with boundaries. In this way, one may talk about taking the "boundary" of such a foliation. I'll leave the discussion of such a construction for a later post.
