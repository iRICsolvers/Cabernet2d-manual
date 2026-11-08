Quasi-3D Flow Calculation Method
===================================

Why quasi-3D calculation is needed
--------------------------------------

Cabernet2D's governing equations are depth-averaged 2D shallow-water
equations that assume a uniform velocity profile over the water depth. In
real flows, however, there are strongly three-dimensional structures that
vary significantly over depth, such as the helical secondary flow in
meandering channels (where the near-bed flow turns toward the inner bank)
and the horseshoe vortex around obstacles such as bridge piers and spur
dikes. These structures make the near-bed flow direction and magnitude
different from the depth-averaged velocity, and they govern local scour and
deposition patterns.

The quasi-3D flow calculation method is a simplified way of evaluating this
kind of depth-wise flow structure in order to correct the **near-bed
velocity**, which directly determines the direction and magnitude of
bedload sediment transport. Three methods are available in the GUI
calculation condition "Quasi-3D calculation method (j_q3d)."

The three options in the GUI
--------------------------------

.. list-table::
   :header-rows: 1
   :widths: 10 30 60

   * - GUI label
     - Name
     - Overview
   * - (0)
     - Engelund equilibrium secondary flow
     - Directly computes the near-bed transverse velocity from the
       streamline curvature.
   * - (1)
     - Nays2DH :math:`A_n` transport equation
     - Evolves the secondary flow intensity :math:`A_n` through a transport
       equation, representing the delay in development and decay at bend
       entrances and exits.
   * - (2)
     - BVC + dynamic pressure correction (Uchida & Fukuoka, 2012)
     - Directly estimates the near-bed velocity vector from the transport
       equation of horizontal vorticity, and adds dispersion-stress and
       non-hydrostatic bottom-pressure correction terms to the
       depth-averaged momentum equations.

.. note::

   Method (2) BVC is very effective for local scour calculations where the
   flow changes abruptly over a short distance, such as around bridge
   piers and impermeable spur dikes. For straight channels or gently
   meandering channels, however, the simpler methods (0) Engelund and
   (1) Nays2DH may reproduce the observed bed variation just as well or
   better. Before adopting (2) as your final result, we recommend
   comparing it against (0)/(1) and choosing the method that best matches
   your site conditions and objectives.

(0) Engelund equilibrium secondary flow
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The secondary flow intensity is computed directly as an equilibrium value
from the local streamline curvature, water depth and velocity
(Engelund, 1974).

.. math::
   A_n = V \cdot h \cdot \frac{1}{r_s}

.. math::
   u_{n,\mathrm{bed}} = \beta_g \cdot N^* \cdot V \cdot \frac{h}{r_s}

where :math:`V` is the depth-averaged velocity, :math:`h` is the water
depth, :math:`r_s` is the radius of curvature of the streamline,
:math:`\beta_g` is a coefficient of the bedload transport formula, and
:math:`N^*` is the secondary flow intensity coefficient.

:math:`N^*` is set with the GUI parameter "Secondary flow intensity
coefficient N\* (snst)" (default 7.0, the theoretical value from
Engelund). This parameter is only active when this method is selected; for
the other methods it stays fixed at its default and is not shown.

Because the calculation is instantaneous (an equilibrium assumption), this
is the fastest and most stable method, but it cannot represent the delayed
development of secondary flow at a bend entrance.

(1) Nays2DH :math:`A_n` transport equation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This method evolves the secondary flow intensity :math:`A_n` in space and
time via a transport equation, removing the equilibrium assumption
(Johannesson & Parker, 1989; Hosoda et al., 2000; Iwasaki, Shimizu &
Kimura, 2013).

.. math::
   \lambda_v \frac{\partial(A_n/J)}{\partial t}
   + \nabla \cdot \left[\boldsymbol{u}_{\mathrm{surf}} \cdot \frac{u_{n,\mathrm{surf}}}{J}\right]
   - \nabla \cdot \left[\boldsymbol{u}_{\mathrm{bed}} \cdot \frac{u_{n,\mathrm{bed}}}{J}\right]
   = \frac{1}{J}\frac{u_{s,\mathrm{surf}}^2 - u_{s,\mathrm{bed}}^2}{r_s}
   + \frac{A_n}{J}\cdot\frac{V(\chi^2 + \frac{7}{12}\chi + \frac{1}{12})}{h\,\chi_1^3}

:math:`J` is the Jacobian of the computational grid, :math:`\lambda_v` is a
time-scale coefficient, :math:`\chi,\,\chi_1` are Engelund parameters, and
the subscripts surf and bed denote values near the water surface and near
the bed, respectively.

This method can reproduce the delayed development and decay of secondary
flow at the entrance and exit of a bend, making it suitable for meandering
channels. It also feeds the dispersion stress back into the depth-averaged
momentum equations directly: this stress arises from depth-integrating the
3D velocity profile (increased bed shear on the outer bank due to helical
flow).

