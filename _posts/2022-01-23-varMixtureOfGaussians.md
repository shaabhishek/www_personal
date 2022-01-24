---
layout: post
title: Moments of a Mixture of Gaussians
usemathjax: true
---

Assume data from the following distribution:

$$
  \newcommand{\xvec}{\textbf{X}}
  \newcommand{\z}{Z}
  \newcommand{\E}{\mathbb{E}}
  \newcommand{\V}{\mathbb{V}}
$$

$$\begin{align}
\z \sim \textbf{Cat}([\pi_1, \pi_2]) \notag\\
\xvec_1 \sim \mathcal{N}(\mu_1, \Sigma_1) \notag\\
\xvec_2 \sim \mathcal{N}(\mu_2, \Sigma_2) \notag\\
\xvec = (1 - \z) \xvec_1 + \z \xvec_2
\end{align}$$
with $$\pi_1 + \pi_2 = 1$$ and $$\E[ \z ] = \pi_2$$.

Then, what are $$\E[\xvec]$$ and $$\V[\xvec]$$?

First, we find $$\E[\xvec]$$ using [Law of Total Expectation / Adam's Law](https://en.wikipedia.org/wiki/Law_of_total_expectation):

$$
\begin{align}
\E[\xvec] &= \E_\xvec[ (1 - Z) \xvec_1 + Z \xvec_2 ] \notag\\
&= \E_\z[ \E_{\xvec | \z}[(1 - Z) \xvec_1 + Z \xvec_2 | Z] ] \notag\\
&= \E_\z[ (1 - \z) \E_{\xvec | \z=0}[ \xvec_1 | \z = 0] + \z \E_{\xvec | \z=1}[\xvec_2 | \z = 1] ] \notag\\
&= \E_\z[ (1 - \z) \mu_1 + \z \mu_2 ] \notag\\
&= \pi_1 \mu_1 + \pi_2 \mu_2
\end{align}
$$

Now, we can compute $$\V[\xvec]$$ as:
$$
\begin{gather}
\V[\xvec] &= \E[X^2] - \E[X]^2
\end{gather}
$$

(TODO)