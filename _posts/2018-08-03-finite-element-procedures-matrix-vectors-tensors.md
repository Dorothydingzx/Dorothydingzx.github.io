---
title: "Finite Element Procedures – Matrix, Vectors, Tensors"
date: 2018-08-03 16:55:03
categories:
- "Notes"
tags:
- "FEA"
redirect_from:
- /archives/pmlr0v.html
---

{% raw %}
## Special Matrix

**symmetric matrix**

**identity matrix / unite matrix**

**symmetric banded matrix**

the following matrix is a symmetric banded matrix of order 5 and the half-bandwidth is 2.

$$
{\rm{A}} = \left[ {\begin{array}{*{20}{c}}
3&2&1&0&0\\
2&3&4&1&0\\
1&4&5&6&1\\
0&1&6&7&4\\
0&0&1&4&3
\end{array}} \right]
$$

**diagonal matrix**: nonzero elements only on the diagonal of the matrix

upper half of the matrix

**inverse matrix**, the inverse of a matrix

**partitioning of matrix**

**the trace and determinant of a matrix**: only defined if the matrix is square

tr(**A**) = sum of elements on the diagonal

det **A** = determinant

det (**BC…F**) = (det **B**)(det **C**)…(det **F**)

**orthogonal matrix**:

$$
{{\rm{P}}^T} = {{\rm{P}}^{ - 1}}
$$
{% endraw %}

<!-- more -->

{% raw %}
## Vectors

**change of basis**: transformation that corresponds to a change of basis

$$
y = {\rm{A}}x = {{\rm{P}}^{ - 1}}{\rm{AP}}
$$

**rotation matrix** (orthogonal): In general case, this rotation is carried out in the *n*-dimensional space.

$$
{\rm{P}} = \left[ {\begin{array}{*{20}{c}}
{\cos \theta }&{ - \sin \theta }\\
{\sin \theta }&{\cos \theta }
\end{array}} \right]
$$

**reflection matrix** (orthogonal)

$$
{\rm{P}} = {\rm{I}} - \alpha {\rm{v}}{{\rm{v}}^T};{\kern 1pt} {\kern 1pt} {\kern 1pt} {\kern 1pt} {\kern 1pt} {\kern 1pt} {\kern 1pt} {\kern 1pt} {\kern 1pt} \alpha = \frac{2}{{{{\rm{v}}^T}{\rm{v}}}}
$$

where **v** can be arbitrary. This matrix is called a reflection matrix, because the vector **Pw** is the reflection of vector **w** in the plane to which v is orthogonal.

## Tensor

**Cartesian tensors**: tensors represented in rectangular Cartesian coordinate frames.

**Scalar**: an entity is called a scalar if it has only a single component in the coordinates and this component does not change under a coordinate transformation.

**A vector or tensor of first order**: if it has three components $$\xi _i$$ in the unprimed frame and three components $$\xi _i^{,}$$ in the primed frame, and if these components are related by characteristic law (using the summation convention).

$$
\xi _i^{,} = {p_{ik}}{\xi _k}
$$

the **scalar product** of the vectors **u** and **v**

$$
{\rm{u}} \times {\rm{v}} = \left| {\rm{u}} \right|\left| {\rm{v}} \right|\cos \theta = {u_i}{v_i}
$$

the **dot product** of the vectors **u** and **v**

$$
{\rm{w}} = \det \left[ {\begin{array}{*{20}{c}}
{{{\rm{e}}_1}}&{{{\rm{e}}_2}}&{{{\rm{e}}_3}}\\
{{u_1}}&{{u_2}}&{{u_3}}\\
{{v_1}}&{{v_2}}&{{v_3}}
\end{array}} \right]
$$

the scalar and dot product of vectors are frequently employed in finite element analysis to evaluate angles between two given directions and to establish the direction perpendicular to a given plane.

**A second order tensor**: it has nine components $$t_{ij}$$, i = 1, 2, 3 and j = 1, 2, 3 in the unprimed frameand nine components $$t_{ij}^{,}$$ in the primed frame and if these components are related by the characteristic law

$$
t_{ij}^{,} = {p_{ij}}{p_{jk}}{t_{kl}}
$$

<div class="archived-comments" markdown="0">
<h3>2 Comments</h3>
<p class="archived-comments-note">These comments were left on the original WordPress version of this blog.</p>
<ol class="archived-comment-list">
<li class="archived-comment">
<div class="archived-comment-meta"><strong>christinaheadrick</strong> <span>September 30, 2018 at 15:38</span></div>
<div class="archived-comment-body"><p>Having read tһis I believeⅾ it was really enlightening.</p><p>I appreciate yoս finding thhe time aand energy to put this article<br/>
together. I once avain find myѕelf personally spending a ⅼot of timee<br/>
both reading andd leaving comments. But so what, it<br/>
wɑs stilⅼ ѡorthwhile!</p></div>
</li>
<li class="archived-comment">
<div class="archived-comment-meta"><strong>Dorothy</strong> <span>October 1, 2018 at 15:32</span></div>
<div class="archived-comment-body"><p>Thanks for your appreciation. I will try to make my articles more clear later.</p></div>
</li>
</ol>
</div>
{% endraw %}
