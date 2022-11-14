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

# Impact Cratering Scaling Laws

Most crater scaling laws are based on deriving (typically power-law)
relationships between non-dimensional variables, which are constructed
using Buckingham Pi theory. Here is a <a
href="https://drive.google.com/file/d/1R9gNLZGYjFNfGHO0vxk703aYqFLNI3y1/view?usp=sharing"
target="_blank">brief introduction to the
Buckingham Pi Theorem</a>. Here is an <a
href="https://www.atmosp.physics.utoronto.ca/people/codoban/PHY138/Mechanics/dimensional.pdf"
target="_blank">example of using this approach to
calculate the energy of an explosion</a>. 

Classic introduction to using pi-scaling approaches for impact
cratering: {cite}`Holsapple1993`

See also Chapter 7 in Melosh's Impact Cratering book
{cite}`Melosh1987` (The book is out of print; <a href="https://drive.google.com/file/d/1ucbtjJWBGkYtJzkuhjWJe0ysmsxeTGtP/view?usp=sharing" target="_blank">PDF is here</a>)



## Online crater scaling tools

Note that the first two online calculators assume a gravitational accelartion
for the Moon and Earth, respectively. To first order, the transient
crater size on other bodies is scaled by the ratio of the gravitational accelerations.
<ul>
<li>Moon only: <a
href="https://www.lpi.usra.edu/lunar/tools/lunarcratercalc/" 
target="_blank">Lunar
Cratering Calculator</a> -- an
<a href="https://www.lpi.usra.edu/lunar/tools/lunarcratercalc/theory.pdf"
target="_blank">explanation of the equations</a> behind the
calculator </li>
<li>Earth only: <a href="https://impact.ese.ic.ac.uk/ImpactEarth/ImpactEffects/" 
target="_blank">Earth
Impact Effects Program</a> -- <a
href="https://impact.ese.ic.ac.uk/ImpactEarth/ImpactEffects/effects.pdf"
target="_blank">explanation of the equations</a></li>
<li>Any body: <a
href="https://www.eaps.purdue.edu/impactcrater/index.html" target="_blank">Crater
scaling from impact parameters or from final crater size</a> </li>
</ul>

### WARNINGS! Things to keep in mind

These scaling laws are developed in a homogeneous, flat (planar)
surface. They do not account for crust-mantle transition or curvature
of a body and its gravity field. Thus they are not applicable for
events between similar sized bodies. In these cases, the
{doc}`disruption` is more appropriate.

The outcomes of impacts are sensitive to the magnitude of the impact
velocity. The absolute velocity has a relatively small effect on
scaling the size of the transient crater. It has a larger effect on
scaling the amount of melting and vaporization, because shock-induced
melting and vaporization requires reaching specific peak pressures.


## Explanation of Parameters

Figure 2 from {cite}`Collins2005`<p>

<img src="https://drive.google.com/uc?export=view&id=157WDCDPSm9iI14gBQS3P9k1M9FuZAKiB">

## Melting and Vaporization during Impact Cratering

The energy in the shocked state is given by the conservation
equation:

$E-E_1 = (1/2)(P+P_1)(V_1-V)$

The irreversible work is the energy in the shock wave minus the energy
recovered during decompression. If the irreversible work is
sufficiently great, the material may reach the melting point (or
boiling point) after release to ambient pressures.

Key paper on estimating the amount of melting and vaporization during
impact cratering: {cite}`Pierazzo1997` (newer calculations in
{cite}`Barr2011` and {cite}`Kraus2011`).

Example of impact pressures needed to melt and vaporize ice from {cite}`Kraus2011`:
<img src="https://drive.google.com/uc?export=view&id=13habboP66O9evW71xfYsGOkS-J1zPfr6">


