---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# User Manual for IM Tool

This is a one-dimensional shock impedance matching calculator. The program is written in python 3 and uses the <a href="https://panel.holoviz.org/" target="_blank">panel package</a> to generate interactive widgets.

The impedance match solution is the unique intersection point defined by the designated impact velocity and each material's shock Hugoniot. The solution provides the state in each material that satisfies continuity in pressure and particle velocity at the interface. In subsequent layers, the shock/reshock Hugoniots and/or release isentropes define the unique states that are continuous in pressure and particle velocity at each interface. 

The tool includes the ability to plot, fit and add data from the online Shock Wave Database at http://www.ihed.ras.ru/rusbank/ ({cite}`Levashov2004`). 

## Quick Start
The IM Tool can be run in three different ways:
* As a web app on Heroku (response can be a little slow): <a href="https://impedance-match-app.herokuapp.com/" target="_blank">impedance-match-app.herokuapp.com</a>

* From the Jupyter Book page {ref}`IM_Tool`: Launch CoLab; run the notebook

* On your local computer: <a href="https://github.com/ImpactsWiki/impact-tools-book" target="_blank">Download the repo</a> and run the Jupyter Notebook locally

Select 2, 3, or 4 materials.<br>
Enter impact velocity for material 1 onto material 2.<br>
Changing the impact velocity initiates a new calculation and plot.<br>

## Hugoniot Equations

The IM Tool defaults to using the Hugoniot to also represent release and reshock. This approximation generally provides robust solutions to a reasonable problem configuration. 

There are 3 built-in equation forms for the shock Hugoniot that relate particle velocity $u_p$ and shock velocity $U_S$. For each material entry, the number of non-zero parameters determines the form for the Hugoniot:
* 2 parameters = Linear: $U_S = c_0 + s_1  u_p$
* 3 parameters = Quadratic: $U_S = c_0 + s_1  u_p + s_2  u_p^2$
* 4 parameters = Modified Universal Hugoniot: $U_S = c_0 + b  u_p - c  u_p e^{(- d  u_p)}$

Then the shock state variables $(P_H,V_H,E_H)$ are calculated from the Rankine-Hugoniot equations

$$
P_H & = P_0 + \rho_0 u_p U_S, \\
E_H & = E_0 + \frac{P_0+P_H}{2} \left[V_0-V_H \right], \\
V_H & = V_0 \left[ 1 - \frac{u_p}{U_S} \right],
$$

where $P_0=0$, $E_0=0$, and $V_0=1/\rho_0$.

## Material Database Format

The default material database file is named <i>materials-data.csv</i>. The material database is a comma separated text file with one line for each material. Each entry contains:
* Material = Short material name
* Density(g/cm$^3$) = density at initial state
* rho0_err
* c0(km/s) = Hugoniot parameter
* c0_err
* s1 or b = Hugoniot parameter
* s1_err
* s2(s/km) or c = Hugoniot parameter
* s2_err
* d(s/km) = Hugoniot parameter
* d_err
* g0 = Mie-Gr&uuml;neisen parameter at initial state
* g0_err
* q = Mie-Gr&uuml;neisen equation exponent
* q_err
* up_low(km/s) = minimum particle velocity for Hugoniot fit
* up_high(km/s) = maximum particle velocity for Hugoniot fit
* IHED_id = IHED database substance ID number
* Date = YYYY-MM-DD
* Notes

The database is in km/s for velocities and g/cm$^3$ for density. These parameters are converted to mks and all calculations are done in mks. The parameter uncertainties are not used at this time and are placeholders for future error propagation.

## Add or Remove Materials Panel
The user can add new materials on-the-fly in the parameter entry panel in either the web app or the 
Alternatively, when running the Jupyter notebook, you can replace the <i>materials-data.csv</i> file with your own database.

Materials can also be removed from the database. 

## Built-in Functions
The IM_module contains several functions to plot and fit Hugoniot data. The material models are modular for future expansion to different forms for the equation of state (e.g., functions for the quartz standard, ANEOS models, and tabulated EOS). Hence, the program numerically solves for the intersection points at each material interface.

