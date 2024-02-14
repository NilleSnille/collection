Notes on Boltzmann Machines and Contrastive Divergence

Process

Nils Hallerfelt

October 2022

> **Boltzmann Machines**
>
> A Boltzmann machine is an energy based model consisting of *N* nodes
> connected to each other, where each node can take a binary value. We
> denote each nodes random variable as *Xi*, for *i ∈* \[1*, N*\]. Thus
> the state of the Boltzmann machine can be expressed by the random
> vector **X**. The network has parameters *θ* = (**W***,* **b**), where
> **W** are the weights and **b** are biases. As mentioned the Boltzmann
> machine is an energy based model, where the energy function is defined
> by:
>
> *Eθ* = *−***b***T***x** *−* **x***T***Wx** (1)
>
> From the energy function, the Boltzmann machines defines a probability
> distribution over the binary states:

+-----------------------------------------------------------------------+
| > *pθ*(**x**) = exp *−Eθ*(**x**) (2)                                  |
|                                                                       |
| �**x***′* exp *−Eθ*(**x***′*) = exp *−Eθ*(**x**) *−* log *Z*(*θ*)     |
|                                                                       |
| where the sum is over all possible states and *Z* is the partition    |
| function. This shows the entropy interpretation                       |
|                                                                       |
| that the idea of a Boltzmann machine is built on: the higher the      |
| energy is of a state **x**, the less likely it is to                  |
|                                                                       |
| > occur.                                                              |
+=======================================================================+
+-----------------------------------------------------------------------+

> **Introducing Latent Nodes**
>
> A Boltzmann machine with *N* visible units have*N*(*N* + 1)
> parameters. This model is used to model *N*-bit 2\
> binary patterns, that is 2*N*possible states. Thus the number of
> parameters of the the Boltzmann machine is significantly smaller than
> the number of parameters needed to model a distribution of
> 2*N*possible states. One way to make the model more expressive is to
> introduce extra latent nodes to the model: we will denote these nodes
> by **h** and say that we have *M* hidden units.

1

> **Introducing Restrictions and Real Valued Inputs**

<table>
<colgroup>
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="11">In order to represent real valued inputs, i.e.
<strong>x</strong> <em>∈</em> R<em>N</em>, while having binary hidden
nodes <strong>h</strong> <em>∈</em> [0<em>,</em> 1]<em>M</em>, we can
define the energy function in another way which also restricts the
Boltzmann machine:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>(<strong>x</strong> ) =</td>
<td></td>
<td>(<em>xi − bv i</em>)2</td>
<td></td>
<td>�</td>
<td></td>
<td><em>xiwi,jyj</em></td>
<td></td>
<td></td>
<td><blockquote>
<p><em>h .</em></p>
</blockquote></td>
<td>(3)</td>
</tr>
<tr class="even">
<td><em>θ</em>(<strong>x</strong> ) =</td>
<td>�</td>
<td>2<em>σ</em>2</td>
<td><em>−</em></td>
<td>�</td>
<td>�</td>
<td><em>σ</em>2</td>
<td><em>−</em></td>
<td>�</td>
<td><blockquote>
<p><em>j</em> <em>j.</em></p>
</blockquote></td>
<td></td>
</tr>
</tbody>
</table>

Where we have chosen *N* = 2. By defining the energy function in this
way we can show that the (visible) input

> nodes are independent between each other and Gaussian given any state
> of the hidden nodes:

+-------------+-------------+-------------+-------------+-------------+
| *p*(**x*    | > *p*(*     | �           | > *wi,jhj,  | \(4\)       |
| **\|***h**) | xi\|***h**) |             | > σ*2       |             |
| =           | > = *N*(*bv |             | > *i*)*.*   |             |
| *p*         | > i*+       |             |             |             |
| (*x*1*\|*** |             |             |             |             |
| h**)*p*(*x* |             |             |             |             |
| 2*\|***h**) |             |             |             |             |
+=============+=============+=============+=============+=============+
+-------------+-------------+-------------+-------------+-------------+

