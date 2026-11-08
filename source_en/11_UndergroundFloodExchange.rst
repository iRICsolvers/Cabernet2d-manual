Linking to Underground Space (Multi-Level Flood Computation)
===================================================================

Cabernet2D can link a surface flood-inundation grid to a grid for an
underground space, such as an underground shopping area, through the
discharge exchanged at an opening such as a stairway or escalator. The
surface-level project and the underground-level project are each run as
separate computations, exchanging data through the discharge at the
opening.

Exit to a lower-level space (surface-level project)
---------------------------------------------------------

On the surface grid, an opening through which water flows down into the
underground space (a stairway, escalator, etc.) is set as an "Exit to
lower-level space cells." The outflow computed here is used as the inflow
condition for the underground-level project.

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Total opening width (ug_width)
     - The total width of the opening (m)
   * - Sill elevation (ug_base)
     - The sill elevation of the opening (m)
   * - Coefficient c1 / Exponent c2 (ug_c1, ug_c2)
     - The coefficient and exponent of the empirical outflow formula
       :math:`Q = c_1 \cdot B \cdot H^{c_2}`. The default values
       (c1=1.59, c2=1.65) come from the stairway inflow experimental
       formula in the MLIT (Japan) guideline "Guideline for Flood
       Prevention Measures in Underground Space."
   * - Specify direction (ug_dir_yesno) / Direction (ug_direction)
     - Whether to specify the outflow direction from one of four
       directions (+i, -i, +j, -j), and which one. Because this opening is
       a sink, the direction means the direction water travels as it is
       drained (for example, specifying the +i direction means water
       enters the exit cell(s) from the -i side and is drained toward
       +i). Any face not specified is automatically closed (impermeable).

Inflow point from the upper-level space (underground-level project)
--------------------------------------------------------------------------

In the underground-level project, the outflow computed on the surface side
(as a time series) is set as an inflow point, "Inflow from upper-level
space cells."

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Specify direction (ue_dir_yesno) / Direction (ue_direction)
     - Whether to specify the inflow direction from one of four
       directions, and which one. Because this inflow point is a source,
       the direction means the direction water flows out of the entrance
       cell(s). Any face not specified is automatically closed
       (impermeable).
   * - Inflow discharge time series (ue_qin)
     - The time series of the inflow discharge (m3/s). Enter here the
       discharge computed at the exit cells of the surface-level project.

Workflow
-----------

1. In the surface-level project, set up the "Exit to lower-level space"
   cells and run the computation to obtain a time series of the outflow
   discharge.
2. Enter the resulting discharge time series into the "Inflow discharge
   time series" of the "Inflow from upper-level space" cells in the
   underground-level project.
3. Run the underground-level project to compute the flood conditions
   inside the underground space.

Because the surface and underground computations are run separately,
mutual feedback (for example, the underground water level affecting the
surface outflow) is not automatically taken into account. Adjust the
discharge settings as needed while checking the results.
