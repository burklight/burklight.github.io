## The Gibbs variational principle and the Donsker-Varadhan lemma

The Gibbs variational principle and the Donsker-Varadhan lemma are two important inequalities that relate:
- the relative entropy $D(\mu \lVert \nu)$ of a probability distribution $\mu$ with respect to another distribution $\nu$,
- the expectation $\mathbb{E}_{x \sim \mu}[g(x)]$ of a measurable function $g$ with respect to $\mu$, and
- the cumulant generating function $\log \mathbb{E}_{x \sim \nu} [e^{g(x)}]$ of that function with respect to $\nu$. 

They were originally proposed (as far as I know) by J. W. Gibbs in 1902 and by M. D. Donsker and S. R. S. Varadhan in 1975 respectively. The way that they are commonly referred to and written in these days is the following:

---
**Gibbs variational principle** *Let $(\mathcal{X}, \mathscr{X})$ be a measurable space, $\nu$ be a probability measure on $\mathcal{X}$, and $g$ be a measurable function on $\mathcal{X}$ such that $\mathbb{E}_{x \sim \nu}[e^{g(x)}] < \infty$. Let $\mathcal{P}_{\nu}(\mathcal{X})$ be the set of probability measures $\mu$ on $\mathcal{X}$ such that $\mu \ll \nu$, then*

$$
\begin{equation*}
\log \mathbb{E}_{x \sim \nu} [ e^{g(x)} ] = \sup_{\mu \in \mathcal{P}_{\nu}(\mathcal{X})} \Big \lbrace \mathbb{E}_{x \sim \mu}[g(x)] - D(\mu \lVert \nu) \Big \rbrace.
\end{equation*}
$$

---

---
**Donsker-Varadhan lemma:** *Let $(\mathcal{X}, \mathscr{X})$ be a measurable space and $\mu$ and $\nu$ be two probability measures on $\mathcal{X}$. Let $\mathcal{G}_{\nu}$ the set of all measurable functions on $\mathcal{X}$ such that $\mathbb{E}_{x \sim \nu}[e^{g(x)}] < \infty$. If $\mu \ll \nu$, then*

$$
\begin{equation*}
D(\mu \lVert \nu) = \sup_{g \in \mathcal{G}_{\nu}} \Big \lbrace \mathbb{E}_{x \sim \mu}[g(x) ] - \log \mathbb{E}_{x \sim \nu} [e^{g(x)}] \Big \rbrace
\end{equation*}
$$

---

In this blog I will mainly cover three things:
1. *The duality between both formulations.* We will see that both statements are equivalent in that the Donsker-Varadhan lemma is the dual problem of the Gibbs variational principle.
2. *The proof of the Gibbs variational principle.* We will see the proof of the Gibbs variational principle following R. van Handel beautiful lecture notes proof. As per point 1., this will also effectively proof Donsker-Varadhan lemma.
3. *The proof of Donsker-Varadhan lemma.* We will go over the original proof from M. D. Donsker and S. R. S. Varadhan. The original paper is behind a paywall and the proof is pretty, so I thought that I might as well keep it here.

---
**Note:** *In the Gibbs variational principle, we do not need to restrict the probability measures $\mu$ to those that are absolutely continuous with respect to $\nu$. That is, the supremum can be the set of all probability distributions $\mathcal{P}(\mathcal{X})$. However, often we are only interested in the distributions in $\mathcal{P}_{\nu}(\mathcal{X})$. Moreover, it is this more restricted formulation the one that will allow us to find the duality statement.*

---

## Two sides of the same coin

It is known that, for a fixed $\nu$, the relative entropy $D(\mu \lVert \nu)$ is convex  and lower semicontinuous with respect to $\mu$ [Polyanskiy and Wu 2022, Theorem 5.1 and Theorem 4.8]. For convenience, let us define this function as $D_{\nu}(\mu) := D(\mu \lVert \nu)$.

Then, we can employ some duality tricks to realize that both the Gibbs variational principle and the Donsker-Varadhan lemma are two sides of the same coin.

Let $\nu$ be a probability measure. Let $\mathcal{P}\_{\nu}(\mathcal{X})$ be the set of all probability distributions $\mu$ on $\mathcal{X}$ such that $\mu \ll \nu$. Similarly, let $\mathcal{G}\_{\nu}$ be the set of all measurable functions in $\mathcal{X}$ such that $\mathbb{E}\_{x \sim \nu}[e^{g(x)}] < \infty$. This is equivalent to the set of all measurable functions in $\mathcal{X}$ such that $\mathbb{E}\_{x \sim \mu}[g(x)] < \infty$ for all $\mu \in \mathcal{P}\_{\nu}(\mathcal{X})$. Therefore, $\mathcal{G}\_{\nu}$ is the dual space of $\mathcal{P}\_{\nu}(\mathcal{X})$ and the canonical dual pairing between the two spaces is $\langle \mu, g \rangle := \mathbb{E}\_{x \sim \mu} [g(x)]$.

