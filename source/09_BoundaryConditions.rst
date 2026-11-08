境界条件の詳細（流入・流出・検査断面）
==========================================

計算格子の辺（edge）を選択して設定する境界条件について，流入側・流出側・流量検査断面
の設定項目を説明します．いずれもi方向・j方向で同じ構成です（以下ではi方向を例に説明）．

流入水位境界（Inflow water level boundary）
-----------------------------------------------

上流端の水位を指定する境界条件です．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Water Level Condition for i-direction (GaugeCondition_i)
     - (0) 一定値(m) ／ (1) 一定勾配 ／ (2) 水位の時系列(m)
   * - Inflow Direction(+-) (GaugeDirection_i)
     - 流入方向（i+方向／i-方向）
   * - Method for specifying the upstream velocity distribution (Riemann_i)
     - 上流端流速の与え方：速度を指定しない（ゼロとする）／Manning公式による／
       内部のRiemann不変量による
   * - Maximum Froude number at i-direction gauge boundary (GFrmax_i)
     - 境界で許容する最大Froude数
   * - Water surface level value at i-direction boundary (GaugeVal_i)
     - 一定水位値(m)（Water Level Conditionが(0)の場合）
   * - Time series of water level values (GaugeSeries_i)
     - 水位の時系列(m)（Water Level Conditionが(2)の場合）
   * - Slope for the upstream Manning's velocity (jMslopeCond_i)
     - Manning公式で使う勾配：一定値／局所水面勾配
   * - Water surface slope value (GaugeSlope_i)
     - 一定勾配値（Water Level Conditionが(1)の場合）

流入流量境界（Inflow discharge boundary）
-----------------------------------------------

上流端の流量を指定する境界条件です．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Inflow Direction(+-) (inDirection_i)
     - 流入方向（i+方向／i-方向）
   * - Use Riemann invariant condition for discharge input boundary (qRiemann_i)
     - 内部のRiemann不変量を用いて境界流速を整合的に決定するかどうか
   * - Slope value of the i-direction inflow (slopeIn_i)
     - 流入境界の勾配（等流水深の算定などに使用）
   * - Discharge time series in i-direction (qIn_i)
     - 流量の時系列(m3/s)
   * - Check critical Froude number (qFrCk_i)
     - 境界でのFroude数チェックを行うかどうか
   * - Critical Froude number (qDegFr_i)
     - チェックに使う限界Froude数
   * - Adjustment coefficient for equilibrium bedload transport rate (SedAdjIn_i)
     - 上流端の平衡掃流砂量に対する調整係数（1.0で平衡供給）
   * - Suspended sediment supply ratio in i-direction (SedAdjIn_qs_i)
     - 上流端の浮遊砂供給比率。複合河道網モードではこちらが計算条件の
       「Upstream suspended sediment supply ratio」に優先して使われます
       （:doc:`08_MultiChannelNetworks` 参照）．

流出水位境界（Outflow boundary）
------------------------------------

下流端の水位を指定する境界条件です．選択肢の詳細は :doc:`08_MultiChannelNetworks`
の「流出境界条件の種類」を参照してください．

流量検査断面（Discharge inspection section）
-------------------------------------------------

計算結果の確認用に，任意の断面を通過する流量を記録する機能です．流れの計算そのものには
影響しません．ポストウィンドウでの流量縦断図表示や，流量の時間変化の確認に使えます．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Discharge positive direction (Direction_i)
     - 流量を正とする方向（i+方向／i-方向）
