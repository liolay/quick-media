## 图片旋转问题修复
> 图片旋转作为一个常见功能，实际使用中用处挺多，但是这次实现却遇到了个小问题，记录一二

使用的几个类

- `Graphics2d` 
- `AffineTransform` 
- BufferedImage


### 1. Graphics2d 方式

利用Graphics2d的rotate方法来实现图片旋转，奇怪的是一直不生效，实现代码如下


```java
BufferedImage bufferedImage = ImageUtil.getImageByPath("bg.png");
Graphics2D g2d = bufferedImage.createGraphics();
g2d.rotate(Math.toRadians(90), bufferedImage.getWidth() >> 1, bufferedImage.getHeight() >> 1);
g2d.dispose();
```



### 2. `AffineTransform` 方式

```java
BufferedImage bufferedImage = ImageUtil.getImageByPath("bg.png");

AffineTransform tx = new AffineTransform();
tx.rotate(0.5, bufferedImage.getWidth() / 2, bufferedImage.getHeight() / 2);

AffineTransformOp op = new AffineTransformOp(tx,
        AffineTransformOp.TYPE_BILINEAR);
bufferedImage = op.filter(bufferedImage, null);
```


## 参考

- [Rotating a Buffered Image : Image « Advanced Graphics « Java](http://www.java2s.com/Code/Java/Advanced-Graphics/RotatingaBufferedImage.htm)