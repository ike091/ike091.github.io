---
layout: post
author: Isaak Getz
tags: [monte-carlo, pi]
---

Recently, I took a scientific computing class, and during this class we talked
about Monte-Carlo methods for calculating various things. One of the things you
can compute with this method is pi, which I thought was pretty interesting.
All you need to do this is a few geometry formulas and the ability to randomly
generate points in space.

To start off, we'll take a look at the volume for a sphere (a similar method
could also be used with circles or higher-dimensional balls):

$$V_{sphere} = \frac{4}{3} \pi r^3$$

And the volume of a cube that perfectly surrounds said sphere (where $$l = 2r$$):

$$V_{cube} = (2r)^3 = 8r^3$$

Dividing the volumes of each shape results in a fraction of pi:

$$\frac{V_{sphere}}{V_{cube}} =
\frac{\frac{4}{3} \pi r^3}{8r^3} =
\frac{1}{6}\pi$$

We can then plot random points inside this cube/sphere to estimate the relative
volumes of each shape. We'll count the number of points that land inside the
sphere, versus the points that land inside the cube (which will be the same as
the total number of points). Since we know that dividing these volumes will
result in $$\frac{1}{6}\pi$$, we can approximate pi itself with the following
formula:

$$\pi \approx 6 * \frac{points\ inside\ sphere}{total\ points}$$

I wrote up a simple script to do this in python, and it worked quite well.
However, for higher sample sizes, things started to get extremely slow.
I also happen to be learning Go for a (very interesting) distributed systems
class I'm taking, and decided to rewrite this code in Go.
Maybe I'd even be able to add some parallelism.

Right off the bat, the directly translated serial program in Go was almost an
order of magnitude faster. Kind of an interesting illustration of how slow
python can be compared to compiled languages (although the running times of
these programs are probably largely dominated by random number generation, and
I'd have to look into the respective random implementations to really say
anything interesting).

