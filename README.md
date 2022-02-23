![Travis build status](https://api.travis-ci.org/sejda-pdf/webp-imageio.svg?branch=master)



# 使用说明
maven项目的pom.xml添加以下依赖
````xml
        <dependency>
            <groupId>net.ifok.image</groupId>
            <artifactId>webp4j</artifactId>
            <version>1.0.0</version>
        </dependency>
````
## 转换为其他格式

WebP 图片可以使用默认设置进行解码，如下所示。

```
BufferedImage image = ImageIO.read(new File("/path/input.webp"));
ImageIO.write(image,"png",new File("d:\\tmp\\11.jpg"));
```

需要自定义 WebP 解码器设置，您需要创建 ImageReader 和 WebPReadParam 的实例进行配置

```
// 获取 WebP ImageReader 实例 
ImageReader reader = ImageIO.getImageReadersByMIMEType("image/webp").next();

// 配置解码参数 
WebPReadParam readParam = new WebPReadParam();
readParam.setBypassFiltering(true);

// 在 ImageReader 上配置输入 
reader.setInput(new FileImageInputStream(new File("input.webp")));

// 解码图片
BufferedImage image = reader.read(0, readParam);
```

## 转换为webp格式

编码以与解码类似的方式完成。

您可以使用 Image I/O 便捷方法使用默认设置进行编码。

```
// 从某处获取要编码的图像 
BufferedImage image = ImageIO.read(new File("input.png"));

// 使用默认设置将其编码为 webp 
ImageIO.write(image, "webp", new File("output.webp"));
```

或者，您可以创建 ImageWriter 和 WebPWriteParam 的实例以使用自定义设置。

```
// 从某处获取要编码的图像 
BufferedImage image = ImageIO.read(new File("input.png"));

// 获取 WebP ImageWriter 实例 
ImageWriter writer = ImageIO.getImageWritersByMIMEType("image/webp").next();

// 配置编码参数 
WebPWriteParam writeParam = new WebPWriteParam(writer.getLocale());
writeParam.setCompressionMode(ImageWriteParam.MODE_EXPLICIT);
writeParam.setCompressionType(p.getCompressionTypes()[WebPWriteParam.LOSSLESS_COMPRESSION]);

// 在 ImageWriter 上配置输出 
writer.setOutput(new FileImageOutputStream(new File("output.webp")));

// 编码
writer.write(null, new IIOImage(image, null, null), writeParam);
```



# Forked 仓库地址
This is a fork from [luciad/webp-imageio](https://bitbucket.org/luciad/webp-imageio/)
# 相关文章
[Java Image I/O](http://docs.oracle.com/javase/7/docs/api/javax/imageio/package-summary.html) reader and writer for the
[Google WebP](https://developers.google.com/speed/webp/) image format.


# 支持平台
- windows (32, 64 bit)
- linux (64 bit)
- mac (64 bit)

--------------

# 修改内容
- 本地动态文件保存于jar包无需额外对jdk添加配置
- 发布到中央仓库 (`net.ifok.image`:`webp4j` artifact)

# 许可
webp-imageio is distributed under the [Apache Software License](https://www.apache.org/licenses/LICENSE-2.0) version 2.0.
