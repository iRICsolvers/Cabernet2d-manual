構造物（落差工・カルバート・ゲート・ポンプ）
================================================

Cabernet2Dには，河道内の落差工のような地形的な段差を扱う機能と，カルバート・ゲート・
ポンプのように計算領域内の2点間を人為的に流量でつなぐ構造物を扱う機能があります．

落差工（Vertical Drop Structure）
----------------------------------

段差部でのエネルギー損失
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

計算条件「Artificial Diffusion (Flow Calc.) and Drop Parameters」タブの
「Vertical Drop Parameters」グループで，河床の急激な落差（床止工・堰など）における
エネルギー損失を考慮するかどうかを設定します．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Vertical drop energy loss (j_drop)
     - 落差部のエネルギー損失計算を有効にするかどうか
   * - Drop energy loss coefficient (alpha_drop)
     - エネルギー損失量の係数
   * - Drop energy loss power exponent (m_drop)
     - エネルギー損失量の指数

落差構造物の位置と形状
~~~~~~~~~~~~~~~~~~~~~~~~~~~

落差工そのものの位置・高さ・影響範囲は，境界条件画面で格子の辺（i方向／j方向）を
選択して個別に設定します．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Height difference of the drop structure (VdropHeight_i/j)
     - 落差の高さ(m)
   * - Affected length of the drop structure (VdropLength_i/j)
     - 落差の影響が及ぶ範囲の長さ(m)

カルバート・ゲート・ポンプ（連結構造物）
--------------------------------------------

共通の考え方
~~~~~~~~~~~~~~~

ボックスカルバート（BoxCulvert），樋門ゲート（Gate），排水ポンプ（Pump）は，
計算領域内の離れた2地点（流入側セルと流出側セルと）を，地表の流れとは別に，
構造物を通した流量でつなぐ機能です．ポストウィンドウの境界条件画面で，
流入側（Inlet）・流出側（Outlet）となるセルをそれぞれ指定し，同じ
「Coupling code number」（連結コード番号）を割り当てることで，両者をペアとして
関連付けます．

カルバート・ゲート共通の流量式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

カルバート（``bc_``）・ゲート（``gt_``）とも，流入側セル（Inlet）に以下のパラメータを
設定します（流出側セルでは不要です）．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Width (m) / Height (m)
     - 断面の幅・高さ
   * - Elevation (m)
     - 構造物の敷高
   * - Multiply
     - 計算流量に乗じる倍率
   * - Extended formula
     - 水没状態に応じた拡張式を使うかどうか
   * - Coefficient of submerged flow / subsurface flow / free flow
     - 水没流・潜り流・自由流それぞれの流量係数

ゲートには，さらに開閉操作に関する設定があります．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Open/Close operation (gt_method)
     - 開閉の決め方：自動（水位に応じて自動判定）／時系列で指定
   * - Open/Close operation time series (gt_openclose)
     - 開閉操作の時系列（Set dataを選んだ場合）
   * - Outside water level (gt_outwl)
     - 流出側の外水位を設定するかどうか（流出側セルで設定）
   * - Water level time series (wl1)
     - 外水位の時系列(m)

ポンプ
~~~~~~~~~

ポンプは，内水側（Inlet）から外水側（Outlet）へ強制的に排水するための構造物です．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Auto/Set data (p_method)
     - 排水量の決め方：自動（開始・停止水位で運転）／時系列で指定
   * - Maximum drainage discharge (p_qmax)
     - 自動運転時の最大排水量(m3/s)
   * - Begin operating water level (p_startope)
     - 運転を開始する内水位(m)
   * - Stop operating water level (p_stopope)
     - 運転を停止する内水位(m)
   * - Drainage discharge time series (qt2)
     - 排水量の時系列(m3/s)（Set dataを選んだ場合，または流出側セルで設定）
