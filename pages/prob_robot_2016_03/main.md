# 確率ロボティクス2016第3回
<h1 style="font-size: 250%;">確率ロボティクス</h1>
<h2>第3回</h2>
上田 隆一

2016年10月5日\@千葉工業大学

<!--nextpage-->
<h2>今日の内容</h2>
<ul>
 	<li>センサ値と状態、信念</li>
</ul>
<!--nextpage-->
<h2>前回</h2>
<ul>
 	<li>制御出力[latex]\\boldsymbol{u}_t[/latex]で状態[latex]\\boldsymbol{x}_{t-1}[/latex]から[latex]\\boldsymbol{x}_t[/latex]に変化</li>
 	<li>自律ロボット（エージェント）にとって、状態[latex]\\boldsymbol{x}_t[/latex]は、未知</li>
 	<li>エージェントは状態[latex]\\boldsymbol{x}_t[/latex]に対する認識である信念[latex]bel_t[/latex]を持つ</li>
 	<li>[latex]bel_t[/latex]には、制御出力に対する実際の動きの雑音が蓄積していく
<ul>
 	<li>ガウス分布に従う場合は共分散行列に雑音が足されていく</li>
</ul>
</li>
</ul>
<!--nextpage-->
<h2>状態を（間接的に）観測する</h2>
<ul>
 	<li>センサの値には状態に対するヒント（情報）が隠れている</li>
 	<li>センサ入力の定義
<ul>
 	<li>[latex]\\boldsymbol{z} = (z_1,z_2,\\dots,z_m) \\in \\mathcal{Z}[/latex]</li>
</ul>
</li>
 	<li>多くの場合、情報は間接的
<ul>
 	<li>レーザレンジファインダーは移動ロボットの
[latex]\\boldsymbol{x} = (x,y,\\theta)[/latex]を直接は教えてくれない
<ul>
 	<li>変数が違う（[latex]\\mathcal{X} \\neq \\mathcal{Z}[/latex]）</li>
 	<li>雑音もある</li>
</ul>
</li>
</ul>
</li>
</ul>
<!--nextpage-->
<h2>観測方程式</h2>
<ul>
 	<li>センサ入力と状態を結びつける式
<ul>
 	<li>現代制御に出てくる</li>
</ul>
</li>
 	<li>線形な場合
<ul>
 	<li>[latex]\\boldsymbol{z} = C\\boldsymbol{x} + \\delta[/latex]
<ul>
 	<li>時刻の添字[latex]t[/latex]は省略</li>
 	<li>[latex]\\delta[/latex]: センサ入力の値に混入する雑音</li>
</ul>
</li>
</ul>
</li>
 	<li>非線形な場合
<ul>
 	<li>[latex]\\boldsymbol{z} = h(\\boldsymbol{x}) + \\delta[/latex]</li>
</ul>
</li>
 	<li>前回の制御のときと同様、このような定式化をしてしまうと
観測にまつわる不確かさの表現力に乏しい</li>
</ul>
<!--nextpage-->
<h2>観測にまつわる不確かさの表現</h2>
<ul>
 	<li>[latex]p(\\boldsymbol{z}|\\boldsymbol{x})[/latex]: 状態[latex]\\boldsymbol{x}[/latex]にいた場合に、[latex]\\boldsymbol{z}[/latex]というセンサ入力を得る確率の密度</li>
 	<li><span style="color: #ffff00;">[latex]\\ell(\\boldsymbol{x}|\\boldsymbol{z})[/latex]（尤度）</span>:センサ入力[latex]\\boldsymbol{z}[/latex]を得た場合に、[latex]\\boldsymbol{x}[/latex]が真の状態でありそうな度合いを数値化したもの
<ul>
 	<li>[latex]p(\\boldsymbol{z}|\\boldsymbol{x})[/latex]と基本的には同じもので、因果をひっくり返したもの</li>
 	<li>ただし確率の性質を満たす必要はない</li>
 	<li>[latex]\\ell[/latex]を<span style="color: #ffff00;">尤度関数</span>と呼ぶ</li>
