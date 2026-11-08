計算設定（人工粘性・ホットスタート/OpenMP）
================================================

流れ計算の人工粘性
----------------------

計算条件「Artificial Diffusion (Flow Calc.) and Drop Parameters」タブの
「Artificial Viscosity for Water Surface / Flow Calculation」グループで，
水面・流れの計算を安定化させるための人工粘性を設定します．これは河床変動計算の
人工粘性（:doc:`07_VegetationAndBankCollapse` の法面崩落の節，および掃流砂計算の
人工粘性 art_visc_coef）とは別のものです．

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Water surface (j_adiff)
     - 水面計算の人工粘性を有効にするかどうか
   * - Type of artificial viscosity (j_hdiffType)
     - 粘性係数の与え方：一定値／最大流速と格子サイズの関数
   * - Viscosity coefficient (hdiff)
     - 粘性係数の値（一定値を選んだ場合）

側壁・障害物の摩擦
~~~~~~~~~~~~~~~~~~~~~

同じタブの「Side-Wall / Obstacle Friction」グループで，側壁・障害物表面の摩擦係数
（cw）を設定します．値を大きくすると，壁面付近の流速がより強く減衰します．

ホットスタート（リスタート計算）
------------------------------------

計算条件「Hot Start / OpenMP」タブで，計算の途中経過を一時ファイルに保存し，
そこから計算を再開する機能を設定します．長時間の計算を分割して実行したい場合や，
計算が何らかの理由で中断した後に続きから再開したい場合に使います．

一時ファイルの出力
~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Output temporary files (write_flag)
     - 一時ファイルを出力するかどうか
   * - Temporary File Path (tmp_pass)
     - 一時ファイルの保存先パス
   * - Number of temporary files (n_tempfile)
     - 保存する一時ファイルの世代数（1〜10）。指定した世代数を使い回して
       上書き保存します．
   * - Time unit of temporary output (i_tmp_out_unit)
     - 出力時刻の単位（秒／時／日／月／年）
   * - Output time of temp file 0〜4 (outtime_tmp0〜4)
     - 各世代の一時ファイルを出力する時刻

計算の再開
~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - パラメータ
     - 説明
   * - Calculate from initial or temporary file (read_flag)
     - 計算の開始方法：初期状態から（Initial）／一時ファイルから再開（Restart）
   * - Input Temporary File Name (tmp_readfile)
     - 再開に使う一時ファイル（read_flagがRestartの場合に指定）

.. note::

   リスタートで再開した計算は，保存時点の流れ場・河床・植生などの状態を
   引き継ぎますが，計算条件（境界条件や各種パラメータ）はそのとき開いている
   プロジェクトの設定が使われます．条件を変更してから再開することも可能です．

並列計算（OpenMP）
----------------------

同じタブの「Number of threads for parallel computation (n_parallel)」で，
OpenMPによる並列計算に使用するスレッド数を指定します．計算機のCPUコア数に応じて
設定することで，計算時間を短縮できます．
