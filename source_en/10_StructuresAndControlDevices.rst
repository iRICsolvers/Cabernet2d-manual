Structures (Drop Structures, Culverts, Gates, Pumps)
=========================================================

Cabernet2D has a feature for handling topographic drops in the channel,
such as grade-control structures, and a feature for connecting two points
within the computational domain through an artificial discharge, such as
culverts, gates and pumps.

Vertical drop structures
----------------------------

Energy loss at a drop
~~~~~~~~~~~~~~~~~~~~~~~~~

In the "Vertical Drop Parameters" group of the "Artificial Diffusion
(Flow Calc.) and Drop Parameters" calculation condition tab, you set
whether to consider energy loss at an abrupt bed drop (such as a
grade-control structure or weir).

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Vertical drop energy loss (j_drop)
     - Whether to enable the energy loss calculation at a drop
   * - Drop energy loss coefficient (alpha_drop)
     - A coefficient for the amount of energy loss
   * - Drop energy loss power exponent (m_drop)
     - An exponent for the amount of energy loss

Location and shape of the drop structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The location, height, and affected range of the drop structure itself are
set individually in the boundary condition screen by selecting grid edges
(in the i-direction or j-direction).

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Height difference of the drop structure (VdropHeight_i/j)
     - The height of the drop (m)
   * - Affected length of the drop structure (VdropLength_i/j)
     - The length (m) over which the drop's influence extends

Culverts, gates and pumps (coupled structures)
---------------------------------------------------

The common idea
~~~~~~~~~~~~~~~~~~~

Box culverts (BoxCulvert), floodgates (Gate) and drainage pumps (Pump)
connect two separate points in the computational domain (an inlet cell and
an outlet cell) through a discharge carried by the structure, independent
of the surface flow. In the boundary condition screen, you designate the
inlet and outlet cells and assign them the same "Coupling code number" to
pair them together.

The common discharge formula for culverts and gates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For both culverts (``bc_``) and gates (``gt_``), the following parameters
are set on the inlet cell (they are not needed on the outlet cell).

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Width (m) / Height (m)
     - The width and height of the opening
   * - Elevation (m)
     - The invert (sill) elevation of the structure
   * - Multiply
     - A multiplier applied to the computed discharge
   * - Extended formula
     - Whether to use the extended formula that accounts for the degree of
       submergence
   * - Coefficient of submerged flow / subsurface flow / free flow
     - The discharge coefficients for submerged flow, orifice
       (sub-surface) flow, and free flow, respectively

Gates additionally have settings for the open/close operation.

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Open/Close operation (gt_method)
     - How the open/close state is determined: automatic (based on water
       level) / set with a time series
   * - Open/Close operation time series (gt_openclose)
     - The time series of the open/close operation (when "Set data" is
       chosen)
   * - Outside water level (gt_outwl)
     - Whether to set an outside (downstream) water level (set on the
       outlet cell)
   * - Water level time series (wl1)
     - The time series of the outside water level (m)

Pumps
~~~~~~~~

A pump forcibly drains water from the inside (Inlet) to the outside
(Outlet).

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Auto/Set data (p_method)
     - How the drainage rate is determined: automatic (operates between a
       start and stop water level) / set with a time series
   * - Maximum drainage discharge (p_qmax)
     - The maximum drainage discharge (m3/s) under automatic operation
   * - Begin operating water level (p_startope)
     - The inside water level (m) at which operation begins
   * - Stop operating water level (p_stopope)
     - The inside water level (m) at which operation stops
   * - Drainage discharge time series (qt2)
     - The time series of the drainage discharge (m3/s) (when "Set data"
       is chosen, or set on the outlet cell)
