Material Transport (Dye Diffusion and GELATO)
===================================================

Independent of the flow and bed variation computations, Cabernet2D offers
two features for handling material introduced into the water (such as
dye) and particles that move with the flow (such as drifting debris or
tracked suspended-sediment particles).

Dye advection-diffusion computation
-----------------------------------------

In the "Dye Advection and Diffusion" calculation condition tab, you can
compute how a dye (tracer) injected at a specific location advects and
diffuses within the computed flow field.

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Diffusion and transportation of dye (j_dye)
     - Whether to enable the dye advection-diffusion computation
   * - Start time of dye injection (start_dye)
     - The injection start time (sec)
   * - End time of dye injection (end_dye)
     - The injection end time (sec)
   * - Concentration injecting dye (dye_in)
     - The concentration of the injected dye
   * - Diffusion coefficient multiplying factor (coef_dye)
     - A multiplier applied to the diffusion coefficient

The injection location is specified on the grid as a "dye injection cell"
grid condition.

GELATO (particle tracking model)
--------------------------------------

GELATO (General Lagrangian Tracer Tracking) is a model that tracks the
trajectory of particles (tracers) carried by the flow in a Lagrangian
manner, separate from the Eulerian flow computation. It can be used, for
example, to visualize the transport path of drifting debris or tracked
suspended-sediment particles.

Basic settings
~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Gelato Activate (j_gelato)
     - Whether to enable the GELATO computation
   * - Velocity using for Gelato (j_gelVel)
     - The velocity used to move the particles: depth-averaged velocity /
       surface velocity / near-bottom velocity
   * - Maximum Tracer Numbers (max_tNumber)
     - The maximum number of tracked particles

Particle behavior
~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Minimum depth below which tracer stops (hminTrace)
     - The depth threshold (m) below which a particle stops moving
   * - coefficient for sediment suspension (alpha_uswf)
     - A coefficient controlling how readily a particle is entrained as
       suspended sediment
   * - How to specify the fall velocity (j_wf)
     - How the fall velocity is given: using the Rubey formula / entered
       directly
   * - Diameter for Rubey formula (d_Rubey)
     - The grain diameter (m) used in the Rubey formula
   * - Fall velocity for Gelato (wf_Gelato)
     - The directly specified fall velocity (m/s)
   * - A value in D=A Nu + B / B value (a_diff, b_diff)
     - Coefficients for giving the diffusivity as a linear function of the
       eddy viscosity :math:`\nu_t`: :math:`D = A\nu_t + B`
   * - Time step for Gelato (ddt)
     - The time step of the particle tracking computation

Particle release conditions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the "General Lagrangian Tracer Tracking(2)" tab, you specify the time
range (start, end, and step) over which particles are released, and the
release location as a range in non-dimensional grid coordinates (Xi:
streamwise direction, Eta: transverse direction).

Related feature: vegetation block tracking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The "Vegetation Block Tracking" tab provides a feature that tracks lodged
or washed-out clumps of vegetation (driftwood-like masses) using the same
approach as GELATO. Combined with the vegetation model
(:doc:`07_VegetationAndBankCollapse`), this lets you track where
washed-out trees end up downstream.