> Similarly the conditional of **h** given **x** are internally
> independent, but are Bernoulli instead of Gaussian:

+--------+--------+--------+--------+--------+--------+--------+--------+
|        | �      |        | sigm   | �      | *x     |        | \(5\)  |
|        |        |        | oid*h* |        | iwi,j* |        |        |
+========+========+========+========+========+========+========+========+
| *      | �      | *p*(   | > *p*( | �      | *σ*2   | > ))   |        |
| p*(**h |        | *hj\|* | *hi\|* |        | *i*    |        |        |
| ***\|* |        | **x**) | **x**) |        |        |        |        |
| **x**) |        |        | > =    |        |        |        |        |
| =      |        |        | > *    |        |        |        |        |
|        |        |        | B*((*b |        |        |        |        |
|        |        |        | > j*+  |        |        |        |        |
+--------+--------+--------+--------+--------+--------+--------+--------+

> **Gaussian-Bernoulli RBM**\
> By equation (3), (4), and (5) we have defined a Gaussian-Bernoulli RBM
> with the joint probability distribution:

<table>
<colgroup>
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="10"><blockquote>
<p><em>pθ</em>(<strong>x</strong><em>,</em> <strong>h</strong>) = exp
<em>−Eθ</em>(<strong>x</strong><em>,</em> <strong>h</strong>)</p>
</blockquote>
<p>�<strong>x</strong><em>′,</em><strong>h</strong><em>′</em> exp
<em>−Eθ</em>(<strong>x</strong><em>′,</em> <strong>h</strong><em>′</em>)
= exp (<em>−Eθ</em>(<strong>x</strong><em>,</em> <strong>h</strong>)
<em>−</em> log <em>Z</em>(<em>θ</em>))</p>
<p>As we will want to maximize the log-probability of the input, we
marginalize over the latent variables.</p></th>
<th rowspan="2"><p>(6)</p>
<p>(7)</p></th>
</tr>
<tr class="odd">
<th><em>p</em>(<strong>x</strong>) =</th>
<th><blockquote>
<p>exp <em>−cθ</em>(<strong>x</strong>) <em>,</em></p>
</blockquote></th>
<th><blockquote>
<p><em>c</em>(<strong>x</strong>) =</p>
</blockquote></th>
<th></th>
<th>log[1 + exp (<em>bh</em> +</th>
<th></th>
<th><em>xiwi,j</em></th>
<th><blockquote>
<p>)]</p>
</blockquote></th>
<th></th>
<th><blockquote>
<p>(<em>xi − bv i</em>)2</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>θ</em></td>
<td><blockquote>
<p>�<strong>x</strong><em>′</em> exp
<em>−cθ</em>(<strong>x</strong><em>′</em>)<em>,</em></p>
</blockquote></td>
<td><em>θ</em></td>
<td>�</td>
<td><em>j</em></td>
<td>�</td>
<td><em>σ</em>2 <em>i</em></td>
<td><em>−</em></td>
<td>�</td>
<td><blockquote>
<p>2<em>σ</em>2</p>
</blockquote></td>
<td></td>
</tr>
</tbody>
</table>

> where *cθ*(**x**) is the log partition function of
> *pθ*(**h***\|***x**).
>
> **Training**\
> In order to train the model we define the loss function as:
>
> *L*(*θ,* **x**) = *−* log *p*(**x**)*.* (8)

2

> the gradient with respect to the parameters *θ* is defined as:
>
> *∇θL*(*θ,* **x**) = *∇θcθ*(**x**) *−*
> E*x′∼pθ*(**x**)\[*∇θcθ*(**x***′*)\] (9)
>
> As the expectation term is intractable so we need to use some
> estimation technique. As both conditional dis-tributions are easy to
> sample from, it can be estimated taking samples from the distribution
> via Gibbs MCMC sampling. However, we will instead use contrastive
> divergence where only one step in the Gibbs process is taken.
>
> **Contrastive Divergence**
>
> We can rewrite the objection function of maximizing the log
> probability as a minimization of the KL-divergence between a target
> distribution and a parameterized distribution.

+-----------+-----------+-----------+-----------+-----------+-----------+
| *DKL*(    | �         | *p*target | �         | >         | \(10\)    |
| *p*target |           | log       |           | *p*target |           |
| *\|\|pθ*) |           | *p*target |           | > log     |           |
| =         |           | *−*       |           | > *pθ*    |           |
+===========+===========+===========+===========+===========+===========+
+-----------+-----------+-----------+-----------+-----------+-----------+

> As the first term does not depend on *θ* we can overlook it, and then
> maximize the negated second term, having it as the objective:

+-----------------+-----------------+-----------------+-----------------+
| *f*(*θ*) =      | �               | > *p*target log | \(11\)          |
|                 |                 | > *pθ*          |                 |
+=================+=================+=================+=================+
+-----------------+-----------------+-----------------+-----------------+

As we saw earlier the gradient of the log *pθ*(**x**) has a term that is
intractable. So we remove as by the following.

> Consider a Gibbs-sampler that is initialized by a point from the data,
> this will define the target distribution *p*target = *p*0 by
> definition. In terms of KL-divergence this results in the following:

<table>
<colgroup>
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 9%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="2"><em>DKL</em>(<em>p</em>0<em>||pθ</em>) =</th>
<th colspan="2">�</th>
<th colspan="4"><em>p</em>0(<strong>x</strong><em>′</em>) log
<em>p</em>0(<strong>x</strong><em>′</em>) <em>−</em></th>
<th>�</th>
<th><blockquote>
<p><em>p</em>0(<strong>x</strong><em>′</em>) log
<em>pθ</em>(<strong>x</strong><em>′</em>)</p>
</blockquote></th>
<th>(12)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td colspan="11"><p>As the Gibbs sampler progresses, we denote the
<em>k</em>:th step as <em>pθ k</em>, and by definition <em>pθ k</em>will
converge to <em>pθ</em> as</p>
<blockquote>
<p><em>k −→</em> inf. Thus we have that:</p>
</blockquote></td>
</tr>
<tr class="even">
<td colspan="3">The gradient of (12) can be derived to be:</td>
<td colspan="2"><em>pθ</em> inf(<strong>x</strong>) =</td>
<td colspan="6">exp <em>cθ</em>(<strong>x</strong>)<br />
�<strong>x</strong><em>′</em> exp
<em>cθ</em>(<strong>x</strong><em>′</em></td>
</tr>
<tr class="odd">
<td>�</td>
<td
colspan="5"><em>p</em>0(<strong>x</strong><em>′</em>)<em>∇cθ</em>(<strong>x</strong><em>′</em>)
<em>−</em></td>
<td>�</td>
<td colspan="3"><blockquote>
<p><em>pθ</em>
inf(<strong>x</strong><em>′</em>)<em>∇cθ</em>(<strong>x</strong><em>′</em>)</p>
</blockquote></td>
<td>(13)</td>
</tr>
</tbody>
</table>

3

To get rid of the intractable term, we can proceed one step in the Gibbs
sampling, getting *pθ* 1, and define the

> contrastive divergence as:
>
> *CD* = *DKL*(*p*0*\|\|pθ* inf) *− DKL*(*pθ* 1*\|\|pθ* inf) (14)
>
> The gradient of the CD term is:
>
> *∇θCD*(*θ*) =�*p*0(**x***′*)*∇cθ*(**x***′*) *−*�*pθ*
> 1(**x***′*)*∇cθ*(**x***′*) *− ϵ*(*θ*)*,* *ϵ*(*θ*) *≈* 0 (15)

Since we are having a RBM it the log partition *cθ* is tractable, and
thus both these terms are tractable, where the

> second term is using a single step in Gibbs sampling algorithm.
>
> **Notes**

During these notes I have used the paper "Boltzmann machines and
energy-based models" by Takayuki Osogami

> extensively.

4