</ul>
</li>
 	<li>これをエージェントが知っていると、エージェントが状態を推定できる</li>
 	<li> どうやってこれを知るか？
<ul>
 	<li>事前実験</li>
 	<li>センサの特性や環境の特性の知識</li>
 	<li>正解はない</li>
</ul>
</li>
</ul>
<!--nextpage-->
<h2>センサ入力に生じる雑音に対する考察</h2>
<ul>
 	<li>ガウス分布状にノイズが乗るセンサの尤度
<ul>
 	<li><a href="http://www.slideshare.net/ryuichiueda/ss-53911082?ref=https://lab.ueda.asia/?page_id=180" target="_blank">昨年の講義資料の第三回</a>の11ページ</li>
</ul>
</li>
 	<li>動的な障害物とセンサの関係
<ul>
 	<li><a href="http://www.slideshare.net/ryuichiueda/ss-53911082?ref=https://lab.ueda.asia/?page_id=180" target="_blank">昨年の講義資料の第三回</a>の17-19ページ</li>
</ul>
</li>
</ul>
&nbsp;

<!--nextpage-->
<h2>センサ入力からの[latex]bel[/latex]の更新</h2>
<ul>
 	<li>センサ入力と尤度関数から<span style="color: #ffff00;">ベイズの定理を使って</span>[latex]bel[/latex]を更新</li>
 	<li>[latex]bel(\\boldsymbol{x}|\\boldsymbol{z}) = \\frac{p(\\boldsymbol{z}|\\boldsymbol{x})bel(\\boldsymbol{x})}{\\int_{\\mathcal{x}}p(\\boldsymbol{z}|\\boldsymbol{x}')bel(\\boldsymbol{x}')d\\boldsymbol{x}'} \\\\
= \\eta p(\\boldsymbol{z}|\\boldsymbol{x})bel(\\boldsymbol{x}) \\\\
= \\eta \\ell(\\boldsymbol{x}|\\boldsymbol{z})bel(\\boldsymbol{x})[/latex]</li>
 	<li>計算が終わったら[latex]bel(\\boldsymbol{x}|\\boldsymbol{z})[/latex]を[latex]bel(\\boldsymbol{x})[/latex]と表記
<ul>
 	<li>本来[latex]bel_t[/latex]は過去のロボットの制御出力、センサ入力全てから得られる条件つき確率になっている</li>
</ul>
</li>
</ul>
<!--nextpage-->
<h2>1次元、ガウス分布に雑音が従う場合の問題</h2>
<ul>
 	<li>今、[latex]bel[/latex]が、次の式で表されているとします。
<ul>
 	<li>[latex]bel(x) = \\frac{1}{\\sqrt{2\\pi \\sigma^2}}\\exp \\{-\\frac{(x-\\hat{x})^2}{2\\sigma^2}\\}[/latex]</li>
 	<li>[latex]\\sigma[/latex]: 標準偏差</li>
 	<li>[latex]\\hat{x}[/latex]: 推定の中心（推定値）</li>
</ul>
</li>
 	<li>センサ入力[latex]z[/latex]がありました。
<ul>
 	<li>[latex]z[/latex]の値は、[latex]x[/latex]をロボットの真の位置とするとき、対して次の分布に従います
<ul>
 	<li>[latex]p(z|x) = \\ell(x|z) = \\frac{1}{\\sqrt{2\\pi \\zeta^2}}\\exp \\{-\\frac{(z-x)^2}{2\\zeta^2}\\}[/latex]</li>
</ul>
</li>
</ul>
</li>
 	<li>さて[latex]bel[/latex]はどのように更新されるでしょうか？</li>
</ul>
<!--nextpage-->
<h2>計算</h2>
<ul>
 	<li>[latex]x[/latex]に関係ない項を[latex]\\eta[/latex]に放り込みながら整理
<ul>
 	<li>[latex]bel(x | z) = \\eta e^{-\\frac{(x-\\hat{x})^2}{2\\sigma^2}}e^{-\\frac{(z-x)^2}{2\\zeta^2}} \\\\
=\\eta e^{-\\frac{1}{2\\sigma^2}x^2 -\\frac{1}{2\\zeta^2}x^2 + \\frac{\\hat{x}}{\\sigma^2}x + \\frac{z}{\\zeta^2}x }  \\\\
= \\eta e^{-\\frac{\\sigma^2 + \\zeta^2}{2\\sigma^2\\zeta^2}\\left\\{ x^2 - 2(\\frac{\\zeta^2\\hat{x}}{\\sigma^2 + \\zeta^2} +\\frac{\\sigma^2 z}{\\sigma^2 + \\zeta^2})x \\right\\} } \\\\
= \\eta e^{-\\frac{\\sigma^2 + \\zeta^2}{2\\sigma^2\\zeta^2}\\left(x - \\frac{\\zeta^2\\hat{x} +\\sigma^2 z}{\\sigma^2 + \\zeta^2}  \\right)^2  }[/latex]</li>
</ul>
</li>
</ul>
<!--nextpage-->
<h2>結果</h2>
<ul>
 	<li>[latex]bel(x | z) [/latex]は、次のパラメータを持つガウス分布に
<ul>
 	<li>中心: [latex]\\frac{\\zeta^2\\hat{x} +\\sigma^2 z}{\\sigma^2 + \\zeta^2}[/latex]
<ul>
 	<li>元の分布の中心[latex]\\hat{x}[/latex]とセンサ入力の示す値[latex]z[/latex]の
<span style="color: #ffff00;">重み付き平均</span>に推定の中心が移動</li>
 	<li><span style="color: #ffff00;">[latex]\\zeta[/latex]が小さい（センサ入力に自信がある）と[latex]z[/latex]寄りに</span></li>
 	<li><span style="color: #ffff00;">[latex]\\sigma[/latex]が小さい（元の推定に自信がある）と[latex]\\hat{x}[/latex]寄りに</span></li>
</ul>
</li>
 	<li>分散: [latex]\\frac{\\sigma^2\\zeta^2}{\\sigma^2 + \\zeta^2}[/latex]
<ul>
 	<li>元の[latex]bel[/latex]の分散[latex]\\sigma^2[/latex]より[latex]\\frac{\\zeta^2}{\\sigma^2 + \\zeta^2}[/latex]倍だけ<span style="color: #ffff00;">小さくなる</span></li>
</ul>
</li>
</ul>
</li>
</ul>
<!--nextpage-->
<h2>非線形・雑音が多変量ガウス分布に従う場合の<span id="MathJax-Element-77-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-1514" class="math"><span id="MathJax-Span-1515" class="mrow"><span id="MathJax-Span-1516" class="mi">b</span><span id="MathJax-Span-1517" class="mi">e</span><span id="MathJax-Span-1518" class="mi">l</span></span></span></span>の導出</h2>
<ul>
 	<li>制御出力と同様に導出してみましょう。</li>
 	<li>非線形な観測方程式
<ul>
 	<li>[latex]\\boldsymbol{z} = h(\\boldsymbol{x}) + \\delta[/latex]</li>
 	<li>[latex]\\delta[/latex]は共分散行列[latex]Q[/latex]、中心ゼロの多変量ガウス分布に従うとする</li>
</ul>
</li>
 	<li>[latex]\\boldsymbol{\\hat{x}}[/latex]周りで線形化するとこうなる
<ul>
 	<li>[latex] h(\\boldsymbol{x}) = h(\\boldsymbol{\\hat{x}}) + \\frac{\\partial h(\\boldsymbol{x})}{\\partial\\boldsymbol{x}}\\big|_{\\boldsymbol{\\hat{x}}} (\\boldsymbol{x} - \\boldsymbol{\\hat{x}}) =h(\\boldsymbol{\\hat{x}}) + H (\\boldsymbol{x} - \\boldsymbol{\\hat{x}})[/latex]
<ul>
 	<li>[latex]H =\\frac{\\partial h(\\boldsymbol{x})}{\\partial\\boldsymbol{x}}\\big|_{\\boldsymbol{\\hat{x}}}[/latex]とする。</li>
 	<li>[latex]H[/latex]はヤコビ行列</li>
</ul>
</li>
</ul>
</li>
</ul>
<!--nextpage-->
<h2>尤度関数、[latex]bel[/latex]への代入</h2>
<ul>
 	<li>[latex]\\ell(\\boldsymbol{x} | \\boldsymbol{z}) = \\eta e^{-\\frac{1}{2} (\\boldsymbol{z} -h(\\boldsymbol{x}))^TQ^{-1}(\\boldsymbol{z} -h(\\boldsymbol{x}))} \\\\
=\\eta e^{-\\frac{1}{2} (\\boldsymbol{z} -h(\\boldsymbol{\\hat{x}}) - H(\\boldsymbol{x} - \\boldsymbol{\\hat{x}} ))^TQ^{-1}(\\boldsymbol{z} -h(\\boldsymbol{\\hat{x}}) - H(\\boldsymbol{x} - \\boldsymbol{\\hat{x}} )) }[/latex]</li>
 	<li>[latex]bel(\\boldsymbol{x}|\\boldsymbol{z}) = \\ell(\\boldsymbol{x} | \\boldsymbol{z})bel(\\boldsymbol{x}) \\\\
=\\eta e^{-\\frac{1}{2} (\\boldsymbol{x} - \\boldsymbol{\\hat{x}})^T\\Sigma^{-1}(\\boldsymbol{x} - \\boldsymbol{\\hat{x}})} e^{-\\frac{1}{2} (\\boldsymbol{z} -h(\\boldsymbol{\\hat{x}}) - H(\\boldsymbol{x} - \\boldsymbol{\\hat{x}} ))^TQ^{-1}(\\boldsymbol{z} -h(\\boldsymbol{\\hat{x}}) - H(\\boldsymbol{x} - \\boldsymbol{\\hat{x}} )) }[/latex]</li>
</ul>
&nbsp;

<!--nextpage-->
<h2>計算（大変）は割愛しますが・・・</h2>
<ul>
 	<li>[latex]bel(\\boldsymbol{x}|\\boldsymbol{z})[/latex]は次のパラメータを持つ
多変量ガウス分布に
<ul>
 	<li>分布の中心: [latex] \\boldsymbol{\\hat{x}} + K(\\boldsymbol{z} - h(\\boldsymbol{\\hat{x}})) [/latex]</li>
 	<li>共分散行列: [latex](I - KH) \\Sigma[/latex]</li>
 	<li>ここで
[latex]K = \\Sigma H (H \\Sigma H^T + Q )^{-1}[/latex]
<span style="color: #ffff00;">（確率ロボティクスの式(3.64)、間違ってます！！！！）</span></li>
</ul>
</li>
</ul>
<!--nextpage-->
<h2>カルマンゲイン[latex]K[/latex]</h2>
<ul>
 	<li>以下を表す
<ul>
 	<li>センサ入力でどれだけ状態推定の曖昧さを減らせるか</li>
 	<li>これまでの推定の状態を、センサ入力の教える状態にどれだけ近付けるか</li>
</ul>
</li>
 	<li>[latex]K = \\Sigma H (H \\Sigma H^T + Q )^{-1}[/latex]</li>
 	<li>先ほどの1次元の問題では、[latex]\\Sigma[/latex]が[latex]\\sigma^2[/latex]、[latex]Q[/latex]が[latex]\\zeta^2[/latex]、[latex]H[/latex]が単位行列に
<ul>
 	<li>整理すると[latex]K = \\frac{\\sigma^2}{\\sigma^2 + \\zeta^2}[/latex]</li>
 	<li><span style="color: #ffff00;">[latex]I - KH =\\frac{\\zeta^2}{\\sigma^2 + \\zeta^2}[/latex]</span></li>
</ul>
</li>
</ul>
<!--nextpage-->
<h2>次回</h2>
<ul>
 	<li>カルマンフィルタの整理</li>
 	<li>パーティクルフィルタの数理</li>
</ul>
