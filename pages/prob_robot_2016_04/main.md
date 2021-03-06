# 確率ロボティクス2016第4回
<h1 style="font-size: 250%;">確率ロボティクス</h1>
<h2>第4回</h2>
上田 隆一

2016年10月10日\@千葉工業大学

<!--nextpage-->
<h2>前回・前々回のおさらいと今回</h2>
<ul>
 	<li>前々回
<ul>
 	<li>制御出力（移動）に伴う雑音の扱い</li>
 	<li>信念に反映させる方法</li>
</ul>
</li>
 	<li> 前回
<ul>
 	<li>センサ入力に乗る雑音の扱い</li>
 	<li>信念に反映させる方法</li>
</ul>
</li>
 	<li>今回
<ul>
 	<li> 制御とセンサ計測を繰り返していくと信念もその都度更新されなければならない
<ul>
 	<li><span style="color: #ff0000;">ベイズフィルタ</span></li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>ベイズフィルタ（の前に）</h2>
<ul>
 	<li>前々回の制御出力の式と前回のセンサ入力の式を並べて記号を整理
<ul>
 	<li>以下のように定義しましょう
<ul>
 	<li>制御出力[latex]\\boldsymbol{u}_t [/latex]後の信念:
<ul>
 	<li>[latex]\\hat{bel}_t(\\boldsymbol{x}) = bel(\\boldsymbol{x} |\\boldsymbol{u}_{1:t},\\boldsymbol{z}_{1:t-1},bel_0)[/latex]</li>
</ul>
</li>
 	<li>センサ入力[latex]\\boldsymbol{z}_t[/latex]後の信念:
<ul>
 	<li>[latex]bel_t(\\boldsymbol{x}) = bel(\\boldsymbol{x} |\\boldsymbol{u}_{1:t},\\boldsymbol{z}_{1:t},bel_0)[/latex]</li>
</ul>
</li>
 	<li>ここで
<ul>
 	<li>[latex]bel_0[/latex]: 最初にエージェントが持つ信念</li>
 	<li>[latex]\\boldsymbol{u}_{1:t}[/latex]: 時刻[latex]1[/latex]から[latex]t[/latex]までの制御出力のシーケンス</li>
 	<li>[latex]\\boldsymbol{z}_{1:t}[/latex]: 時刻[latex]1[/latex]から[latex]t[/latex]までのセンサ入力のシーケンス</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>ベイズフィルタ</h2>
<ul>
 	<li>制御出力後の変更（motion update）
<ul>
 	<li><span style="color: #ff0000;">[latex]\\hat{bel}_t(\\boldsymbol{x}) = \\int_\\mathcal{X} p(\\boldsymbol{x} | \\boldsymbol{x}',\\boldsymbol{u}_t )bel_{t-1}(\\boldsymbol{x}') d\\boldsymbol{x}'[/latex]</span>
<ul>
 	<li>式の意味: 状態が動いた後の信念は、その動きの予測の密度関数に、もとの信念の密度関数をかけて積分したもの</li>
</ul>
</li>
</ul>
</li>
 	<li>センサ入力後の更新（sensor update）
<ul>
 	<li><span style="color: #ff0000;">[latex]bel_t(\\boldsymbol{x}) = \\eta \\ell(\\boldsymbol{x}|\\boldsymbol{z}_t)\\hat{bel}_t(\\boldsymbol{x})[/latex]</span>
<ul>
 	<li>式の意味: センサから情報が入った後の信念は、そのセンサ値が分かったときの尤度関数と、もとの信念の密度関数をベイズの定理でかけたもの</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>拡張カルマンフィルタ</h2>
<ul>
 	<li>ベイズフィルタをガウス分布に限定したもの
<ul>
 	<li>これも前回、前々回の式をまとめると構成できる</li>
</ul>
</li>
 	<li>制御出力後の変更（motion update）
<ul>
 	<li><span style="color: #ff0000;">移動後の[latex]\\hat{bel}_t[/latex]</span>:
<ul>
 	<li><span style="color: #ff0000;">中心: [latex]\\hat{\\boldsymbol{x}}_t = f(\\boldsymbol{\\bar{x}}_{t-1},\\boldsymbol{u}_t)[/latex]</span>
<ul>
 	<li>雑音を考慮しない状態方程式で出力前の推定の中心を移動させたもの</li>
 	<li>[latex]\\bar{x}_{t-1}[/latex]: [latex]bel_{t-1}[/latex]の中心</li>
</ul>
</li>
 	<li><span style="color: #ff0000;">共分散: [latex]\\hat\\Sigma_t = F_t\\bar\\Sigma_{t-1}F_t^T + R_t[/latex]</span>
