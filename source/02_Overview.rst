基礎式
====================

Cabernet2Dでは以下の2次元浅水流式を用います．

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

ただし, :math:`x, y` は互いに直交する平面座標軸, :math:`t` は時間,
:math:`u, v` は :math:`x, y` 方向の水深平均流速, :math:`h` は水深,
:math:`H` は水位, :math:`g` は重力加速度, :math:`\tau_x, \tau_y` は :math:`x, y` 方向の河床せん断力, 
:math:`\rho` は水の密度, :math:`\nu_t` は渦動粘性係数である． 

抵抗則にマニング則を用いると, 河床せん断力は下記で表される．

.. math::
   \frac{\tau_x}{\rho h}= \frac{gn^2}{h^{4/3}} u\sqrt{u^2+v^2}, \ \ \ 
   \frac{\tau_y}{\rho h}= \frac{gn^2}{h^{4/3}} v\sqrt{u^2+v^2}

ただし, :math:`n` はマニングの粗度係数.  渦動粘性係数は，ゼロ方程式モデルを採用し，下記で表す．

.. math::
   \nu_t = \frac{\kappa}{6} u_\ast h

ただし，:math:`u_\ast` は摩擦速度 

.. math::
   u_\ast=\sqrt{ghI_f}, \ \ \ I_f=\frac{n^2 (u^2+v^2)}{h^{4/3}}

ただし，:math:`I_f` は摩擦勾配である．

流砂，河床変動に関する基礎式はNays2dHのものと同様ですので，ここでの記載は省略します．

数値計算法
===========

計算はNays2dHと同様に上記基礎式を境界適合の2次元一般座標の方程式に変化し，構造格子型の格子上で
セルセンターに水深の計算点，格子の辺の流速の計算点と配置する
スタカード格子による差分法で行われます．タイムステップ毎に，
運動方程式は移流部分を非移流部分に分ける分離解法を
用い，移流部分はCIP法を，非移流部分は運動方程式と連立して :math:`u, v, h` が同時に満たされる
ように繰り返し計算を行います．

Cabernet2Dでは合流支川や分派河川も本川と一体で計算し，全体を１つの領域として計算します．
境界条件は個々の河川網における流入境界，流出境界においてGUI上でその位置および条件を指定するようになっています．

計算手順
==========

計算手順は下記の通りです．

#. 計算格子の作成
#. 流入・流出など境界条件の設定
#. 計算条件の設定
#. 計算の実施
#. 計算結果の表示

