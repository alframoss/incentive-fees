# Incentive Fees in Hedge Fund Management

This GitHub repository contains all the work related to my masters thesis.

## Introduction

We consider an expected utility maximising manager who controls the allocation of wealth between a riskless and risky asset. The manager has power utility describing their terminal wealth preference. The manager’s compensation includes both a management fee and a performance fee based on exceeding the high-water mark of the fund. Under assumptions about the continuous-time financial market and the asset prices, we present a numerical solution of the optimal trading strategy.

## Problem Formulation

Using a dynamic programming method, similar of that to solving the Merton problem, we show that a solution to the manager's optimal control problem is also a solution to a partial differential equation. We find a solution to this equation, known as the Hamilton-Jacobi-Bellman (HJB) equation, using finite difference. To understand the details of this contruction, please read the document titled `MA4K9_Project_U2007120.pdf`. The equation for the value function $V^c(t, x)$ is
$$-\frac{\partial V^c}{\partial t}(t, x)-\sup_{\pi\in\mathcal{A}(t, x)}\left[(rx+\sigma\lambda\pi_t)\frac{\partial V^c}{\partial x}(t, x)+\frac{1}{2}\sigma^2\pi_t^2\frac{\partial^2 V^c}{\partial x^2}(t, x)\right]=0,$$
with terminal condition
$$V^c(T, x)=\Phi^c(x, B_T)\quad\forall x\in\mathbb{R}.$$
Maximising over $\pi$ yields the optimal feedback control function
$$\hat\pi(t, x)=-\frac{\lambda}{\sigma}\frac{V_x^c(t, x)}{V_{xx}^c(t, x)},$$
and the partial differential equation
$$V_t^c(t, x) + rxV_x^c(t, x) - \frac{\lambda^2}{2}\frac{\left(V_x^c(t, x)\right)^2}{V^c_{xx}(t, x)} = 0.$$

## Numerical Approximation

We use a naive finite difference method to numerically approximate these partial differential equations. Using forward Euler approximations in time and central Euler approximations in space we obtain
$$V_i^{j+1} = V_i^j+\frac{rh}{2}\left(V_{i+1}^j-V_{i-1}^j\right)-\frac{\lambda^2h}{8}\frac{\left(V_{i+1}^j-V_{i-1}^j\right)^2}{V_{i+1}^j - 2V_i^j + V_{i-1}^j}\quad0\leq j\leq N\quad 1\leq i\leq M,$$
with boundary conditions
$$V_i^0=\Phi^c(ik, B_T)\quad0\leq i\leq M,$$
$$V_0^j=U(K)\quad0\leq j\leq N.$$
For the approximation of the optimal control, we obtain
$$\hat\pi_i^j=-\frac{\lambda k}{2\sigma}\frac{V_{i+1}^j-V_{i-1}^j}{V_{i+1}^j-2V_i^j+V_{i-1}^j}\quad0\leq j\leq N\quad 1\leq i\leq M-1.$$

The document `22052024_MA4K9_code.ipynb` is a workbook that contructs these finite difference grids using dynamic programming.

## Results

Please read Chapter 6.4 in `MA4K9_Project_U2007120.pdf` to understand the economic significance of this workbook.
