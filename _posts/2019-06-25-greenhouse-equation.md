---
title: "The Greenhouse Equation"
tags: climate-change misc
---

 <script type="text/x-mathjax-config">
  (function () {

    MathJax.Hub.Config(
  				{ tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]},
  					processEscapes: true,
  					messageStyle: "none",
  					processSectionDelay: 0,
  					processUpdateTime: 0,
  					"fast-preview": {disabled: true},
  					TeX: { equationNumbers: {autoNumber: "AMS"},
  						   noErrors: {disabled: true},
  						   extensions: ["mhchem.js"]
  						  }
  				}
  	        );

  if (typeof MathJaxListener !== 'undefined') {
  	MathJax.Hub.Register.StartupHook('End', function () {
  		MathJaxListener.invokeCallbackForKey_('End');
  	});
  }

  })();
  </script>

  <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

![Glacier](https://media.graytvinc.com/images/690*388/Glacier+melt+-+MGN.jpg)

This is an account of the **Greenhouse Equation**,
as described on page 49 in chapter 5 of *A Farewell
to Ice* by Peter Wadhams.


Consider a black body at temperature $T$.  Temperature is measured
in degrees Kelvin (K).  A black body is a perfect emitter and absorber of radiant
energy (heat, light, microwaves, etc).  The rate at which energy is
emitted at all wavelengths by such a body per square meter is called its
*radiant flux*.  The radiant flux increases with temperature (think of
hot coals: dull red if not too hot, much brighter/whiter if you blow on them).
The precise dependence of radiant flux on temperatue is given by  the
Stefan-Boltzmann law (1855): radiant flux is  $\sigma T^4$, where
the constant $\sigma$ is about $5.67 x 10^{-8}$ watts per square meter per degree K to
the fourth power.

Let $\epsilon$ be the *emissivity* of a real body.  This is a q
between 0 and 1 that describes the deviation from the "ideal"
condition of a black body.  As we discuss below, the Earth with
no atmosphere is very nearly a black body: $\epsilon = 1$.
An atmosphere reduces the emissivity ($\epsilon < 1$), with the
precise value depending upon the nature of the atmosphere, e.g., the
mixture of gases that it contains.

The amount of energy emitted by body per unit time is its
radiant flux multiplied by its surface area.  Energy per unit time
has the units of power, measured in watts.  The radiant energy per unit time
emitted by a spherical body of radius $R$ is therefore

$$
E_{emitted} = 4 \pi R^2 \epsilon \sigma T^{4}
$$

In our case, $R$ = radius of the Earth.

The solar flux (incoming energy) at the radius of the  Earth's
orbit is $S = 1.37$ kilowatts per square meter.
We now ask: how much of that incoming energy is absorbed by the
Earth?  We know that certain fraction is reflected back into space,
while the rest is absorbed.  Let $\alpha$ be the fraction of
the energy whih is reflected.  This is called the *albedo*. As a point of reference,
the albedo of fresh snow is about $0.9$, while the albedo of open sea water
is about $0.1$.  The albedo of the Earth as a whole epends on cloud cover, the extent of the polar
ice caps, etc., but is presently about $0.3$.

We can calculate the amount of energy absorbed by the Earth per unit time:

$$
E_{absorbed} = \pi R^2 S (1 - \alpha)
$$

In the steady state,the incoming and outgoing flows
of energy — the absobed and emitted quantities — are in balance. Setting these quantities
equal to eachother and solving the resulting equation,
one finds that

$$
T^4 = \frac{1}{4\sigma} \frac{S(1 - \alpha)}{\epsilon}  \quad\quad (\text{Greenhouse Equation})
$$

Let's unpack the Greenhouse Equation.  First, note that  that the $R$'s cancel out.
Next, note that the factor $1/4\sigma$ is a physical constant.  There remain
three variables $S$, $\alpha$, and $\epsilon$  -— solar flux, albedo,
and emissivity.  These three variables determine the equilibrium temperature
of the Earth.

Let's first study the effect of changing emissivity and albedo.

## Exercise 1: assume no atmosphere

As a first exercise, suppose that $\alpha = 0.3$ and  $\epsilon
= 1$.  That is we take the albedo of the Earth to be about what it is now,
with regions of land, sea, and ice, but we assume that the
Earth has no atmosphere, and so acts as a black body.  Solving
for the temperature under these conditions yields

$$
 T = 255\ K
$$

This works out to about $-18$ degrees C.
The Earth without an atmosphere, with an emissitivy
of 1, would be very cold -- too cold to support life.
Atmosphere is more than a medium in which birds fly
and which supplies us with the oxygen that powers our
cells.

Let's continue playing with emissivity.

## Exercise 2: Add $\text{CO}_2$.

Adding $\text{CO}_2$ to the atomosphere lowers the emissivity of the Earth.
Why? Because $\text{CO}_2$ molecules absorb infrared radiation, converting
it into random molecular motion, i.e., heat.  The energy of the infrared radiation
that would normally be carried back into space is instead trapped in the atmosphere.
Q.E.D.   What is the effect?  Since $\epsilon$ appears in the
denominator of the Greenhouse Equation, the equilibrium temperature rises
as the emissivity decreases.

## Exercise 3: Melt the north polar ice cap.

If we melt the north polar ice cap, we decrease the albedo
of the Earth.  That is, we decrease $\alpha$, and therefore
increase $1 - \alpha$.  Conclusion: the equilibrium temperature
increases.

## Exercise 4: Change the behavior of the sun.

The solar flux $S$ is not constant: there is, for example,
the well-known 11-year solar cycle, the "sun-spot cycle," with an
associated cycle in energy flux (see reference [3]).
The relative increase in $S$ from valley to peak is about
0.002, or 0.2%.  However, because the cycle is a periodic —
or almost periodic — phenomenon, its long-term effect is very small,
likely zero: increases in solar flux in one half of the cycle
are balanced by decreases in the other half.

Not well understood, though much discussed, are longer period cycles and long term
drift in $S$, if any. Good data is hard to come by: the best measurements
are of recent origin, from space-based instruments. An interesting
but speculative approach is to study sun-like stars.

## Comments

1. We, the human race, have had an effect on emissivitiy by
adding $\text{CO}_2$ to the atmosphere.  The resulting
heating has reduced ice cover than therefore has indirectly
reduced albedo.  Human activity can affect emissivity and albedo,
but not the solar flux.

2.  Sadly, as we see with albedo, most of the climate feedback loops
are positive, rather than negative. Negative feedback, of which a thermostat
is an example, is a Good Thing.  Systems with negative feedback are stable.
Positive feedback is a Bad Thing in this context.
Systems with positive feedback are unstable. Read *runaway* and
imagine a mis-wired thermostat that increases the fuel fed to the
furnace as the temperatue rises.


## Note

The Kelvin scale of temperature is related to Centigrade by
the equation $T_C = T_K - 273.16$.  That is water freezes
at 273.16 degrees K.  Seems like an odd scale.  But: absolute
zero, or 0 degrees K, is the temperature at which all molecular
motion ceases (well, up to a small quantum effect). Absolutel
zero is also the temperature at which an ideal gas occupis zero
volume.


## References


1. A Farewell to Ice, by Peter Wadhams

2. [History of the Greenhouse Effect and Globl Warming](https://www.lenntech.com/greenhouse-effect/global-warming-history.htm)

3. [Solar Cycle Varation in Solar Irradiance](http://www2.mps.mpg.de/dokumente/publikationen/solanki/r72.pdf), by K.L. Yeo·N.A. Krivova·S.K. Solanki.
