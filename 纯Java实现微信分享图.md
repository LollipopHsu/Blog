---


---

<h2 id="纯java实现微信朋友圈分享图">纯Java实现微信朋友圈分享图</h2>
<h3 id="实现分享图的效果">1.实现分享图的效果</h3>
<p><img src="https://lh3.googleusercontent.com/u5Ee3nhBzzBMp58ONj51Z561R4kJ9SS-0BmnZvsxCZF0B0LEUWNYDfI-8amHcTONEXxrZzmhFS8" alt="enter image description here" title="朋友圈分享图"></p>
<h3 id="开发环境">2.开发环境</h3>
<h4 id="jdk">2.1 JDK</h4>
<pre><code>* oracle‘s jdk 1.8以上
</code></pre>
<h4 id="字体">2.2 字体</h4>
<pre><code>* 若选择了微软雅黑字体又是代码部署到Linux，则需要安装微软雅黑字体，字体安装方式自行google
</code></pre>
<h3 id="加载背景">3. 加载背景</h3>
<h4 id="加载背景图">3.1  加载背景图</h4>
<p>这是使用白色框底来作背景图<sup class="footnote-ref"><a href="#fn1" id="fnref1">1</a></sup>.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token comment">//这里从项目resources加载背景图，读文件到输入流，代码作了简列</span>
InputStream background <span class="token operator">=</span> null
BufferedImage zoomPicture <span class="token operator">=</span> ImageIO<span class="token punctuation">.</span><span class="token function">read</span><span class="token punctuation">(</span>background<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="圆头像的实现">4. 圆头像的实现</h3>
<h4 id="头像裁剪">4.1 头像裁剪</h4>
<p>头像裁剪成半径</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token comment">//头像半径</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> PROFILE_RADIUS <span class="token operator">=</span> <span class="token number">80</span><span class="token punctuation">;</span>
</code></pre>
<pre class=" language-java"><code class="prism  language-java"><span class="token comment">// 2. 头像裁剪成圆形  </span>
BufferedImage roundedImage <span class="token operator">=</span> SharedImageUtils<span class="token punctuation">.</span><span class="token function">createRoundedImage</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">URL</span><span class="token punctuation">(</span>userProfileUrl<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">openStream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
							 SharedImageUtils<span class="token punctuation">.</span>PROFILE_RADIUS<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h4 id="背景图上绘画头像">4.2 背景图上绘画头像</h4>
<p>绘画位置</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token comment">/* 要放置的头像y坐标 */</span>
 <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> PROFILE_Y <span class="token operator">=</span> <span class="token number">1056</span><span class="token punctuation">;</span>
<span class="token comment">/* 要放置的头像X坐标 */</span>
 <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> PROFILE_X <span class="token operator">=</span> <span class="token number">90</span><span class="token punctuation">;</span> 
</code></pre>
<pre class=" language-java"><code class="prism  language-java"><span class="token comment">//頭像旁邊附帶文字(ps:字体是微软雅黑，linux不具备有，需要安装，)  </span>
BufferedImage profileImage <span class="token operator">=</span> SharedImageUtils<span class="token punctuation">.</span><span class="token function">mergePicture</span><span class="token punctuation">(</span>zoomPicture<span class="token punctuation">,</span>  
  roundedImage<span class="token punctuation">,</span>  
  nickName <span class="token operator">+</span> <span class="token string">" 为你推荐网批货源"</span><span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>PROFILE_X<span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>PROFILE_Y<span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>PROFILE_RADIUS<span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>PROFILE_RADIUS<span class="token punctuation">)</span><span class="token punctuation">;</span> 
</code></pre>
<h3 id="商品图案的显示">5. 商品图案的显示</h3>
<h4 id="绘画的位置和长宽">5.1 绘画的位置和长宽</h4>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> COPYWRITER_X <span class="token operator">=</span> <span class="token number">150</span><span class="token punctuation">;</span>  
<span class="token comment">/* 商店图案Y位置 */</span>  
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> SHOP_PIC_Y <span class="token operator">=</span> <span class="token number">70</span><span class="token punctuation">;</span>  
<span class="token comment">/*商店图案位置*/</span>  
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> SHOP_PIC_X <span class="token operator">=</span> <span class="token number">93</span><span class="token punctuation">;</span>  
<span class="token comment">/* 商店图案寬度 */</span>  
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> SHOP_PIC_WIDTH <span class="token operator">=</span> <span class="token number">900</span><span class="token punctuation">;</span>  
<span class="token comment">/* 商店图案長度 */</span>  
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> SHOP_PIC_LENGTH <span class="token operator">=</span> <span class="token number">950</span><span class="token punctuation">;</span>
</code></pre>
<h4 id="绘画图案">5.2  绘画图案</h4>
<pre class=" language-java"><code class="prism  language-java">shopImage <span class="token operator">=</span> SharedImageUtils<span class="token punctuation">.</span><span class="token function">mergePicture</span><span class="token punctuation">(</span>profileImage<span class="token punctuation">,</span> shopImage<span class="token punctuation">,</span> null<span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>SHOP_PIC_X<span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>SHOP_PIC_Y<span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>SHOP_PIC_WIDTH<span class="token punctuation">,</span> SharedImageUtils<span class="token punctuation">.</span>SHOP_PIC_LENGTH<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="文案的显示">6. 文案的显示</h3>
<h4 id="文案绘画的位置与字体大小">6.1  文案绘画的位置与字体大小</h4>
<pre class=" language-java"><code class="prism  language-java">BufferedImage textImage <span class="token operator">=</span> SharedImageUtils<span class="token punctuation">.</span><span class="token function">drawTextInImage</span><span class="token punctuation">(</span>shopImage<span class="token punctuation">,</span> <span class="token string">"档口: "</span> <span class="token operator">+</span> shopName<span class="token punctuation">,</span> <span class="token number">150</span><span class="token punctuation">,</span> <span class="token number">1200</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
<span class="token comment">//添加文案  </span>
BufferedImage mergeImage <span class="token operator">=</span> SharedImageUtils<span class="token punctuation">.</span><span class="token function">drawTextInImage</span><span class="token punctuation">(</span>textImage<span class="token punctuation">,</span> <span class="token string">"地址: "</span> <span class="token operator">+</span> shopAddr<span class="token punctuation">,</span> <span class="token number">150</span><span class="token punctuation">,</span> <span class="token number">1280</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
</code></pre>
<h3 id="二维码的显示">7. 二维码的显示</h3>
<h4 id="二维码的大小与位置">7.1 二维码的大小与位置</h4>
<pre class=" language-java"><code class="prism  language-java"><span class="token comment">/* 要放置的二维码寬度 */</span>  
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> QRCODE_WIDTH <span class="token operator">=</span> <span class="token number">230</span><span class="token punctuation">;</span>  
<span class="token comment">/* 要放置的二维码長度 */</span>  
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> QRCODE_LENGTH <span class="token operator">=</span> <span class="token number">230</span><span class="token punctuation">;</span>  
<span class="token comment">/* 要放置的二维码Y位置 往下为大值，往上为小值 */</span>  
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> QRCODE_Y <span class="token operator">=</span> <span class="token number">1070</span><span class="token punctuation">;</span>  
<span class="token comment">/*要放置的二维码X位置 往下为大值，往上为小值 */</span>  
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">final</span> <span class="token keyword">int</span> QRCODE_X <span class="token operator">=</span> <span class="token number">740</span><span class="token punctuation">;</span>
</code></pre>
<h4 id="二维码的绘画">7.2  二维码的绘画</h4>
<pre class=" language-java"><code class="prism  language-java">BufferedImage shopQrBuffer <span class="token operator">=</span> ImageIO<span class="token punctuation">.</span><span class="token function">read</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">URL</span><span class="token punctuation">(</span>shopQrUrl<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
mergeImage <span class="token operator">=</span> SharedImageUtils<span class="token punctuation">.</span><span class="token function">mergeQrcode</span><span class="token punctuation">(</span>mergeImage<span class="token punctuation">,</span>  
  shopQrBuffer<span class="token punctuation">,</span>  
  <span class="token string">"扫描或长按小程序码"</span><span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>QRCODE_X<span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>QRCODE_Y<span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>QRCODE_WIDTH<span class="token punctuation">,</span>  
  SharedImageUtils<span class="token punctuation">.</span>QRCODE_LENGTH<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h4 id="最终的分享图">8. 最终的分享图</h4>
<pre class=" language-java"><code class="prism  language-java"><span class="token comment">// 5. 生成分享图  </span>
ImageIO<span class="token punctuation">.</span><span class="token function">write</span><span class="token punctuation">(</span>mergeImage<span class="token punctuation">,</span> <span class="token string">"jpg"</span><span class="token punctuation">,</span> response<span class="token punctuation">.</span><span class="token function">getOutputStream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h4 id="源码">9. 源码</h4>
<ul>
<li><a href="https://github.com/SteamPako/sharedImagas.git">https://github.com/SteamPako/sharedImagas.git</a></li>
</ul>
<hr class="footnotes-sep">
<section class="footnotes">
<ol class="footnotes-list">
<li id="fn1" class="footnote-item"><p>[link](<a href="https://picasaweb.google.com/106437634114917759264/6630213808569212145#6630213806186676098">https://picasaweb.google.com/106437634114917759264/6630213808569212145#6630213806186676098</a> "background.jpg)<br>
这是使用的背景图是白色框底 <a href="#fnref1" class="footnote-backref">↩︎</a></p>
</li>
</ol>
</section>

