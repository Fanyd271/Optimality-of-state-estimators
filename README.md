# Optimiality of Set-based Robust State Estimators
This repo includes all experimentes implemented in the paper "Theoretical Relationship of Set-Based Robust State Estimators: An Optimality Perspective" accepted by 
the IEEE Transactions on Automatic Control as the Technical Note. Please check the data and test some experiments to complement the paper.

> Theoretical Relationship of Set-Based Robust State Estimators: An Optimality Perspective
>
> [Yidian Fan](https://Fanyd271.github.io), Feng Xu
> 
> Contact: Yidian Fan (fyd20@tsinghua.org.cn), Feng Xu (xu.feng@sz.tsinghua.edu.cn)

## Contents
- [Pre-requisites](https://github.com/Fanyd271/Optimality-of-state-estimators#Pre-requisites)
- [Organization Structure](https://github.com/Fanyd271/Optimality-of-state-estimators#Organization-Structure)
- [Quick start](https://github.com/Fanyd271/Optimality-of-state-estimators#Quick-start)
- [News](https://github.com/Fanyd271/Optimality-of-state-estimators#News)
  
## Pre-requisites
+ Example codes uses [MATLAB R2019b or higher](https://www.mathworks.com/products/matlab.html), [MPT Toolbox](https://www.mpt3.org/), [CVX](http://cvxr.com/)
+ Additional care should be taken to the MPT3 toolbox. We detected a bug in the file "mtimes.m", which is in the installation subdirectory
  "\tbxmanager\toolboxes\mpt\3.2.1\all\mpt3-3 2 1\mpt\modules\geometry\sets\@Polyhedron\mtimes.m"
  of the MPT3 toolbox. This function deals with the operation that a scalar $\alpha$ times a polyhedron $P=\lbrace x|Ax\leq b\rbrace$.
  The 125th line makes $\alpha P=\lbrace x|Ax\leq \alpha b\rbrace$, which is only valid when $\alpha\geq 0$.
  The correct form is $\alpha P=\lbrace x|\frac{1}{\alpha}Ax\leq b\rbrace$, $\forall \alpha\neq 0$.

## Organization Structure
This repo has one main directory with eight subdirectories, whose roles are listed as follows.
- Main directory: The main files that conduct large-scale numerical tests on the systems.
  - Twotank_intense_test.m: Run large-scale tests on the two-tank system.
  - Fourtank_intense_test.m: Run large-scale tests on the four-tank system.
  - main.m: Run one sampling case to debug or visualize the result.
  - Verification.m: Compute the approximation accuracy of the proposed algorithms by optimization programs.
- Data: The stored numerical results of the experiments described in the manuscript and Answer sheet.
- Error_data_twotank, Error_data_fourtank:The intermediate results of cases in which the MPT3 reports errors. These data are reserved for debugging and illustrating
  the limits of the MPT3.
- Warning_data_fourtank, Warning_data_twotank: The intermediate results of cases in which the numerical errors of the proposed algorithms are relatively large.
  The leading cause is the numerical inaccuracy of the MPT3 toolbox.
- Systems: The parameters of the numerical systems, including the two-tank, four-tank.
- Toolbox: Matlab functions utilized in the program.
  - Box.m: Generates the minimal interval that encloses a given polytope $P$, i.e., $\square(P)$.
  - Compute_SESs.m: Computes the state estimation sets (SES) $X_{k+1}^P$ and $X_{k+1}^I$ given the observer bundles $\mathbb{L}_k$ and $\mathbb{LS}_k$.
  - IO_opt.m: Solve $\mathbb{LS}_k$ of the linear-time invariant (LTI) system.
  - L_opt.m: Solve $\mathcal{L}(v;X_k)$ given the direction $v$ and the SES $X_k$. See Theorem 4.1 for details.
  - mRep.m: Solve the mH-Rep and mV-rep of a given polytope. This procedure is intended to reduce the representational complexity of each intermediate polytope in the SME process.
  - Normalize: Normalize the outward normals of the polytope ($\|h_i\|=1$) to make sure the numerical errors  of all facets are of the same scale. See Sec. V in the manuscript.
  - Plot_sets.m: Plot the resulting SESs $X_{k+1}^M$, $X_{k+1}^P$, and $X_{k+1}^I$ of the LTI system.
  - Select_vertices.m: Solve the vertice $P(v;X_k)$ given the direction $v$ and SES $X_k$. See Lemma 2.4 in the paper.
  - Smatrix.m: Solve the coordinate transformation matrix $T_k=\mathcal{T}(v,L_k)$ given the direction $v$ and observer gain $L_k$. See Lemma 4.7 in the main content.
  - Support_func.m: Compute the support function $S(v;X)$.
  - SVO_opt.m: Solve $\mathbb{L}_k$ of the LTI system.
  - zonotope.m: Generates a zonotope with G-rep $Z(c,G)=\{c+G\xi|\|\xi\|_{\infty}\leq 1\}$. This function can be utilized to generate symmetric and complicated uncertainty sets.

## Quick start
+ Run "main.m" to see the experimental result of one sampling case on the two-tank system. The numerical accuracy of the proposed algorithms is reported,
   and the resulting state estimation sets are plotted. 
+ Run "data_load.m" to visualize the outcomes of the large-scale numerical tests.

## News 
- [24-01-20] :v: Our work is accepted by the IEEE Transaction on Automatic Control.
