Boundary Conditions in Detail (Inflow, Outflow, Inspection Sections)
==========================================================================

This chapter describes the inflow, outflow, and discharge inspection section
settings, which are configured by selecting an edge of the computational
grid. All of these have the same structure in the i-direction and the
j-direction (the i-direction is used as the example below).

Inflow water level boundary
-------------------------------

A boundary condition that prescribes the water level at the upstream end.

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Water Level Condition for i-direction (GaugeCondition_i)
     - (0) Constant value (m) / (1) Constant slope / (2) Time series of water level (m)
   * - Inflow Direction(+-) (GaugeDirection_i)
     - Inflow direction (i+ direction / i- direction)
   * - Method for specifying the upstream velocity distribution (Riemann_i)
     - How the upstream boundary velocity is given: do not prescribe it
       (set to zero) / using Manning's equation / using the internal
       Riemann invariant
   * - Maximum Froude number at i-direction gauge boundary (GFrmax_i)
     - The maximum Froude number allowed at the boundary
   * - Water surface level value at i-direction boundary (GaugeVal_i)
     - The constant water level value (m) (when the Water Level Condition
       is (0))
   * - Time series of water level values (GaugeSeries_i)
     - The time series of water level (m) (when the Water Level Condition
       is (2))
   * - Slope for the upstream Manning's velocity (jMslopeCond_i)
     - The slope used in Manning's equation: constant value / local water
       surface slope
   * - Water surface slope value (GaugeSlope_i)
     - The constant slope value (when the Water Level Condition is (1))

Inflow discharge boundary
-------------------------------

A boundary condition that prescribes the discharge at the upstream end.

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Inflow Direction(+-) (inDirection_i)
     - Inflow direction (i+ direction / i- direction)
   * - Use Riemann invariant condition for discharge input boundary (qRiemann_i)
     - Whether to determine the boundary velocity consistently using the
       internal Riemann invariant
   * - Slope value of the i-direction inflow (slopeIn_i)
     - The slope of the inflow boundary (used, for example, to compute the
       normal depth)
   * - Discharge time series in i-direction (qIn_i)
     - The discharge time series (m3/s)
   * - Check critical Froude number (qFrCk_i)
     - Whether to check the Froude number at the boundary
   * - Critical Froude number (qDegFr_i)
     - The critical Froude number used for the check
   * - Adjustment coefficient for equilibrium bedload transport rate (SedAdjIn_i)
     - An adjustment coefficient applied to the equilibrium bedload supply
       at the upstream end (1.0 gives equilibrium supply)
   * - Suspended sediment supply ratio in i-direction (SedAdjIn_qs_i)
     - The suspended sediment supply ratio at the upstream end. In
       multi-channel mode this value is used instead of the "Upstream
       suspended sediment supply ratio" in the calculation conditions
       (see :doc:`08_MultiChannelNetworks`).

Outflow boundary
--------------------

A boundary condition that prescribes the water level at the downstream
end. For the available options, see "Types of outflow boundary condition"
in :doc:`08_MultiChannelNetworks`.

Discharge inspection section
---------------------------------

This feature records the discharge passing through an arbitrary
cross-section, for checking the computation results. It does not affect
the flow computation itself. It can be used, for example, to display a
longitudinal discharge profile in the post-processing window, or to check
how the discharge changes over time.

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Parameter
     - Description
   * - Discharge positive direction (Direction_i)
     - The direction (i+ or i-) treated as a positive discharge