Consider the convex conjugate $D\_{\nu}^{\*} : \mathcal{G}\_{\nu} \to \mathbb{R}$ of $D\_{\nu}$, that is

$$
\begin{equation*}
    D_{\nu}^{*}(g) = \sup_{\mu \in \mathcal{P}(\mathcal{X})} \Big \lbrace \langle \mu, g \rangle - D_{\nu}(\mu)  \Big \rbrace.
\end{equation*}
$$

From the Gibbs variational principle, we know that $D\_{\nu}^{\*}(g) = \log \mathbb{E}\_{x \sim \nu} [e^{g(x)}]$. The dual space of $\mathcal{G}\_{\nu}$ is now $\mathcal{M}\_{\nu}(\mathcal{X})$, which comprises all signed measures such that $\int_{\mathcal{X}} g(x) d\mu(x) < \infty$ for all $g \in \mathcal{G}\_{\nu}$ and the canonical dual pairing between the two spaces is $\langle \mu, g \rangle :=  \int_{\mathcal{X}} g(x) d\mu(x)$. 

Since $D_{\nu}$ is convex and lower semicontinuous by the Fenchel–Moreau theorem it holds that the convex conjugate $(D\_{\nu}^{\*})^{\*}$ of $D\_{\nu}^{\*}$ is equal to the original function $D_{\nu}$. Hence, we have that

$$
\begin{aligned}
    D_{\nu}(\mu) &= \sup_{g \in \mathcal{G}_{\nu}} \Big \lbrace \langle \mu, g \rangle - D_{\nu}^{*}(g) \Big \rbrace \\
    &= \sup_{g \in \mathcal{G}_{\nu}} \Big \lbrace \langle \mu, g \rangle - \log \mathbb{E}_{x \sim \nu} [e^{g(x)}] \Big \rbrace,
\end{aligned}
$$

which recovers the Donsker-Varadhan lemma. In fact, it finds a slightly more general version where $\mu$ does not need to be a probability measure. In any case, as it holds for all signed measures $\mu \in \mathcal{M}\_{\nu}(\mathcal{X})$, it also holds for all probability measures $\mu \in \mathcal{P}\_{\nu}(\mathcal{X}) \subseteq \mathcal{M}\_{\nu}(\mathcal{X})$.

## Proof of the Gibbs variational principle

The Gibbs variational principle is often traced back to Theorem III on Chapter XI of J. W. Gibbs' 1902 compilation book. The results there are in the language of statistical mechanics and admittedly I have not been able to follow it - albeit some non-negligible efforts.

In any case, I really like R. van Handel's proof from Lemma 4.1 in his lecture notes. Below, I basically re-write his proof, so go check his notes as well :).

*Proof:* Consider a probability measure $\gamma \in \mathcal{P}\_{\nu}(\mathcal{X})$. Then, 

$$
\begin{equation*}
    \log \int_{\mathcal{X}}  e^{g(x)} d \nu(x) - D(\mu \lVert \gamma) = \log \int_{\mathcal{X}}  e^{g(x)} d \nu(x) - \int_{\mathcal{X}} \log \Big( \frac{d\mu}{d\gamma}(x) \Big) d\mu(x)
\end{equation*}
$$

and $\sup_{\mu \in \mathcal{P}\_{\nu}(\mathcal{X})} \big \lbrace \log \int_{\mathcal{X}} e^{g(x)} d \nu(x) - D(\mu \lVert \gamma) \rbrace =  \log \int_{\mathcal{X}} e^{g(x)} d \nu(x)$ since the relative entropy is non-negative.

An inspection of the Radon-Nikodym theorem [McDonald and Weiss 1999, Theorem 9.3] hints that we may want to consider the probability measure $\gamma$ with Radon-Nikodym derivative

$$
\begin{equation*}
    \frac{d \nu}{d \gamma} (x) = \frac{\int_{\mathcal{X}} e^{g(y)} d\nu(y)}{e^{g(x)}}.
\end{equation*}
$$

Crucially, this probability measure has the property that $\gamma \ll \nu$ and $\nu \ll \gamma$. Using this selection of $\gamma$ and the fact that for probability measures $\mu \ll \nu \ll \gamma$ it holds that $\frac{d \mu}{d \gamma} = \frac{d \mu}{d \nu} \frac{d \nu}{d \gamma}$ we obtain that