(2) BVC + dynamic pressure correction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The general bottom-velocity analysis method (Uchida & Fukuoka, 2011, 2012)
directly estimates the near-bed velocity vector from the depth integral of
the surface velocity and horizontal vorticity.

.. math::
   u_{b,x} = u_{s,x} - \Omega_y \cdot h - \frac{\partial W_h}{\partial x}
             - w_s\frac{\partial z_s}{\partial x}, \qquad
   u_{b,y} = u_{s,y} + \Omega_x \cdot h - \frac{\partial W_h}{\partial y}
             - w_s\frac{\partial z_s}{\partial y}

:math:`\Omega_i` is the depth integral of horizontal vorticity, :math:`W_h`
is the depth integral of vertical velocity, :math:`w_s` is the vertical
velocity at the water surface, and :math:`z_s` is the water surface
elevation. Through the rise and "blow-up" of the water surface on the
upstream face of an obstacle, the reversal of near-bed velocity associated
with a horseshoe vortex emerges naturally. The shallow-water approximation
omits this effect, so it cannot reproduce the correct near-bed velocity
pattern upstream of an obstacle.

In method (2), the near-bed velocity estimate above is always combined
with two additional correction terms that are built into the
depth-averaged momentum equations (in the GUI these are offered as a
single option, and operate internally with fixed default settings):

- **Dispersion tensor**: evaluates the additional momentum transport that
  arises from depth-integrating the 3D velocity profile (an effect of
  helical flow in meandering channels and horseshoe vortices around
  obstacles), computed from the difference between the BVC surface and
  bottom velocities, and adds it as an extra force in the momentum
  equations.
- **Non-hydrostatic bottom pressure correction**: adds the non-hydrostatic
  bottom pressure deviation, obtained by integrating the quasi-steady
  vertical momentum equation, to the pressure gradient term of the
  depth-averaged momentum equations.

This method is especially powerful in situations such as local scour
around bridge piers and spur dikes, where the flow changes abruptly over a
short distance. On the other hand, it has the highest computational cost
of the three methods, and in regions with sharp curvature changes,
internal numerical stabilization (an upper clamp on the vorticity, and
exclusion of evaluation in cells adjacent to obstacles) is applied.

Optional output of the 3D velocity profile
-----------------------------------------------

Whichever method you choose, the "3D Velocity Profile" group in the GUI
lets you output the vertical velocity profile. This is purely a
visualization option and does not affect the flow, sediment transport or
bed variation calculations themselves.

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Parameter
     - Description
   * - 3D velocity computation (j_3d)
     - Whether to compute the vertical velocity profile. When method (2)
       BVC is selected, this is always computed regardless of this
       checkbox.
   * - Number of vertical layers (nz)
     - The number of vertical subdivisions (default 10).
   * - Vertical velocity calculation (j_3dv)
     - Whether to compute the vertical velocity component by integrating
       the 3D continuity equation.

Methods (0) and (1) use the Engelund (1974) polynomial profile
(second-order in the streamwise direction, sixth-order for the secondary
flow direction); method (2) uses the BVC third-order polynomial profile.

Guidance for choosing a method
------------------------------------

- If you want a fast, stable computation, or only need a simple estimate
  of transverse sediment transport → **(0) Engelund**
- If you want to reproduce the delayed development of secondary flow at
  the entrance and exit of bends in a meandering channel →
  **(1) Nays2DH**
- If you want to accurately reproduce local scour around a localized
  obstacle such as a bridge pier or spur dike → **(2) BVC + dynamic
  pressure correction** (but for straight or gently meandering channels,
  (0)/(1) may give better results, so always compare)

References
-------------

- Engelund, F. (1974): Flow and bed topography in channel bends. *J. Hydraul. Div.*, 100(11), 1631-1648.
- Johannesson, H. & Parker, G. (1989): Secondary flow in mildly sinuous channel. *J. Hydraul. Eng.*, 115(3), 289-308.
- Hosoda, T., Nagata, N., Iwata, M. & Kimura, I. (2000): A depth averaged model of open channel flows with lag between main flow and secondary flow in a generalized curvilinear coordinate system. *J. Hydraul. Eng. JSCE*, 44, 587-592.
- Iwasaki, T., Shimizu, Y. & Kimura, I. (2013): Effects of a secondary flow model on bed variation in a mildly meandering channel. *J. JSCE, Ser. B1 (Hydraulic Engineering)*, 69(3), 147-163.
- Uchida, T. & Fukuoka, S. (2011): A new depth-averaged quasi-3D bed variation calculation method based on a general bottom velocity analysis method. *J. JSCE, Ser. B1 (Hydraulic Engineering)*, 67(1), 16-29.
- Uchida, T. & Fukuoka, S. (2012): A quasi-3D bed variation calculation method considering non-hydrostatic bottom pressure. *Annual Journal of Hydraulic Engineering, JSCE*, 56, I_1225-I_1230.
