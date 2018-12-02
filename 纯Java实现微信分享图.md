纯Java实现微信朋友圈分享图
-------------------------------------
### 1.实现分享图的效果
![enter image description here](https://lh3.googleusercontent.com/u5Ee3nhBzzBMp58ONj51Z561R4kJ9SS-0BmnZvsxCZF0B0LEUWNYDfI-8amHcTONEXxrZzmhFS8 "朋友圈分享图")

### 2.开发环境
#### 2.1 JDK
	* oracle‘s jdk 1.8以上
#### 2.2 字体
	* 若选择了微软雅黑字体又是代码部署到Linux，则需要安装微软雅黑字体，字体安装方式自行google
### 3. 加载背景
#### 3.1  加载背景图
这是使用白色框底来作背景图[^1].
```java code
//这里从项目resources加载背景图，读文件到输入流，代码作了简列
InputStream background = null
BufferedImage zoomPicture = ImageIO.read(background);
```
### 4. 绘画头像
#### 4.1 头像裁剪
头像裁剪成半径
```
//头像半径
public static final int PROFILE_RADIUS = 80;
```
``` java code
// 2. 头像裁剪成圆形  
BufferedImage roundedImage = SharedImageUtils.createRoundedImage(new URL(userProfileUrl).openStream(), SharedImageUtils.PROFILE_RADIUS);
```
#### 4.2 头像绘画到背景图




[^1]: [link](https://picasaweb.google.com/106437634114917759264/6630213808569212145#6630213806186676098 "background.jpg)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1NDgzNTc0MSwtMjQwODY0MjgwLDk3Nj
E1NDA3NCwtNjUwNTUwMTI0LC0xNDc2ODkyNTkyLC0yMjcxMTYz
ODJdfQ==
-->