$$
\begin{aligned}
     \log \int_{\mathcal{X}}  &e^{g(x)} d \nu(x) - D(\mu \lVert \gamma) \\
     &= \log \int_{\mathcal{X}}  e^{g(x)} d \nu(x) - \int_{\mathcal{X}} \bigg( \log \Big( \frac{d\mu}{d\nu} (x) \Big) + \log \int_{\mathcal{X}} e^{g(y)} d\nu(y) - \log e^{g(x)}   \bigg) d \mu(x) \\
     &= \int_{\mathcal{X}} g(x) d\mu - D(\mu \lVert \nu).
\end{aligned}
$$

Finally, taking the supremum of $\mu$ over all $\mathcal{P}\_{\nu}(\mathcal{X})$ recovers the original statement. $\square$

By the duality argument from before, this also proves the Donsker-Varadhan lemma. 


## Original proof of the Donsker-Varadhan lemma

Originally, the Donsker-Varadhan lemma was formulated a little differently. More precisely:

---
**Original Donsker-Varadhan (as originally formulated):** *Let $(\mathcal{X}, \mathscr{X})$ be a measurable space and $\mu$ and $\nu$ be two probability measures on $\mathcal{X}$. Let also $\mathcal{U}$ be the set of all measurable functions on $\mathcal{X}$ such that there exists constants $c_1$ and $c_2$ satisfying that $0 < c_1 \leq u(x) \leq c_2 < \infty$ a.s.. If $\mu \ll \nu$, then*

$$
\begin{equation*}
D(\mu \lVert \nu) = \sup_{u \in \mathcal{U}} \Big \lbrace \mathbb{E}_{x \sim \mu}[ \log u(x) ] - \log \mathbb{E}_{x \sim \nu} [u(x)] \Big \rbrace
\end{equation*}
$$

---

Letting $u = e^g$ basically recovers the statement as we know it today. To be precise, in the original statement, they considered $(\mathcal{X}, \mathscr{X})$ to be a *metric* space, and the set of functions $\mathcal{U}^{\*}$, which are the functions in $\mathcal{U}$ that are also continuous and where the condition $0 < c_1 \leq u(x) \leq c_2 < \infty$ holds for all $x \in \mathcal{X}$. However, as will be apparent in their proof, these extra requirements are not necessary.

---
**Note:** *This extra requirements may be interesting in some situations where one is interested in having a smaller optimization set. However, often, in my limited experience, one wants to have as much liberty as possible when choosing the function $u$.*

---

The proof from M. D. Donsker and S. R. S. Varadhan consists of two parts:
- showing that $D(\mu \lVert \nu) \geq \mathbb{E}\_{x \sim \mu}[ \log u(x) ] - \log \mathbb{E}\_{x \sim \nu} [u(x)]$ for all $u \in \mathcal{U}$,
- and showing that the supremum is achieved.

The proof of the lemma is still very readable with the notation conventions of today. However, I will write a slightly shorter version in the same spirit.

In the original proof and paper, M. D. Donsker and S. R. S. Varadhan also deal with the lower semicontinuity of the relative entropy and the fact that $D(\mu \lVert \nu)$ is finite if $\mu \ll \nu$, but these were already known facts from the information theory community and we will not deal with them here.

### Proof of the inequality

By definition, the relative entropy of $\mu$ with respect to $\nu$ is $D(\mu \lVert \nu) := \mathbb{E}\_{x \sim \mu} \Big[ \log \Big( \frac{d\mu}{d\nu}(x) \Big) \Big]$, where $\frac{d\mu}{d \nu}$ is the Radon-Nikodym derivative of $\mu$ with respect to $\nu$. For the rest of the proof, it is convenient to give this measure it own symbol, for instance $\rho = \frac{d \mu}{d \nu}$.

The proof starts with a change of measure [McDonald and Weiss 1999, Proposition 9.1] followed by standard manipulations of logarithms. More precisely,

$$
\begin{aligned}
\mathbb{E}_{x \sim \mu} [ \log u(x) ] &= \int_{\mathcal{X}} \log  u(x)  d\mu(x) \\
&= \int_{\mathcal{X}} \rho(x) \log u(x)  d\nu(x) \\
&= \int_{\mathcal{X} } \rho(x) \log \Big(\frac{\rho(x)}{\rho(x)} \cdot u(x) \Big) d\nu(x) \\
&= \int_{\mathcal{X}} \rho(x) \log  \rho(x)  d\nu(x) +   \int_{\lbrace x \in \mathcal{X} : \rho(x) > 0 \rbrace} \rho(x) \log \Big(\frac{u(x)}{\rho(x)}  \Big) d\nu(x).
\end{aligned}
$$

Employing the change of measure once more to the first term on the right hand side of the last equation reveals that

$$
\begin{equation*}
\int_{\mathcal{X}} \rho(x) \log  \rho(x)  d\nu(x) = \int_{\mathcal{X}}  \log  \rho(x)  d\mu(x) := D(\mu \lVert \nu).
\end{equation*}
$$

