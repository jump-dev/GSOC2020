# JuMP

JuMP is a modeling interface and a collection of supporting packages for mathematical optimization that is embedded in Julia. With JuMP, users formulate various classes of optimization problems with easy-to-read code, and then solve these problems using state-of-the-art open-source and commercial solvers. JuMP also makes advanced optimization techniques easily accessible from a high-level language.

## Mentors

- [Mathieu Besançon](https://github.com/matbesancon)
- [Chris Coey](https://github.com/chriscoey)
- [Joaquim Dias Garcia](https://github.com/joaquimg)
- [Benoît Legat](https://github.com/blegat)
- [Mario Souto](https://github.com/mariohsouto)


## Project Ideas

###  Visualization of bridge graph

#### Abstract

Bridges help reformulate the constraints and functions from a model into another form that is compatible by the solver. The goal of this project is to let users see the potential bridges from a model to another, and the bridges effectively used to map a model to a reformulation which can be optimized by a given solver.

| **Intensity**                          | **Priority**              | **Involves**  | **Mentors**              |
| -------------                          | ------------              | ------------- | -----------              |
| Moderate  |  Medium  | Vizualize the potential bridges applied to a model. Very useful for debugging and performance improvement. | [Mathieu Besançon](https://github.com/matbesancon) and [Benoît Legat](https://github.com/blegat) |

#### Technical Details

Technical details available in thei [issue](https://github.com/JuliaOpt/MathOptInterface.jl/issues/680)


#### Helpful Experience

- Basic knowledge of JuMP v0.20
- Prior work with optimization solvers


#### First steps

- Create a JuMP.print_bridge_graph that calls MOI.Bridges.print_graph: https://github.com/JuliaOpt/JuMP.jl/issues/2142
- Print MOI.Bridges.debug in the error message when a constraint is not supported in JuMP: https://github.com/JuliaOpt/JuMP.jl/issues/2143

###  Feasibility and Optimality checker

#### Abstract

JuMP and MathOptInterface (MOI) enable users to easily write Mathematical Programs (optimization models) and to solve them with a wide variety of solvers. Due to numerical issues and solver implementation choices, solvers differ significantly on how they define solutions, optimal points, locally optimal points, infeasible/feasible points, unbounded or ill-posed certificates, and so on. To be able to effectively compare solver performance, one needs to define common metrics of optimality and feasibility of constraints. In this project, we aim to systematize this comparison developing a set of (extensible) functions to evaluate and obtain information about solutions.

| **Intensity**                          | **Priority**              | **Involves**  | **Mentors**              |
| -------------                          | ------------              | ------------- | -----------              |
| Easy |  High  | Check feasibility and optimiality of optmization problems | [Chris Coey](https://github.com/chriscoey), [Joaquim Dias Garcia](https://github.com/joaquimg) and [Benoît Legat](https://github.com/blegat)|

#### Technical Details

We will develop tools to analyse feasibility and optimality of solutions of mathematical optimization models represented with MOI. Such tools will be made available and convenient for users at the MOI and JuMP levels, hence the main core will be developed in MOI and thin wrappers will expose the features through JuMP. We will fully document the new features.

Checking feasibility and optimality may be ambiguous tasks since many metrics can be used, therefore we hope to develop extensible functions, so that new metric can be incorporated in the future or implemented by users. For instance, optimality can of linear programs (LPs) can be checked by measuring primal dual gaps or complementary slackness conditions, provides a primal-dual feasible pair is given. Checking optimality.

These functions should be readily available for solver with problems loaded and “optimize” process completed, so the in-memory solution is tested and reports are generated. Also, there should be an interface to test user defined solutions. Starting points could also be tested.



#### Helpful Experience

- Basic knowledge of JuMP v0.20
- Understanding of main concepts of feasibility and optimality for linear programs is very important. The extension of these concepts to integer, conic, and non-linear programs is also helpful, but may be learned during the project.

#### First steps

- Understand how model data such as variables, constraints and solutions can be accessed from MOI.
- Explore how solvers like GLPK, Cbc, Gurobi, CPLEX, Xpress, SCS, MOSEK define their solution status metric
- Read Issue https://github.com/JuliaOpt/JuMP.jl/issues/693


### Optimization problem differentiation

#### Abstract

The goal of this project is to enable JuMP to differentiate the optimal solution of convex optimization problems with respect to its parameters. In other words, we need to obtain derivatives (or subgradients) of optimal solutions with respect to coefficients in the objective and constraints (http://reports-archive.adm.cs.cmu.edu/anon/anon/usr/ftp/2019/CMU-CS-19-109.pdf and https://arxiv.org/pdf/1904.09043.pdf).

This feature can enable the use of convex optimization problem within differentiable pipelines. One application is to use optimization problems as layers in a neural network (https://arxiv.org/pdf/1703.00443.pdf). More recently, this technique has been used in control (http://papers.nips.cc/paper/8050-differentiable-mpc-for-end-to-end-planning-and-control.pdf) and game theory (https://arxiv.org/abs/1805.02777).

A related project that may fall into scope is applying Automatica Differentiation (AD) to JuMP/MOI problems. This can be made to work if the solver is also written in Julia.

| **Intensity**                          | **Priority**              | **Involves**  | **Mentors**              |
| -------------                          | ------------              | ------------- | -----------              |
| Moderate |  Medium  | Differentiate solutions of Optimization problems | [Mario Souto](https://github.com/mariohsouto), [Joaquim Dias Garcia](https://github.com/joaquimg) and [Mathieu Besançon](https://github.com/matbesancon)|


#### Technical Details

As a reference, we should use the recently released CVXPY layers, https://github.com/cvxgrp/cvxpylayers, package that allows the user to automatic differentiate any convex optimization problem. More information about it can be found in the associated paper,  http://web.stanford.edu/~boyd/papers/pdf/diff_cvxpy.pdf. 

The goal is to develop a MOI extension capable of doing it and also make a JuMP-like interface available.

Potentially, it can be used in automatic differentiation packages in Julia. See for reference Zygote (https://github.com/FluxML/Zygote.jl), ForwardDiff (https://github.com/JuliaDiff/ForwardDiff.jl) and https://arxiv.org/abs/1907.07587.


#### Helpful Experience

Previous knowledge of convex optimization (https://en.wikipedia.org/wiki/Convex_optimization)

#### First steps

- read the paper: https://arxiv.org/abs/1910.12430
