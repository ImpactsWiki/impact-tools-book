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

# Catastrophic Disruption Scaling

When the specific energy (energy per unit mass) of a collision begins
to disturb the gravitational potential energy field of a body, then
the impact cratering scaling laws are no longer applicable, and
researchers transition to a scaling system based on a catastrophic
disruption curve.

Catastrophic disruption is jargon in the impact community that refers
to a criteria where the largest fragment has half the mass of the
target. It is usually denoted by a specific impact energy $Q^*$ in
J/kg. The criteria depends on the body's size, composition, and
velocity.

Later, the gravity regime scaling was modified to include the energy
necessary to disperse half the target mass, leading to the notation $Q^*_D$
{cite}`Melosh1997`. Finally, when dispersing half the total mass, the
notation is $Q^*_{RD}$, introduced in {cite}`Leinhardt2012`.

The classic derivation of the scaling law for both the
strength and gravity regime is {cite}`Housen1990`. This paper is an
amazing derivation of the catastrophic disruption curve, but it is
long and dense. This paper, based on numerical simulations, will be
more accessible for novice readers: {cite}`Benz1999`.

Example disruption curves for basalt and ice from {cite}`Benz1999`,
illustrating the dependence on impact velocity and transition from the
strength regime (downward sloping left side of the curve) and the
gravity regime (upward sloping right side of the curve). <p>

<img
src="https://drive.google.com/uc?export=view&id=1H95WXZQDuwglBsAhuxTZfKoTD-lKNhX6">

<img src="https://drive.google.com/uc?export=view&id=1J1bhj9pXLJYUI-yTsICmMvvvsjv3DAcJ">


## Online Catastrophic Disruption Tool -- Gravity Regime Only

<a href="https://sarahtstewart.net/resources/collision/"
target="_blank">Planetary Collision Calculator</a><p>
Reference for the equations behind this calculator:
{cite}`Leinhardt2012`

### Explanation of the Collision Outcome Regimes

Generally, the outcome of collisions between similar-sized bodies can
fall into some general categories: (1) perfect merging (negligible
mass in ejected fragments -- dark blue region in figure below); (2)
partial accretion (the larger body gains mass); (3) net erosion (the
larger body loses mass); (4) hit-and-run (small change to larger
body's mass). In the figure below, the thick black line with the
critical energy for half the combined mass remaining ($Q^*_{RD}$). The
outcomes depend on the mass ratio of the bodies, the impact
velocities, and the impact angle, where $b$ is the impact parameter
(sine of the impact angle where head on is 0 degrees). $V_{esc}$ is
the mutual escape velocity. $M_p$ is the projectile mass; $M_{targ}$
is the target mass; $V_i$ is the impact velocity. The impact angle
axis is normalized by probability (e.g., 1/4 of all events occur
between 0 and 30 degrees).

Figure 11 from {cite}`Leinhardt2012`<br>
<img
src="https://drive.google.com/uc?export=view&id=1DyewKCG_4KAebHi2I0IRgWUhMDs7MUXI">

The mass of the largest remnant is approximately linear with
normalized specific impact energy. At larger impact energies, the size
of the largest remnant falls of exponentially.<p>

Figure 3 from {cite}`Leinhardt2012`<br>
<img
src="https://drive.google.com/uc?export=view&id=1nAiK1aUrLH8Bi2CF4hdSLg0kA_igfAWy">

