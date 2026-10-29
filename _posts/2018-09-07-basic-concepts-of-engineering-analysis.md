---
title: "Basic concepts of engineering analysis"
date: 2018-09-07 22:33:44
categories:
- "Notes"
tags:
- "FEA"
redirect_from:
- /archives/01mey7.html
---

{% raw %}
## Analysis of discrete systems

The essence of a lumped-parameter mathematical model is that the state of the system can be described directly with adequate precision by the magnitudes of a finite (and usually small) number of state variables. The solution requires the following steps:

1.  ***System idealization***: the actual system is idealized as an assemblage of elements
2.  ***Element equilibrium***: the equilibrium requirements of each element are established in terms of state variables
3.  ***Element assemblage***: the element interconnection requirements are invoked to establish a set of simultaneous equations for the unknown state variables
4.  ***Calculation of response***: the simultaneous equations are solved for the state variables, and using the element equilibrium requirements, the response of each element is calculated.
{% endraw %}

<!-- more -->

{% raw %}
### Steady-State Problems

The response of the system does not change with time. The state variables describing the response of the system under consideration can be obtain can be obtained from the solution of a set of equations that do **not involve time as a variable**.

Simple problems like elastic spring system and nonlinear elastic spring system.

### Propagation / Dynamic Problems

The main characteristic of a propagation or dynamic problem is that the response of the system under consideration **changes with time**. For the analysis of a system, in principle, the same procedures as in the analysis of a steady-state problem are employed, but now the state variables and element equilibrium relations depend on time. The objective of the analysis is to calculate the state variables for all time *t*.

In the case that the system response is obtained using the equations governing the steady state response but substituting the time-dependent load or forcing vector for the load vector employed in the steady-state analysis. Since such an analysis is in essence still a steady-state analysis, but with steady-state conditions considered at any time *t*, the analysis may be referred to as a ***pseudo steady-state analysis***.

In an actual propagation problem, the **element equilibrium relations are time dependent**, and this accounts for major differences in the response characteristics when compared to steady-state problems.

### Eigenvalue Problems

A main characteristic of an eigenvalue problem is that there is no unique solution to the response of the system, and the objective of the analysis is to calculate the various possible solutions. Eigenvalue problems arise in both steady-state and dynamic analyses.

The generalized eigenvalue problem of the form:

**Av**= λ**Bv**

where **A** and **B** are symmetric matrices, λ is a scalar, and v is a vector. If λ and **v** satisfy  
this form, they are called an eigenvalue and an eigenvector, respectively.

The solutions to eigenvalue problem depends on the system under consideration and the loads acting on the system.

### On the Nature of Solutions

For steady-state and propagation problems, it is convenient to distinguish between linear and nonlinear problems. In simple terms, a linear problem is characterized by the fact that the response of the system varies in proportion to the magnitude of the applied loads and all other problems are nonlinear.

## Analysis of continuous systems

As in the solution of discrete models, two different approaches can be followed to generate the system-governing differential equations: the direct method and the variational method.

### Differential Formulation

In the differential formulation we establish the equilibrium and constitutive requirements of typical differential elements in terms of state variables. These considerations lead to a system of differential equations in the state variables, and it is possible that all compatibility requirements (i.e., the interconnectivity requirements of the differential elements) are already contained in these differential equations (e.g., by the mere fact that the solution is to be continuous). Finally, to complete the formulation of the problem, all boundary conditions, and in a dynamic analysis the initial conditions, are stated.

### Variational Formulations

The essence of the variational approach is to calculate the **total potential Π** of the system and to invoke the stationarity of Π i.e., **δΠ=0**, with respect to the state variables. The variational approach provides a particularly powerful mechanism for the analysis of continuous systems. The main reason for this effectiveness lies in the way by which some boundary conditions (namely, the natural boundary conditions) can be generated and taken into account when using the variational approach.

The total potential Π is also called the ***functional*** of the problem. Assume that in the functional the highest derivative of a state variable (with respect to a space coordinate) is of order *m*; i.e., the operator contains at most *m*th-order derivatives. We call such a problem a ***C^(m-1) variational problem***. Considering the boundary conditions of the problem, we identify two classes of boundary conditions:

The **essential boundary condition**: also called ***geometric boundary conditions*** because in structural mechanics the essential boundary conditions correspond to prescribed displacements and rotations. The order of the derivatives in the essential boundary conditions is, in a C^(m-1) problem, at most *m*-1.

The **natural boundary condition**: also called ***force boundary conditions*** because in structural mechanics the natural boundary conditions correspond to prescribed boundary forces and moments. The highest derivatives in these boundary conditions are of order *m* to *2m-*1.

For ***approximate solutions***, a larger class of trial functions can be employed in many cases if the analyst operates on the variational formulation rather than on the differential formulation of the problem; for example, the *trial functions* need not satisfy the natural boundary conditions because these boundary conditions are implicitly contained in the functional. This last consideration has most important consequences, and much of the success of the finite element method hinges on the fact that by employing a variational formulation, a larger class of functions can be used.

### Weighted Residual Methods; Ritz Method

For more complex systems, approximate procedures of solution must be employed. The classical techniques, in which a family of trial functions is used to obtain an approximate solution, are very closely related to the finite element method of analysis and that indeed the finite element method can be regarded as an extension of these classical procedures.

The basic step in the weighted residual and Ritz analyses is to assume a solution with the functions *f*_(i) satisfying all boundary conditions, and then calculate the residual *R*.

$$
\phi = \sum\limits_{i = 1}^n {{a_i}{f_i}}
$$

where the *f*_(i) are linearly independent trial functions and the *a*_(i) are multipliers to be determined in the solution.

For the exact solution this residual is of course zero. A good approximation to the exact solution would imply that *R* is small at all points of the solution domain. The various weighted residual methods, **Galerkin method** and **Least squares method** etc., differ in the criteria that they employ to calculate the *a*_(i) such that *R* is small. However, in all techniques we determine the *a*_(i) so as to make a weighted average of *R* vanish.

### Imposition of constraints

Constraints may need to be imposed on some continuous solution parameters or on some discrete variables in the analysis of an engineering problem and may consist of certain continuity requirements, the imposition of specified values for the solution variables, or conditions to be satisfied between certain solution variables. Two widely used procedures are available, namely, the **Lagrange multiplier method** and the **penalty method**.

22.3035392114.1751808
{% endraw %}
