---


---

<h2 id="maven-基本的认识">Maven 基本的认识</h2>
<h2 id="什么是maven">1. 什么是Maven?</h2>
<p>在平时开发中,经常遇到某个jar包,我在代码层已经Import 和@Automation了,编译器还是提醒你某个jar包找不到,往往这时来个mvn install 问题就解决了。可想而知，<strong>Maven 是帮助我们开发者管理Jar包的工具</strong></p>
<h2 id="maven基本命令">2. Maven基本命令</h2>
<h3 id="代码的编译">2.1 代码的编译</h3>
<pre><code> mvn compile
</code></pre>
<p>同样的，这里把项目jar代码编译成.class文件到项目的target文件夹</p>
<h3 id="安装包">2.2 安装包</h3>
<pre><code>mvn install 
</code></pre>
<p>编译好的.class文件，maven 自动地安装到本地Repository，即maven 的仓库。为什么要安装到仓库，这样的作用是什么？</p>
<ul>
<li>方便Maven工具快速找到相关的jar 包,引入项目里</li>
<li>集中管理项目的jar包</li>
</ul>
<h3 id="清理目标文件">2.3  清理目标文件</h3>
<pre><code>mvn clean 
</code></pre>
<p>maven 只对项目中的target 中的文件清理，原先的安装的文件不受影响。</p>
<h2 id="maven-pom">3. Maven POM</h2>
<h3 id="什么是pom？">3.1 什么是POM？</h3>
<p>POM代表项目对象模型。它是 Maven 中工作的基本单位，这是一个 XML 文件。它始终保存在该项目基本目录中的 <code>pom.xml</code> 文件。</p>
<pre class=" language-xml"><code class="prism  language-xml"><span class="token prolog">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>  
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>project</span> <span class="token attr-name">xmlns</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://maven.apache.org/POM/4.0.0<span class="token punctuation">"</span></span>  
  <span class="token attr-name"><span class="token namespace">xmlns:</span>xsi</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://www.w3.org/2001/XMLSchema-instance<span class="token punctuation">"</span></span>  
  <span class="token attr-name"><span class="token namespace">xsi:</span>schemaLocation</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://maven.apache.org/POM/4.0.0 
                           http://maven.apache.org/xsd/maven-4.0.0.xsd<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>  
 <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>modelVersion</span><span class="token punctuation">&gt;</span></span>4.0.0<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>modelVersion</span><span class="token punctuation">&gt;</span></span>  
 <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>com.lollipop.api<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>  
 <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>ali<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>  
 <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>1.0-SNAPSHOT<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>  
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>project</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<h3 id="pom中装包类型">3.2 POM中装包类型</h3>
<ul>
<li>装包的属性<pre class=" language-xml"><code class="prism  language-xml"> <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>packaging</span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>packaging</span><span class="token punctuation">&gt;</span></span>
</code></pre>
</li>
<li>装包类型</li>
</ul>
<ol>
<li>pom 类型，所有的父级项目的packaging都为pom</li>
<li>jar 类型，默认是jar类型，如果不作配置，maven会将该项目打成jar包，作为内部调用或者是作服务使用</li>
<li>war 类型，如果是需要部署的项目，则需要打包成war类型<br>
每个pom.xml 文件必需有project 、groupId、artifactId、version。<br>
|  元素 | 说明 |<br>
|:-------:|:----:|<br>
| project | 项目根目录 |<br>
| groupId | 公司或组织域倒序+项目 |<br>
| artifactId | 模块名称 |<br>
| version | 模块版本号 |</li>
</ol>
<h2 id="maven-依赖">4. Maven 依赖</h2>
<h3 id="依赖的范围">4.1依赖的范围</h3>
<h5 id="范围标签">4.1.1 范围标签</h5>
<pre class=" language-xml"><code class="prism  language-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
   <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
      <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>xxx.xx.x<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
      <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>xxx<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
      <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>4.0<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
      <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>scop</span><span class="token punctuation">&gt;</span></span>xxx<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>scop</span><span class="token punctuation">&gt;</span></span> #范围标签
   <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<h5 id="范围标签作用域值">4.1.2 范围标签作用域值</h5>
<ol>
<li>compile  范围依赖
<ul>
<li>对程序编译和打包期，该作用域有效</li>
</ul>
</li>
<li>test  范围依赖
<ul>
<li>对测试程序编译和运行期，该作用域有效</li>
</ul>
</li>
<li>procided 范围依赖
<ul>
<li>除打包和部署期无效后，其他期都有效</li>
</ul>
</li>
</ol>
<h3 id="依赖的继承">4.2 依赖的继承</h3>
<p>在项目里，如果多个子模块需要用到同个依赖包，我们可以提取它们到父 POM,子POM仅仅简单的引用<br>
父pom.xml</p>
<pre class=" language-xml"><code class="prism  language-xml"> <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>project</span><span class="token punctuation">&gt;</span></span>
 ...
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencyManagement</span><span class="token punctuation">&gt;</span></span>
   <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>group-a<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>artifact-a<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>1.0<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>

	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>exclusions</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>exclusion</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>group-c<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>excluded-artifact<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>exclusion</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>exclusions</span><span class="token punctuation">&gt;</span></span>

  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>

  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>group-c<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>artifact-b<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>1.0<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>type</span><span class="token punctuation">&gt;</span></span>war<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>type</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>scope</span><span class="token punctuation">&gt;</span></span>runtime<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>scope</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>

  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>group-a<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>artifact-b<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>1.0<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>type</span><span class="token punctuation">&gt;</span></span>bar<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>type</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>scope</span><span class="token punctuation">&gt;</span></span>runtime<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>scope</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
 <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencyManagement</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>project</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>子pom.xml</p>
<pre class=" language-xml"><code class="prism  language-xml">  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>project</span><span class="token punctuation">&gt;</span></span>
  ...
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
		  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>group-c<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
		  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>artifact-b<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
		  <span class="token comment">&lt;!-- This is not a jar dependency, so we must specify type. --&gt;</span>
		  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>type</span><span class="token punctuation">&gt;</span></span>war<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>type</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>

	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
		  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>group-a<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
		  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>artifact-b<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
		  <span class="token comment">&lt;!-- This is not a jar dependency, so we must specify type. --&gt;</span>
		  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>type</span><span class="token punctuation">&gt;</span></span>bar<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>type</span><span class="token punctuation">&gt;</span></span>
	  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>project</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<h3 id="规范依赖版号">4.3 规范依赖版号</h3>
<p>这里就不详细说明了。主要在父级pom里头加入版本号，子级pom简单引入就可以了</p>