Error messages are hidden when running the web app. Problems can be diagnosed by calling the functions in the Jupyter Notebook. Examples of using the IM functions are in the {ref}`Play-Space`. More than 4 layers of materials can be calculated using a series of calls to the IM_match function.

## Mie-Gr&uuml;neisen Model for Reshock and Release
The IM Tool defaults to using the Hugoniot to also represent release and reshock. This approximation generally provides robust solutions for reasonable problem configurations. 

Alternatively, a simple Mie-Gr&uuml;neisen model can be used for reshock and release (e.g., see Chapter 5 in {cite}`Forbes2012`). The thermal Gr&uuml;neisen parameter $\gamma$ is given by

$$ 
\gamma(V) = V \left[\frac{dP}{dE}\right]_V, \label{eq1}\tag{1}
$$

where $\gamma$ is often assumed to only depend on volume. Note that parentheses are used to denote dependent variables.

In the IM Tool, the functional form for the Gr&uuml;neisen parameter is currently limited to

$$
\gamma(V)= \gamma_0 \left[V/V_0\right]^q. \label{eq2}\tag{2}
$$

The options for the form for the Gr&uuml;neisen parameter will be expanded as new equation of state options are developed.

The Mie-Gr&uuml;neisen equation of state defines a thermal pressure term, $P(V,E)$, at specific volume $V$ and specific internal energy $E$ referenced to a known state at $V$, which in this case is the principal shock Hugoniot with pressure $P_H(V)$ and specific internal energy $E_H(V)$. Then the thermal pressure term is given by 

$$ 
P(V,E) = P_H(V)+\frac{\gamma(V)}{V} \left[E(V)-E_H(V)\right]. \label{eq3}\tag{3}
$$

A single shock must satisfy the Rankine-Hugoniot (R-H) conservation equations between an initial state, $s_0$, and the shock state, $s_H$. The initial state $s_0$ is defined by the state variables: specific volume $V_0$, presure $P_0$, and specific energy $E_0$ (which then specifies the initial specific entropy $S_0$ and temperature $T_0$). Note the tabulated initial value for the Gr&uuml;neisen parameter $\gamma_0$ must correspond to state $s_0$. The R-H energy conservation equation is 

$$ 
E_H(V)=E_0+\left[\frac{P_0+P_H(V)}{2}\right]\left[V_0-V\right]. \label{eq4}\tag{4}
$$

Combining these two equations defines the Mie-Gr&uuml;neisen equation of state surface, which is limited to the volume range where $P_H(V)$ is defined,

$$
P(V,E) & =  P_H(V)+\frac{\gamma(V)}{V}\left[E(V)-E_0\right] - \left[P_0+P_H(V)\right]\frac{\gamma(V)}{2V}[V_0-V]  \\
       & =  \frac{\gamma(V)}{V}\left[E(V)-E_0\right] + P_H(V)\left\{ 1- \frac{\gamma(V)}{2V}\left[V_0-V\right] \right\}
        - \frac{P_0\gamma(V)}{2V}\left[V_0-V\right],\label{eq5} (5)
$$

and the last term is dropped when $P_0=0$. The IM Tool assumes $E_0=0$ and $P_0=0$ and $V_0=1/\rho_0$, where $\rho_0$ is the initial density in the material database.

### Reshock (Recentered) Hugoniot

A second shock originating from a first shock state must also satisfy Equations 3 and 4. The initial state is $s_1$ on the principal Hugoniot $P_H(s_1)$. The possible reshock states, denoted $_{RS}$, are a locus of states that satisfy the energy conservation equation

$$
E_{RS}(V) = E_H(V_1) + \frac{P_H(V_1)+P_{RS}(V)}{2} \left[V_1-V\right].\label{eq6}\tag{6}
$$

The specific energy in state $s_1$ is given by

$$
E_H(V_1)=E_0+\left[\frac{P_0+P_H(V_1)}{2}\right]\left[V_0-V_1\right].\label{eq7}\tag{7}
$$

Combining Equations 6 and 7,

