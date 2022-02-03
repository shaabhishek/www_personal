---
layout: post
title: Moments of a Mixture of Gaussians
author: Abhishek Sharma
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
\z \sim \textbf{Cat}([\pi_0, \pi_1]) \notag\\
\xvec_0 \sim \mathcal{N}(\mu_0, \Sigma_0) \notag\\
\xvec_1 \sim \mathcal{N}(\mu_1, \Sigma_1) \notag\\
\xvec = (1 - \z) \xvec_0 + \z \xvec_1
\end{align}$$
with $$\pi_0 + \pi_1 = 1$$ and $$\E[ \z ] = \pi_1$$.

Then, what are $$\E[\xvec]$$ and $$\V[\xvec]$$?

##### $$\E[\xvec]$$

First, we find $$\E[\xvec]$$ using [Law of Total Expectation / Adam's Law](https://en.wikipedia.org/wiki/Law_of_total_expectation):

$$
\begin{align}
\E[\xvec] &= \E_\xvec[ (1 - Z) \xvec_0 + Z \xvec_1 ] \notag\\
&= \E_\z[ \E_{\xvec | \z}[(1 - Z) \xvec_0 + Z \xvec_1 | Z] ] \notag\\
&= \E_\z[ (1 - \z) \E_{\xvec | \z=0}[ \xvec_0 | \z = 0] + \z \E_{\xvec | \z=1}[\xvec_1 | \z = 1] ] \notag\\
&= \E_\z[ (1 - \z) \mu_0 + \z \mu_1 ] \notag\\
&= \pi_0 \mu_0 + \pi_1 \mu_1
\end{align}
$$

##### $$\V[\xvec]$$

Now, we can compute $$\V[\xvec]$$ as:
$$
\begin{gather}
\V[\xvec] &= \E[XX^\top] - \E[\xvec]\E[\xvec]^\top
\end{gather}
$$

We know $$\E[\xvec]$$ so let's find out what $$\E[XX^\top]$$ is:
$$
\begin{align}
\E[XX^\top] &= \E_{Z}[((1 - Z) \xvec_0 + Z \xvec_1)((1 - Z) \xvec_0 + Z \xvec_1)^\top] \notag\\
&= \E_{Z}[(1 - Z)^2 \xvec_0 \xvec_0^\top + Z^2 \xvec_1 \xvec_1^\top - Z(1-Z) (\xvec_0 \xvec_1^T + \xvec_1 \xvec_0^T)] \notag\\
&= \E_{Z}[(1 - Z) \xvec_0 \xvec_0^\top + Z \xvec_1 \xvec_1^\top] \notag\\
&= \E_{Z}[(1 - Z) \E[\xvec_0 \xvec_0^\top] + Z \E[\xvec_1 \xvec_1^\top]] \notag\\
&= \E_{Z}[(1 - Z) (\mu_0 \mu_0^\top + \Sigma_0) + Z (\mu_1 \mu_1^\top + \Sigma_1)] \notag\\
&= \pi_0 (\mu_0 \mu_0^\top + \Sigma_0) + \pi_1 (\mu_1 \mu_1^\top + \Sigma_1)
\end{align}
$$

to finally get
$$
\begin{gather}
\V[\xvec] &= \pi_0 (\mu_0 \mu_0^\top + \Sigma_0) + \pi_1 (\mu_1 \mu_1^\top + \Sigma_1) - (\pi_0 \mu_0 + \pi_1 \mu_1)(\pi_0 \mu_0 + \pi_1 \mu_1)^\top
\end{gather}
$$

##### Summary (and general expression)
To summarize (in general notation for $$K \geq 2$$):

$$
\begin{align*}
\E[\xvec] &= \sum_{k=0}^{K-1} \pi_k \mu_k \\
\V[\xvec] &= \sum_{k=0}^{K-1} \pi_k (\mu_k \mu_k^\top + \Sigma_k) - \E[\xvec]\E[\xvec]^\top
\end{align*}
$$