物質輸送（染料拡散・GELATO）
================================

流れ場・河床変動の計算とは独立に，水中に投入した物質（染料など）や，流れに乗って
移動する粒子（漂流物・浮遊砂の粒子追跡など）を扱う2つの機能があります．

染料の移流拡散計算
----------------------

計算条件「Dye Advection and Diffusion」タブで，特定の地点から投入した染料（トレーサー）
が，計算された流れ場に乗って移流・拡散する様子を計算できます．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Diffusion and transportation of dye (j_dye)
     - 染料の移流拡散計算を有効にするかどうか
   * - Start time of dye injection (start_dye)
     - 投入開始時刻(秒)
   * - End time of dye injection (end_dye)
     - 投入終了時刻(秒)
   * - Concentration injecting dye (dye_in)
     - 投入する染料の濃度
   * - Diffusion coefficient multiplying factor (coef_dye)
     - 拡散係数に乗じる倍率

投入する地点はGridConditionの「染料注入セル」として格子上で指定します．

GELATO（粒子追跡モデル）
----------------------------

GELATO（General Lagrangian Tracer Tracking）は，流れに乗って移動する粒子
（トレーサー）の軌跡を，オイラー型の流れ計算とは別にラグランジュ的に追跡する
モデルです．漂流物や浮遊砂粒子の移動経路の可視化などに使えます．

基本設定
~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Gelato Activate (j_gelato)
     - GELATO計算を有効にするかどうか
   * - Velocity using for Gelato (j_gelVel)
     - 粒子の移動に使う流速：水深平均流速／水表面流速／底面近傍流速
   * - Maximum Tracer Numbers (max_tNumber)
     - 追跡する粒子の最大数

粒子の挙動
~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Minimum depth below which tracer stops (hminTrace)
     - この水深を下回ると粒子の移動を停止する閾値(m)
   * - coefficient for sediment suspension (alpha_uswf)
     - 浮遊砂粒子としての巻き上がりやすさの係数
   * - How to specify the fall velocity (j_wf)
     - 沈降速度の与え方：Rubey式による／直接入力
   * - Diameter for Rubey formula (d_Rubey)
     - Rubey式に用いる粒径(m)
   * - Fall velocity for Gelato (wf_Gelato)
     - 直接指定する沈降速度(m/s)
   * - A value in D=A Nu + B / B value (a_diff, b_diff)
     - 拡散係数を渦動粘性係数 :math:`\nu_t` の一次式 :math:`D = A\nu_t + B` で
       与えるための係数
   * - Time step for Gelato (ddt)
     - 粒子追跡計算の時間刻み

粒子の投入条件
~~~~~~~~~~~~~~~~~

「General Lagrangian Tracer Tracking(2)」タブで，粒子を投入する時刻の範囲
（開始・終了・刻み）と，投入位置を無次元の格子座標（Xi：流下方向，Eta：横断方向）
の範囲として指定します．

関連機能：植生ブロック追跡
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

「Vegetation Block Tracking」タブでは，倒伏・流失した植生のかたまり（流木状の塊）を
GELATOと同様の考え方で追跡する機能が提供されています．植生モデル（
:doc:`07_VegetationAndBankCollapse` ）と合わせて使うことで，流失した樹木が
下流のどこへ流れ着くかを追跡できます．
