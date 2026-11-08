Computation Settings (Artificial Viscosity, Hot Start / OpenMP)
======================================================================

Artificial viscosity for the flow computation
----------------------------------------------------

In the "Artificial Viscosity for Water Surface / Flow Calculation" group
of the "Artificial Diffusion (Flow Calc.) and Drop Parameters" calculation
condition tab, you set the artificial viscosity used to stabilize the
water-surface and flow computation. This is distinct from the artificial
viscosity used in the bed variation computation (see the slope-failure
section of :doc:`07_VegetationAndBankCollapse`, and the bedload artificial
viscosity coefficient art_visc_coef).

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Water surface (j_adiff)
     - Whether to enable artificial viscosity for the water-surface
       computation
   * - Type of artificial viscosity (j_hdiffType)
     - How the viscosity coefficient is given: a constant value / a
       function of the maximum velocity and grid size
   * - Viscosity coefficient (hdiff)
     - The value of the viscosity coefficient (when a constant value is
       chosen)

Side-wall and obstacle friction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the same tab, the "Side-Wall / Obstacle Friction" group sets the
friction coefficient (cw) for side-wall and obstacle surfaces. A larger
value damps the velocity near the wall more strongly.

Hot start (restarting a computation)
------------------------------------------

The "Hot Start / OpenMP" calculation condition tab lets you save the
progress of a computation to a temporary file and resume from it later.
This is useful when you want to split a long computation into stages, or
to resume a computation that was interrupted.

Output of temporary files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Output temporary files (write_flag)
     - Whether to output temporary files
   * - Temporary File Path (tmp_pass)
     - The folder in which temporary files are saved
   * - Number of temporary files (n_tempfile)
     - The number of temporary-file generations to keep (1-10). The
       specified number of generations is reused and overwritten in turn.
   * - Time unit of temporary output (i_tmp_out_unit)
     - The unit of the output time (second / hour / day / month / year)
   * - Output time of temp file 0-4 (outtime_tmp0-4)
     - The time at which each generation of the temporary file is output

Resuming a computation
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Calculate from initial or temporary file (read_flag)
     - How the computation starts: from the initial state (Initial) / from
       a temporary file (Restart)
   * - Input Temporary File Name (tmp_readfile)
     - The temporary file to resume from (set when read_flag is Restart)

.. note::

   A computation resumed from a restart inherits the saved flow field,
   bed, vegetation and other state, but the calculation conditions
   (boundary conditions and various parameters) are those of the project
   that is currently open. You can therefore change conditions before
   resuming.

Parallel computation (OpenMP)
-----------------------------------

In the same tab, "Number of threads for parallel computation
(n_parallel)" sets the number of threads used for OpenMP parallel
computation. Setting this according to the number of CPU cores available
can reduce the computation time.