$$
E_{RS}(V_2)-E_0 = \frac{P_0+P_H(V_1)}{2}\left[V_0-V_1\right] + \frac{P_H(V_1)+P_{RS}(V_2)}{2}\left[V_1-V_2\right].\label{eq8}\tag{8}
$$

Then using Equation 5 with $P_0=0$, the state $s_2$ (with $E_2=E(V_2)$) has the general solution

$$
P(V_2,E_2)  = \frac{\gamma(V_2)}{V_2}\left[E_2-E_0\right] + P_H(V_2)\left\{ 1- \frac{\gamma(V_2)}{2V_2}\left[V_0-V_2\right] \right\}.\label{eq9}\tag{9}
$$

Substitute Equation 8 into 9 to find solutions that describe a shock from $s_1$ to $s_2$ (with $E_2=E_{RS}(V_2)$) and simplify

$$
P_{RS}(V_2,E_2) &  = \frac{\gamma(V_2)}{V_2}\left[E_{RS}(V_2)-E_0\right] + P_H(V_2)\left\{ 1- \frac{\gamma(V_2)}{2V_2}\left[V_0-V_2\right] \right\}, \\
P_{RS}(V_2)     & = \frac{P_H(V_1)+ \left[ P_H(V_2) - P_H(V_1) \right]\frac{\gamma(V_2)}{2V_2} \left[V_0-V_2\right]}{1-\frac{\gamma(V)}{V_2}  \left[ V_1-V_2 \right]} (10)
$$

The R-H equations provide the corresponding solutions for the changes in specific energy and particle velocity, $u_p$, from $s_1$ to $s_2$:

$$
E_{RS}(V_2) & = E_H(V_1) + \frac{P_H(V_1) + P_{RS}(V_2)}{2} \left[V_1-V_2\right], \\ 
u_{p,RS}(V_2) & = u_{p,H}(V_1) - \sqrt{ \left[P_{RS}(V_2)-P_H(V_1)\right] \left[V_1-V_2\right]}. 
$$

### Release Isentrope

An isentrope can be calculated using the Mie-Gr&uuml;neisen equation of state by an interative calculation from a known point on the Hugoniot $s_1$. 

For a reversible isentropic ($dS=0$) process, the first law of thermodynamics stipulates

$$
dE = T dS - P dV = -P dV.\label{eq11}\tag{11}
$$

Then, for a small $\Delta V=V_i-V_{i-1}$ along the isentrope,

$$
E_S(V_i) - E_S(V_{i-1}) = - \frac{1}{2} \left[P_S(V_i) + P_S(V_{i-1}) \right] \left[ V_i-V_{i-1} \right].  \label{eq12}\tag{12}
$$

Substituting Equation 12 into Equation 3 and simplifying for the pressure along the isentrope $P_S$:

$$
P_S(V_i) & = P_H(V_i) + \frac{\gamma(V_i)}{V_i} \left[ E_S(V_{i-1})-  \frac{1}{2} \left[ P_S(V_i)+P_S(V_{i-1}) \right]  \left[ V_i - V_{i-1} \right] - E_H(V_i) \right], \\
         &  = \frac{P_H(V_i) + \frac{\gamma(V_i)}{V_i} \left[ E_S(V_{i-1})-E_H(V_i) - \frac{1}{2} P_S(V_{i-1})\left[V_i-V_{i-1}\right]\right]}{1+\frac{\gamma(V_i)}{2V_i} \left[V_i-V_{i-1}\right]}
$$

Finally the change in particle velocity along the isentrope is given by the Riemann integral, 

$$
u_{p,S}(V) & = u_{p,H}(V_1) - \int_{P_H(V_1)}^{P_S(V)} \frac{dP}{\sqrt{- \left[ \partial P/\partial V \right]_S}} \\
           & = u_{p,H}(V_1) - \int_{P_H(V_1)}^{P_S(V)} \frac{V}{c_s} dP,
$$

which is also calculated iteratively with $\Delta V$.

## Calculating Intersections

To keep the code modular, the intersections between Hugoniots, reshock Hugoniots, and release isentropes are calculated numerically using the function from <a href=" https://github.com/sukhbinder/intersection/" target="_blank"> https://github.com/sukhbinder/intersection/</a>.