<ul>
 	<li>[latex]\\bar\\Sigma_{t-1}[/latex]: [latex]bel_{t-1}[/latex]の共分散</li>
 	<li>[latex]F_t[/latex]:[latex]\\bar\\Sigma_{t-1}[/latex]まわりで状態遷移関数[latex]f[/latex]から作ったヤコビ行列</li>
 	<li>[latex]R_t[/latex]: 移動の雑音の共分散行列（事前に計測しておく）</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<ul>
 	<li>センサ入力後の更新（sensor update）
<ul>
 	<li>センサ入力後の[latex]bel_t(\\boldsymbol{x})[/latex]:
<ul>
 	<li><span style="color: #ff0000;">中心: [latex]\\bar{\\boldsymbol{x}}_t = \\boldsymbol{\\hat{x}}_t + K(\\boldsymbol{z}_t - h(\\boldsymbol{\\hat{x}}_t)) [/latex]</span>
<ul>
 	<li> [latex]h(\\boldsymbol{x})[/latex]: [latex]\\boldsymbol{x}[/latex]で得られる観測値</li>
 	<li>[latex]K = \\hat\\Sigma_t H_t (H_t \\bar\\Sigma_t H_t^T + Q_t )^{-1}[/latex]（カルマンゲイン）
<ul>
 	<li>[latex]H_t[/latex]: [latex]h[/latex]を[latex]\\boldsymbol{\\hat{x}}_t[/latex]まわりで偏微分して得られるヤコビ行列</li>
</ul>
</li>
 	<li>意味: 新しい分布の中心（推定状態）は、もとの推定状態に、実際のセンサ入力ともとの推定状態で得られるはずのセンサ入力の差にカルマンゲインをかけた分だけ足したものとなる</li>
</ul>
</li>
 	<li><span style="color: #ff0000;">共分散行列: [latex]\\Sigma_t = (I - KH_t) \\hat\\Sigma_t[/latex]</span>
<ul>
 	<li>新たな推定の共分散行列は、カルマンゲインにヤコビ行列をかけた分の割合だけ小さくなる</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>ガウス分布に従わないときは？</h2>
<ul>
 	<li>実際を表し、かつ計算ができる分布を頑張って見つける
<ul>
 	<li>機械学習でよく行われる（共役事前分布）
<ul>
 	<li>ロボットの動きに関しては難しい場合が多い</li>
</ul>
</li>
</ul>
</li>
 	<li><span style="color: #ff0000;">数値計算</span>
<ul>
 	<li>第２回に触れました
<ul>
 	<li>モンテカルロ法</li>
 	<li>格子を使う方法</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>モンテカルロ法による[latex]bel[/latex]の計算</h2>
<ul>
 	<li>発想: ロボットのシミュレーションをロボットの中で、一挙にたくさん並列で行う</li>
 	<li> 状態遷移のシミュレーション
<ul>
 	<li>一つ時刻0の状態[latex]\\boldsymbol{x}_0[/latex]を選んで、制御出力に合わせて移動
<ul>
 	<li>誤差を混入</li>
</ul>
</li>
 	<li>一つのシミュレーションの状態を、[latex]bel[/latex]からサンプリングされる標本（サンプル）とみなすことができる
<ul>
 	<li>「粒子（パーティクル）」という言い方も</li>
</ul>
</li>
</ul>
</li>
 	<li>センサ入力の評価
<ul>
 	<li>各パーティクルの姿勢とセンサ入力の妥当性をベイズの定理で評価</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>パーティクルの定義</h2>
<ul>
 	<li>[latex]\\Xi = \\{\\xi^{(i)} = (\\boldsymbol{x}^{(i)}, w^{(i)}) | i = 1,2,\\dots,N \\}[/latex]</li>
 	<li>パーティクルは次のように[latex]bel[/latex]を近似しなければならない
<ul>
 	<li><span style="color: #ff0000;">[latex]Bel(X) = \\int_{\\boldsymbol{x} \\in X} bel(\\boldsymbol{x}) d\\boldsymbol{x} \\approx \\sum_{i=1}^N \\delta(\\boldsymbol{x}^{(i)} \\in X) w^{(i)}[/latex]</span>
<ul>
 	<li>[latex]Bel(X)[/latex]: [latex]X[/latex]の中に真の状態が存在する確率
<ul>
 	<li>密度関数[latel]bel[/latex]を積分すると確率になる</li>
</ul>
</li>
 	<li>[latex]\\forall X \\subset \\mathcal{X}[/latex]</li>
 	<li>[latex]\\delta[/latex]: カッコの中が真なら1、そうでなければ0</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>motion update</h2>
<ul>
 	<li>各パーティクルを[latex]p(\\boldsymbol{x} | \\boldsymbol{x}_{t-1}, \\boldsymbol{u}_t)[/latex]に従って動かす
<ul>
 	<li><span style="color: #ff0000;">[latex]\\boldsymbol{x}^{(i)}_t \\sim p(\\boldsymbol{x} | \\boldsymbol{x}_{t-1}, \\boldsymbol{u}_t) \\qquad (i=1,2,\\dots,N)[/latex]</span>
