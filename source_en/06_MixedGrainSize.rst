Mixed Grain Size Bed Material
================================

Overview
-----------

Real riverbed material is rarely a single grain size. Coarse particles are
harder to move and tend to remain on the bed surface, causing armoring, while
fine particles are selectively washed away. As a result, the grain size
composition of the bed changes over time and space depending on the flow
conditions. Cabernet2D can account for this evolving grain size composition
in the bed variation calculation, configured in the "Bed Material / Mixed
Grain Size" tab of the calculation conditions.

.. list-table::
   :header-rows: 1
   :widths: 10 30 60

   * - GUI option
     - Name
     - Description
   * - (0)
     - Uniform grain size
     - The simplest setting: the bed material is treated as a single
       representative grain size.
   * - (1)
     - Mixed grain size
     - The bed material is treated as a mixture of several grain size
       classes, and the fraction of each class in the exchange layer
       evolves over time.

The exchange layer concept
------------------------------

In the mixed grain size calculation, the bed is divided into an "exchange
layer" (a surface layer that exchanges sediment with the flow) and the
material below it. The exchange layer keeps track of the fraction
:math:`p_k` of each grain size class. As erosion and deposition proceed, the
grain size composition of the exchange layer is updated, which in turn
affects the per-class transport calculation (critical shear stress and
bedload formula evaluation for each grain size class).

In the GUI, the thickness of this layer is set with "Exchange layer
thickness (m)".

Entering the grain size distribution
----------------------------------------

The grain size composition is entered in the "Grain size distribution"
table of the GUI. The input format is selected with "Grain size input
type".

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Input format
     - Description
   * - (0) Fraction (%)
     - Each row gives the percentage of that grain size class in the total
       bed material. All values must sum to 100% (auto-normalized if not).
       Example: d=0.15mm: 10%, d=0.30mm: 20%, d=0.43mm: 40%,
       d=0.61mm: 20%, d=0.86mm: 10%
   * - (1) Cumulative passing (%)
     - Each row gives the percentage of material finer than that grain size
       (sieve analysis format). Values must be monotonically increasing
       (grain sizes are automatically sorted in ascending order).
       Example: d=0.15mm: 10%, d=0.30mm: 30%, d=0.43mm: 70%,
       d=0.61mm: 90%, d=0.86mm: 100%

Both formats are internally converted to fractions summing to 1.0 before
computation.

Friction parameters
-----------------------

The frictional properties of the bed material are set with the following
parameters.

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Parameter
     - Description
   * - Static friction coefficient
     - Default value 1.0.
   * - Kinematic friction coefficient
     - Default value 0.5.

.. note::

   Reducing these values increases the gravitational effect of the
   bedload, smoothing out irregularities of the riverbed. Be cautious:
   making them too small may cause the desired microtopography to
   disappear.

Output
---------

When the mixed grain size calculation is enabled, the following
representative grain sizes are output as results.

- Mix mean grain size dm (mm): the weighted mean grain size of the
  exchange layer
- Mix grain size d10 (mm) / d50 (mm) / d90 (mm): the grain sizes
  corresponding to 10%, 50% and 90% cumulative passing

These outputs let you track how the bed surface coarsens or fines as the
calculation proceeds.
