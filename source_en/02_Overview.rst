Governing Equations
====================

Cabernet2D uses the following 2D shallow-water equations.

.. math::
   \frac{\partial h}{\partial t}+\frac{\partial (uh)}{\partial x}+
   \frac{\partial (vh)}{\partial y}=0

.. math::
 \frac{\partial u}{\partial t}+u \frac{\partial u}{\partial x}+
   v \frac{\partial u}{\partial y}=
   -g \frac{\partial H}{\partial x}
   -\frac{\tau_x}{\rho h}+
   \frac{\partial}{\partial x} (\nu_t \frac{\partial u}{\partial x})+
   \frac{\partial}{\partial y} (\nu_t \frac{\partial u}{\partial y})

.. math::
   \frac{\partial v}{\partial t}+u \frac{\partial v}{\partial x}+
   v \frac{\partial v}{\partial y}=
   -g \frac{\partial H}{\partial y}
   -\frac{\tau_y}{\rho h}+
   \frac{\partial}{\partial x} (\nu_t \frac{\partial v}{\partial x})+
   \frac{\partial}{\partial y} (\nu_t \frac{\partial v}{\partial y})

Here :math:`x, y` are the mutually orthogonal planar coordinate axes,
:math:`t` is time, :math:`u, v` are the depth-averaged velocity components
in the :math:`x, y` directions, :math:`h` is the water depth, :math:`H` is
the water surface elevation, :math:`g` is gravitational acceleration,
:math:`\tau_x, \tau_y` are the bed shear stresses in the :math:`x, y`
directions, :math:`\rho` is the density of water, and :math:`\nu_t` is the
eddy viscosity coefficient.

Using Manning's formula as the resistance law, the bed shear stress is
given by:

.. math::
   \frac{\tau_x}{\rho h}= \frac{gn^2}{h^{4/3}} u\sqrt{u^2+v^2}, \ \ \
   \frac{\tau_y}{\rho h}= \frac{gn^2}{h^{4/3}} v\sqrt{u^2+v^2}

where :math:`n` is Manning's roughness coefficient. The eddy viscosity
coefficient is evaluated with a zero-equation model:

.. math::
   \nu_t = \frac{\kappa}{6} u_\ast H

where :math:`u_\ast` is the friction velocity

.. math::
   u_\ast=\sqrt{ghI_f}, \ \ \ I_f=\frac{n^2 (u^2+v^2)}{h^{4/3}}

and :math:`I_f` is the friction slope.

The governing equations for sediment transport and bed variation are the
same as in Nays2DH and are omitted here.

Numerical Method
===================

As in Nays2DH, the governing equations above are transformed into
boundary-fitted 2D general coordinates and solved on a structured grid
with a staggered arrangement, in which water depth is computed at cell
centers and velocity at cell edges. At each time step, the momentum
equations are split into advection and non-advection parts: the advection
part is solved with the CIP method, and the non-advection part is solved
iteratively together with the momentum equations so that :math:`u, v, h`
are simultaneously satisfied.

Cabernet2D computes confluent tributaries and bifurcating branches together
with the main channel as a single integrated computational domain. For each
river network, the location and condition of inflow and outflow boundaries
are specified through the GUI.

Computation Procedure
==========================

The computation proceeds through the following steps.

#. Create the computational grid
#. Set boundary conditions such as inflow and outflow
#. Set the calculation conditions
#. Run the computation
#. Display the computation results
