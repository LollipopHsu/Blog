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
### 4. 圆头像的实现
#### 4.1 头像裁剪
头像裁剪成半径
```java
//头像半径
public static final int PROFILE_RADIUS = 80;
```
```java
// 2. 头像裁剪成圆形  
BufferedImage roundedImage = SharedImageUtils.createRoundedImage(new URL(userProfileUrl).openStream(),
							 SharedImageUtils.PROFILE_RADIUS);
```
#### 4.2 背景图上绘画头像
绘画位置
```java
/* 要放置的头像y坐标 */
 public static final int PROFILE_Y = 1056;
/* 要放置的头像X坐标 */
 public static final int PROFILE_X = 90; 
```
```java
//頭像旁邊附帶文字(ps:字体是微软雅黑，linux不具备有，需要安装，)  
BufferedImage profileImage = SharedImageUtils.mergePicture(zoomPicture,  
  roundedImage,  
  nickName + " 为你推荐网批货源",  
  SharedImageUtils.PROFILE_X,  
  SharedImageUtils.PROFILE_Y,  
  SharedImageUtils.PROFILE_RADIUS,  
  SharedImageUtils.PROFILE_RADIUS); 
```
### 5. 商品图案的显示
#### 5.1 绘画的位置和长宽
```java
public static final int COPYWRITER_X = 150;  
/* 商店图案Y位置 */  
public static final int SHOP_PIC_Y = 70;  
/*商店图案位置*/  
public static final int SHOP_PIC_X = 93;  
/* 商店图案寬度 */  
public static final int SHOP_PIC_WIDTH = 900;  
/* 商店图案長度 */  
public static final int SHOP_PIC_LENGTH = 950;
```
#### 5.2  绘画图案
``` java
shopImage = SharedImageUtils.mergePicture(profileImage, shopImage, null,  
  SharedImageUtils.SHOP_PIC_X,  
  SharedImageUtils.SHOP_PIC_Y,  
  SharedImageUtils.SHOP_PIC_WIDTH, SharedImageUtils.SHOP_PIC_LENGTH);
```
### 6. 文案的显示
#### 6.1  文案绘画的位置与字体大小
```java
BufferedImage textImage = SharedImageUtils.drawTextInImage(shopImage, "档口: " + shopName, 150, 1200);  
//添加文案  
BufferedImage mergeImage = SharedImageUtils.drawTextInImage(textImage, "地址: " + shopAddr, 150, 1280);  
```
### 7. 二维码的显示
#### 7.1 二维码的大小与位置
```java
/* 要放置的二维码寬度 */  
public static final int QRCODE_WIDTH = 230;  
/* 要放置的二维码長度 */  
public static final int QRCODE_LENGTH = 230;  
/* 要放置的二维码Y位置 往下为大值，往上为小值 */  
public static final int QRCODE_Y = 1070;  
/*要放置的二维码X位置 往下为大值，往上为小值 */  
public static final int QRCODE_X = 740;
```
#### 7.2  二维码的绘画
```java
BufferedImage shopQrBuffer = ImageIO.read(new URL(shopQrUrl));  
mergeImage = SharedImageUtils.mergeQrcode(mergeImage,  
  shopQrBuffer,  
  "扫描或长按小程序码",  
  SharedImageUtils.QRCODE_X,  
  SharedImageUtils.QRCODE_Y,  
  SharedImageUtils.QRCODE_WIDTH,  
  SharedImageUtils.QRCODE_LENGTH);
 ```
 #### 8. 最终的分享图
 ```java
 // 5. 生成分享图  
ImageIO.write(mergeImage, "jpg", response.getOutputStream());
```

  #### 9. 源码
  * https://github.com/SteamPako/sharedImagas.git





[^1]: [link](https://picasaweb.google.com/106437634114917759264/6630213808569212145#6630213806186676098 "background.jpg)
这是使用的背景图是白色框底

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg0NTQ3MTM1MywtMTY1MDMzMDE2NCwyMD
Y2MjUzMjcwLDU1NjkzMTYyNSwyMDQxODA4MDUzLC05ODI4NDM4
OTcsLTIwMTc5OTUwNTEsLTEzNDQ2OTIyOTYsLTI0MDg2NDI4MC
w5NzYxNTQwNzQsLTY1MDU1MDEyNCwtMTQ3Njg5MjU5MiwtMjI3
MTE2MzgyXX0=
-->