Finally, using Jensen's inequality to the second term shows that

$$
\begin{aligned}
\int_{\lbrace x \in \mathcal{X} : \rho(x) > 0 \rbrace} \rho(x) \log \Big(\frac{u(x)}{\rho(x)}  \Big) d\nu(x) &\leq \log \int_{\lbrace x \in \mathcal{X} : \rho(x) > 0 \rbrace} \rho(x) \cdot \frac{u(x)}{\rho(x)}  d\nu(x) \\
&\leq \log \int_{\mathcal{X}} u(x)  d\nu(x),
\end{aligned}
$$

and re-arranging the terms completes the proof. $\square$

### Proof of the achievability 

From the proof of the equality, it seems clear that the inequality holds with equality when $u = \rho$ almost surely. 

With this purpose, let $(u_n)\_{n > 0}$ be a sequence of functions $u_n \in \mathcal{U}$ defined as

$$
\begin{equation*}
    u_n(x) := \max \Big( \min \big( \rho(x), n), \frac{1}{n} \Big). 
\end{equation*}
$$

From this definition, we see that $\lim_{n \to \infty} \int_{\mathcal{X}} \lvert u_n(x) - \rho(x) \rvert \nu(x) = 0$. Hence, since $0 < c_1 \leq u_n \leq c_2 < \infty$ a.s. for some $c_1$ and $c_2$ by definition, by the dominated convergence theorem [McDonald and Weiss 1999, Theorem 5.9] and the continuity of the logarithm

$$
\begin{aligned}
   \lim_{n \to \infty} \log \int_{\mathcal{X}} u_n(x)  d\nu(x) &= \log  \int_{\mathcal{X}} \lim_{n \to \infty} u_n(x)  d\nu(x) \\
   &= \log  \int_{\mathcal{X}} \rho(x)  d\nu(x) \\
   &= \log  \int_{\mathcal{X}} d\mu(x) = 0,
\end{aligned}
$$

where the last step follows from using again the change of measure.

Therefore, to complete the proof we only need to show that $\lim_{n \to \infty} \int_{x \in \mathcal{X}} \log u_n(x) d\mu(x) = D(\mu \lVert \nu)$. The way that they did this is using the Jordan decomposition of $\log u_n$, that is $\log u_n = (\log u_n)^+ - (\log u_n)^-$, where each term represents the positive and negative parts of $\log u_n$ respectively. Then, one may note that both $(\log u_n)^+$ and $(\log u_n)^-$ are monotonically increasing sequences converging to $(\log \rho)^+$ and $(\log \rho)^-$ respectively. Hence, by the monotone convergence theorem [McDonald and Weiss 1999, Theorem 5.6]

$$
\begin{aligned}
    \lim_{n \to \infty} \int_{x \in \mathcal{X}} \log u_n(x) d\mu(x) &= \lim_{n \to \infty} \int_{x \in \mathcal{X}} (\log u_n(x))^+ d\mu(x) - \lim_{n \to \infty} \int_{x \in \mathcal{X}} (\log u_n(x))^- d\mu(x) \\
    &= \int_{x \in \mathcal{X}} \lim_{n \to \infty}  (\log u_n(x))^+ d\mu(x) -  \int_{x \in \mathcal{X}} \lim_{n \to \infty} (\log u_n(x))^- d\mu(x) \\
    &= \int_{x \in \mathcal{X}}  (\log \rho (x))^+ d\mu(x) -  \int_{x \in \mathcal{X}}  (\log \rho (x))^- d\mu(x) \\
    &= \int_{x \in \mathcal{X}}  \log \rho (x) d\mu(x) := D(\mu \lVert \nu),
\end{aligned}
$$

which completes the proof. $\square$

## And that is all

Well, that is the end of this blog. Thank you very much for reading until the end and again I hope I did not bore you too much or I did not write too many incoherences.

Please, let me know if you have any suggestions. 

The references for this blog are:

* J. W. Gibbs. *Elementary principles in statistical mechanics: developed with especial reference to the rational foundation of thermodynamics.* C. Scribner’s sons, 1902.

* M. D. Donsker and S. S. Varadhan. *Asymptotic evaluation of certain Markov process expectations for large time, I*. In: Communications on Pure and Applied Mathematics, 1975.

* McDonald, John N., and Neil A. Weiss. *A course in real analysis.* Taylor & Francis US, 1999.

* Van Handel, Ramon. *Probability in high dimension.* Princeton University Notes, 2014.

* Polyanskiy, Yuri, and Wu, Yihong. *Information Theory: From Coding to Learning.* Cambridge University Press, forthcoming, 2022.