<ul>
 	<li>時刻[latex]t[/latex]における[latex]i[/latex]番目のパーティクルの状態を、状態遷移の確率分布にしたがって一つランダムに選ぶ</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>sensor update</h2>
<ul>
 	<li>各パーティクルの重みをベイズの定理で変える
<ul>
 	<li><span style="color: #ff0000;">[latex]w^{(i)}_t \\quad  \\texttt{*=} \\quad \\ell(\\boldsymbol{x}^{(i)}_t | \\boldsymbol{z}_t)  \\qquad (i=1,2,\\dots,N)[/latex]</span>
<ul>
 	<li>もとの重みに尤度をかける</li>
</ul>
</li>
</ul>
</li>
 	<li>重みの合計を1に正規化
<ul>
 	<li>[latex]\\eta = \\sum_{i=1}^N w^{(i)}_t [/latex]</li>
 	<li>[latex]w^{(i)}_t \\quad \\texttt{/=} \\quad \\eta  \\qquad (i=1,2,\\dots,N)[/latex]</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>その他の処理</h2>
<ul>
 	<li>パーティクルで[latex]bel[/latex]を近似しようとすると、いろいろ計算上の問題が出る
<ul>
 	<li>特定のパーティクルだけ重みが1に近づいて他が0になると近似能力を喪失
<ul>
 	<li><span style="color: #ff0000;">[latex]\\rightarrow[/latex]リサンプリング</span></li>
</ul>
</li>
 	<li>パーティクルの分布がずれて（外から見ていると）真の状態付近に戻ってこない
<ul>
 	<li><span style="color: #ff0000;">[latex]\\rightarrow[/latex]リセット</span></li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>リサンプリング</h2>
<ul>
 	<li>パーティクルの重みをならす処理
<ul>
 	<li>直感的な理解はこれでOK
<ul>
 	<li>重みの大きいパーティクルを複数のパーティクルに</li>
 	<li>重みの小さいパーティクルは消す</li>
</ul>
</li>
 	<li>ただし、統計的になるべく正しく、なるべく速く</li>
</ul>
</li>
 	<li>方法
<ul>
 	<li><a href="http://www.slideshare.net/ryuichiueda/ss-54463338?ref=https://lab.ueda.asia/?page_id=180" target="_blank">2015年の第5回資料の6-10ページ</a></li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>リセット</h2>
<ul>
 	<li>[latex]bel[/latex]と[latex]\\ell(\\boldsymbol{x}|\\boldsymbol{z})[/latex]の分布がかけ離れすぎている</li>
 	<li><a href="http://www.slideshare.net/ryuichiueda/ss-54463338" target="_blank">2015年の第5回資料の12ページから</a>
<ul>
 	<li>ビデオのリンクが切れてます
<ul>
 	<li>こっちが正しいリンク: <a href="https://lab.ueda.asia/?page_id=258" target="_blank">https://lab.ueda.asia/?page_id=258</a>
<ul>
 	<li>ただしわかりにくい</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<h2>格子地図（離散状態）を用いる方法</h2>
<ul>
 	<li>状態空間[latex]\\mathcal{X}[/latex]を離散化
<ul>
 	<li>[latex]\\mathcal{S} = \\{s_i | i=1,2,\\dots,N \\}[/latex]
<ul>
 	<li>[latex]i[/latex]: ここでは時刻ではなく離散状態の番号</li>
 	<li>[latex]\\forall s \\in \\mathcal{S}[/latex]は[latex]\\mathcal{X}[/latex]の部分空間
<ul>
 	<li>[latex]\\bigcup_{i=1}^N s_i = \\mathcal{X}[/latex]</li>
 	<li>[latex]s_i \\cap s_j = \\phi \\qquad \\forall i,j \\in \\{1,2,\\dots,N\\}[/latex]</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2><!--nextpage--></h2>
<ul>
 	<li>制御出力後の変更（motion update）
<ul>
 	<li><span style="color: #ff0000;">[latex]\\hat{Bel}_t(s_i) = \\sum_{j=1}^N P(s_i | s_j,\\boldsymbol{u}_t )Bel_{t-1}(s_j) [/latex]</span></li>
</ul>
</li>
 	<li>センサ入力後の更新（sensor update）
<ul>
 	<li><span style="color: #ff0000;">[latex]Bel_t(s_i) = \\eta^{-1} L(s_i | \\boldsymbol{z}_t ) \\hat Bel_t(s_i) [/latex]</span>
<ul>
 	<li>where [latex]\\eta = \\sum_{j=1}^N L(s_j | \\boldsymbol{z}_t ) \\hat Bel_t(s_j) [/latex]</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2></h2>
&nbsp;
